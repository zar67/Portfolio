---
layout: post
title:  "Making A Combat System In Unity"
date:   2020-03-10 16:00:00 +0000
categories: [Gameplay Programming Module]
---

Our final task in Gameplay Programming is to create a combat system with a Slime enemy, similar to those seen in Minecraft. This task is split basically into two parts: the player's combat and the enemy. ​This is the specification:

<img src="{{ site.baseurl }}/assets/Blog/GPCombat/combat_objectives.png"/>

I will need to setup the player to attack and receive damage as well as setting up a Slime that will jump towards the player and split into smaller slimes when hit

<h3>Registering Hits and Deaths</h3>

Previously in this module we were given the task to create a player character, during this I implemented some attacks and a death animation into my character script. This means that when setting up a combat system I can simply run the right attack animation and call the Death function when needed. 

The way I am registering hits is by using triggers; if something enters the trigger and the player is in an attack state, then the colliding object should be attacked. 

There will be a similar setup on the enemy Slime. On each of the 3 colliders (one for each hand and the sword) there is an attack manager script which will attack the relevant objects if needed. To test this, I created a blank cube and added a new script called Slime.

```C#
private void OnTriggerStay(Collider other)
{
    Slime enemy = other.gameObject.GetComponent<Slime>();
    AttackEnemy(enemy);
}

void AttackEnemy(Slime enemy)
{
    if (enemy != null)
    {
        if (!enemy.hit && player.playerAttacking())
        {
            enemy.hit = true;

            if (player.GetComponent<Animator>().GetBool("armed"))
            {
                enemy.TakeDamage(player.attack_damage * 2);
            }
            else
            {
                enemy.TakeDamage(player.attack_damage);
            }
            hit_something = true;
        }

        if (!player.playerAttacking())
        {
            enemy.hit = false;
            hit_something = false;
        } 
    }
}
```

<h3>Adding an Enemy</h3>

Now that my player can attack, they need something to attack. I improved the look of my basic cube to make it look similar to a gelatinous slime and setup similar trigger functions so that when the player walks into the cube, they are damaged.

<img src="{{ site.baseurl }}/assets/Blog/GPCombat/slime.png"/>

```C#
private void OnTriggerStay(Collider other)
{
    if (other.gameObject.tag.Equals("Player"))
    {
        attack_timer += Time.deltaTime;

        if (attack_timer > attackDelay)
        {
            attack_timer = 0;
            other.GetComponent<RPGCharacterController>().DamagePlayer(attack_damage);
            jumping = false;
        }
    }
}
```

I added a delay to the slime in the OnTriggerStay function, since when the player collided with the slime, they lost all their health immediately. Now, the slime attacks the player on collision with them and if the player stays colliding will only attack after a given delay. 

I also setup a call to my Death() function so that when the player's health gets to low, the player dies and cannot do anything else.

<img src="{{ site.baseurl }}/assets/Blog/GPCombat/player_death.png"/>

<h3>Splitting</h3>

One important feature I still need to implement is the slime splitting. I've setup a size enum (SMALL, MEDIUM, LARGE) and added a starting size and size scaling variables to the slime. 

Starting size is a size variable and determines how big the slime should be at the start of the game and size scaling is a list which allows the user to define how big (scale wise) each size of slime should be. 

On awake I setup the health of the slime to be baseHealth * ((int)startSize + 1) meaning large slimes have more health than smaller slimes. When the slimes health gets smaller than 0, if the size isn't small, I call the Split() function as show below:

```C#
void Split()
{
    Slime obj_1 = Instantiate(this);
    SetupNewSlime(obj_1);

    Slime obj_2 = Instantiate(this);
    SetupNewSlime(obj_2);

    Destroy(this.gameObject);
}

void SetupNewSlime(Slime slime)
{
    float scale = sizeScaling[(int)startSize - 1];

    slime.startSize = current_size - 1;
    slime.health = baseHealth * ((int)slime.startSize + 1);
    slime.current_size = slime.startSize;
    slime.transform.position = RandomSpawnPosition();
    slime.transform.localScale = new Vector3(scale, scale, scale);
    slime.attack_damage = baseAttackDamage * ((int)slime.startSize + 1);
}
```

This function instantiates two new slimes, a size down from the current size, and deletes the original slime. A new random position in a range is calculated, so the new slimes don't spawn on top of each other. If the slime is already a "small" slime, the object is simply deleted instead of being split.

<h3>Slime Movement</h3>

The final major feature to implement is the slime movement, I first setup a patrol area (using a central position and a size) then got the slimes to randomly chose a position in that area and move towards it. The slimes move by jumping, they move continuously forward as they jump and then are delayed after they land before they can jump again. Here is the movement for my slimes:

```C#
void Move(Vector3 direction)
{
    Vector3 rotation = Quaternion.Lerp(
                            transform.rotation, 
                            Quaternion.LookRotation(direction, transform.up), 
                            moveSpeed * Time.deltaTime).eulerAngles;
    transform.rotation = Quaternion.Euler(0, rotation.y, 0);

    if (jumping)
    {
        rigid_body.velocity += direction.normalized * moveSpeed * Time.deltaTime;
    }
    else
    {
        move_timer += Time.deltaTime;

        if (move_timer > moveDelay)
        {
            move_timer = 0;
            rigid_body.velocity = Vector3.up * jumpForce;
            jumping = true;
        }
    }
}
```

If the player comes into range of the slime, then the direction vector passed into the function is the direction to the player, if not a random position in the patrol area is chosen and the slime moves towards that. When the slime hits its target position, a new position is generated. The jumping boolean is set to false in OnTriggerEnter when the slime hits the ground.

<h3>Slime Animations and Particles</h3>

After implementing all the features, my slimes still seem pretty dull, and so I've decided to add some animations and a death particle effect to liven them up a bit. The animations for the slime are simply: jump, fall and land, setting the y-scale to a different value so they look as if they are gelatinous. I have also added a hit animation to turn the slimes red for a small amount of time when they are hit.

<img src="{{ site.baseurl }}/assets/Blog/GPCombat/slime_animation.png"/>

I created a simple death particle of a bunch of cubes which I instantiate when a slime splits or dies. These particles have on them the ParticleController script I made when implementing my collectables, so they are destroyed when they finish playing. 

<img src="{{ site.baseurl }}/assets/Blog/GPCombat/death_particles.png"/>

The final touch I added was adding some UI to show the health of the slimes (above their heads) and the player (top right).

<div class="iframe-container">
<iframe src="https://youtu.be/cLCNPkS0cgQ" frameborder="0" allowfullscreen></iframe>
</div>