[back](../index)
# Learning Log - Day 2
Learning Log 2
Today, I got to finish a huge part of the main gameplay. I completed bomb generation which used repetition (a while loop) to do. I changed my array variables to ArrayLists for dynamic use. And wrote plenty of new custom functions that will help me optimize code and lower the amount of lines.

One of the most important methods (custom function) in my code currently is called searchArrayIndex and searchArray:

```
int searchArrayIndex(ArrayList<int[]> array, int X, int Y) {
  int result = -1;

  for (int i = 0; i < array.size(); i++) {
    int[] data = array.get(i);

    if (data[0] == X && data[1] == Y) {
      result = i;

      break;
    }
  }

  return result;
}
```

Here is searchArrayIndex, which iterates through the given array and looks for X and Y inside of the index. If they’re the same, it returns the results index. This is used to search through arrays like bombs, uncovered, and flags to find the properties of a certain cell. This method also uses repetition to iterate through the array and compare the index to the given information (X and Y).

Another important feature in my code is the (selection) structure when my code is rendering the grid. The order of the code matters since we're working with drawing things on the players screen.

```
      int[] data = searchArray(uncovered, x, y);
      
      if(cellIsFlagged(x, y)) {
        fill(255, 0, 0);
      } else if (cellIsBomb(x, y)) {
        fill(125, 125, 125);
      } else if (data.length <= 0) {
        fill(125, 125, 125);
      } else {
        fill(255, 255, 255);
      }
      
      rect(x * cellSize, y * cellSize, cellSize, cellSize);
      
      if (data.length > 0 && data[2] > 0) {
        textSize(30);
        textAlign(CENTER, CENTER);
        fill(0, 0, 0);
        text(data[2], x * cellSize + cellSize / 2, y * cellSize + cellSize / 2);
        fill(125, 125, 125);
      }
```

In this snippet of code, it first starts with checking the properties of the cell. From there it checks; the cell is flagged, is a bomb, is uncovered, otherwise it is blank. From there it will change the color of the cell and draw it. Afterwards, it checks if the cell is uncovered and if there are more than one bomb around the cell. If so, it will draw text OVER the cell which displays the amount of bombs around the cell.
