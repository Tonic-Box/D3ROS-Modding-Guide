# Statmodding: Advanced
First, if you haven’t, go back, and read the Statmoding Basics course.  

With statmodding, there are many fancy things people do with it. Such as making all your stats show only dots, making all your stats show 0s while still able to deal out damage, and more! I will give some spoilers here, but mostly I will be discussing and teaching the math behind statmoding and manipulating those sheet stats. That way you can do your own unique statmods. :)

### Dots
So, if you are unaware, there is a way to get each of the 7 sheetstat numbers to show only 3 dots (`...`). This comes from a combination of rounding and from viewport limitations. Basically, if you have the stat over 10m, 10b, etc, it'll show some numbers followed by dots. However if you get it just shy of that 10 mark, d3 will actually round it up to 10. This will still show numbers with 3 dots. However if that’s rounding as a negative (eg just shy of -10m, -10b, etc) then as a result it will only show 3 dots with no numbers.

_**A small spoiler**_  
We'll take the mainstats for instance (Dexterity, Intelligence, Strength, and Vitality) as our spoiler discussion.    

So essentially what we are going to try to hit is as close to 9,999,999,999 on each as we can (maybe with a little buffer room to account for stat that may or may not be on gear). So let take into consideration since with stat moddding we are dealing in paragon points, each point is worth 5 mainstat.   

So what is 9,999,999,999 divided by 5? A quick pop into the calculator tells us `1,999,999,999.8`. So that number would work. But we want a little buffer room to account for gear. so lets say, 1,999,999,500 which multiplied by 5 would be `9,999,997,500` which is close enough that it will still round. But remember we need negative to get the dots, so, we would put `-1,999,999,500` paragon in each mainstat for the dots.

For the rest, I'll leave that to you. Remember, EVERYTHING is multiplicative of other things. So toy around and I promise you'll get it. However I will give a few tips:  

**Generally speaking some key values you'll want:**  
**Crit Damage:** This is multiplicative with mainstat for sheet damage so will want this to be negative.  
**Hidden Life stat:** There is a hidden base life stat. You will need to edit this via the raw tab in attributes. Its key is `-3632`  

### Full 21 Dots Spoiler
<details>
  <summary>~Spoiler~</summary>
  <p>  
    
  **The numbers may be slightly different on different systems, but heres the general numbers for 21 dots.**  
  * **Int, Dex, Str, Vit:**   `-1,999,999,500`  
  * **Resist All:**           `225,000,000` (May need to be altered slightly based on system)  
  * **Life Percent:**         `-2,147,483,647`  
  * **Life Regen:**           `0`  
  * **Life Per Hit:**         `-2,147,483,647`  
  * **Armor:**                `-200`  
  * **Crit Chance:**          `2,147,483,647`  
  * **Crit Damage:**          `-2,147,483,647` (May change depending on gear and system if you want DPS dots)  
  </p>
</details>


### Other statmod types
The only difference in running different fancy statmods is working the math to match it! People have done lots of things, from 666b in all, to 0 in all, etc. Just got to get creative and weird with it. :)  
  
### Credit
* D-R-A-S-T-I-C
* Syite
