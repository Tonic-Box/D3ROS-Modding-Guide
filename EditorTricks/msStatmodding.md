# Statmodding: 11... to 99...  
So another neat trick with statmodding, on your mainstats (int, str, dex, vit) instead of showing `10...` you can actually have it show any 2 numbers followed by dots that you want. And the math here is very simple.  
  
basically, take the number you want to show, multiply that by -100m, then divide that number by 5. And the resulting number is what you would set the stat as.  
`({NumberToShow} * -100m) / 5`  
  
Lets take `75...` as an example. So we want to show 75... so we multiply `75` by `-100m` which gives us `-7500m` then we divide that by 5 (since we are dealing with paragon) and that leaves us with `-1500m` which is what you would put as the stat to have it show the `75...`  
  
Now on your end it will show `-7500m`. However for others in your lobby they will see `-75...`  

### Cheatsheet  
Heres a quick cheatsheet of some of the numbers for refference.  
* **[25]** `-500,000,000`  
* **[50]** `-1,000,000,000`  
* **[75]** `-1,500,000,000`  
* **[99]** `-1,980,000,000`  

### Credit
* bdawgg_73
