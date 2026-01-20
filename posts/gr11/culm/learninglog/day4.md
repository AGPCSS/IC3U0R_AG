[back](../index.md)
# Learning Log - Day 4
Today I was able to put the images and assets I made yesterday into use and made my game look more professional. To do this, I had to swap out only a little bit of code and change up some logic like how I render the cells in the grid. I did however make a new function that I’m quite proud of.

```
​​void drawCustomRect(int X, int Y, int sX, int sY) {
  randomSeed(X + Y + sX + sY);
  
  int id1 = (int)(random(1, 4));
  int id2 = (int)(random(1, 4));
  
  while (id1 == id2) {
    id2 = (int)(random(1, 4));
  }
  
  ArrayList<PImage> images = Images120x50;
  
  if (sX == 160 && sY == 50) images = Images160x50;
  else if (sX == 50 && sY == 50) images = Images50x50;
  else if (sX == 400 && sY == 400) images = Images400x400;
  
  image(images.get(cycleImages ? id1 : id2), X - 5, Y - 5, sX + 10, sY + 10);
}
```

This function was made to put in the custom button and frame images into use. Since I intended on making my game look like it was hand drawn, I wanted to make it cycle between images. To do this I had to give each button two different images and make them cycle between one another. To give each button consistent images I used randomSeed to a number based off of the buttons position and size, giving each a unique set of random numbers. From there I generated two random numbers which will correspond to what image it will use. I also added a fail safe that changes up the second id until it's different from the first using a while loop (repetition). From there, the code decides which array of images it will use with a couple of statements (selection) based on the rects size.

I also made some code to optimize the amount of lines I use with the following function

```
void loadImages(ArrayList list, String prefix, int max) {
  for (int i = 1; i <= max; i++) {
    list.add(loadImage("data/" + prefix + i + ".png"));
  }
}
```

This function allows me to iterate (repetition) through 1 to n and append the image to an array for later use. An example of this is `loadImages(Images400x400, "400x400_", 4)`. Which will append all images with the prefix 400x400_ to an array. 

I also added a new gamemode; fog of war. The logic to make this took some thinking and even required some math to be done. In the logic for this game mode I used the interpolation formula: 

```
float lerp(float a, float b, float t) {
   return a + (b - a) * t
}
```

I’ve found this function helpful before so I implemented it into Processing but later realized this function already existed as a global function provided by Processing, so I got rid of it. Now, for my logic, I had to make tiles fade away upon being clicked. So I had to use millis() and subtract the time the cell was clicked and use that for my t variable. Doing this made sure the tile fades away over time. Making it fade over time took a little while until I realized I can simply get the difference between when the cell was clicked and the current time and divide it by 1000 to get the amount of seconds it's been since the cell was clicked and use that in the lerp function.
```
      if (fogOfWarEnabled && data.length > 0 && !stopGame) {
        tint(255, lerp(0, 255, (millis() - data[3]) / 1000.0));
        image(cellImages.get(7), x * cellSize, y * cellSize, cellSize, cellSize);
        tint(255, 255);
      }
```
