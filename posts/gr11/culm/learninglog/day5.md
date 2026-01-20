[back](../index.md)
# Learning Log - Day 5

Today I implemented the Green Light Red Light gamemode. This gamemode is heavily reliant on time so I had to think of some logic for how the red light will work and ended up with this function.

```
void updateRedLight() {
  if (!currentModifiers[2]) {
    return;
  }
  
  randomSeed(millis());
  
  if (nextRedLight == 0 || nextRedLight + redLightLength * 1000 < millis()) {
    int next = (int)(random(redLightFrequency[0], redLightFrequency[1]) * 1000);
    
    nextRedLight = next + millis();
  }
  
  redLight = nextRedLight < millis() && nextRedLight + redLightLength * 1000 > millis();
}
```

This function runs every frame (in the draw method) and constantly updates and registers the red light. How it works is it calculates if the red light has already passed (`nextRedLight + redLightLength * 1000 < millis()`) or if the game hasn’t initialized a time yet (`nextRedLight == 0`). If any of those conditions are true, the game uses the random method to generate a random next time depending on the redLightFrequency which is dictated by the game's difficulty. The very last expression in the method calculates whether or not the current time is in between `nextRedLight` and when the red light ends (`nextRedLight + redLightLength * 1000 > millis()`). Then it sets the boolean variable `redLight` accordingly. 

```
  if (redLight && millis() > nextRedLight + redLightMercy) {
    death();
    
    return;
  }
  ```

This if statement is under the clickCell method, which registers the clicks on the grid. All this if statement does is end the game upon clicking the grid when it’s a red light. It also gives the player some mercy by delaying the time the end game starts to register. This is done by adding onto nextRedLight and comparing the current time to the new time. Giving the player some mercy and time to realize the light is red before it starts to register clicks upon red light.

The rest of my time I used to add comments to my code and will continue doing so on Monday.
