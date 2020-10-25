# Statmodding Others, remotely Over a Lobby (switch)
This can be quite a useful trick for helping out those who can’t statmod themselves. However, it does have its limitations. Normally, when accessing your own stats via memory, there are 4 Heap addresses you'll find that have to do with each stat.  

_NOTE: You must be the lobby host to accomplish this_  

### The logic, limitations, and Theory Crafting

A brief explanation as I understand their function currently:
* **ADDR_1:** This is the address that directly mirrors and can cause updates to your save file
* **ADDR_2:** This is the address that displays on your paragon tabs
* **ADDR_3:** This is the address that directly factors into your stat equations
* **ADDR_4:** Not sure yet, but, it's there.
  
They all mirror and can affect each other in different ways depending on the situation. Normally when modding yourself via memory, you’d just change all 4 addresses to the number you want for the stat. But it gets a little trickier when accessing someone else’s stats in memory over a lobby.  
  When you attempt to find the addresses for someone else’s stats over a lobby, you will only be able to access addresses 2, 3, and 4. Which... Poses us with a hard limitation of not being able to break the positive number cap. This is because, those 3 can be made to affect the 1st address on their side and hence mod their stats, writing it to their save file. However, there are hard code checks on that 1st address.
  Now you can set any stat as far negative as you want with no issue, but can’t break the 50 point caps going positive. So that leaves us with Mainstat and Vitality which seemingly don’t have a cap, right? Wrong! Unfortunately, that apparently do. They have a positive cap of 100k, hence our last limitation.  
  
### So, to condense.. Our limitations and bounds to work in are:  
  * Mainstat & Vitality have a Positive cap of `100,000`
  * We cannot break positive caps (otherwise it will not write the change to their save file)
  * We have a limit of `-2,147,483,648` going negative on any stats (Just the limit of the data type used, sInt32)
  
### In Practice
  
 In practice, it works much the same as finding any other values in memory, except with a small twist. That twist is, there is a trick we have to do to get the 3 addresses we have access to, to force an update to that 1st address we can’t access directly to get the modded values written to the guests save.  
 
_NOTE: I will detail out the steps to giving `100k` in mainstat and vitality over a lobby here. But the same general principals/methodology will work for any stat._  

**1.** First, have them set the stat you want to mod (mainstat or vital) so some arbitrary value, then pop into EdiZon and search for that value.  
**2.** have them change it to a different value, then search your previous results for that new value.  
**3.** In the end you should be left with 3 addresses.  
**4.** put `99995` into all 3 addresses.  
**5.** to force the backwards update to that 1st address, have them:  
    - Spend 5 more points on that stat.  
    - Then, un-equip and re-equip any piece of gear.  
**6.** At this point they should have the stat and should be done with that one.  
**7.** Rinse and repeat. :)  
