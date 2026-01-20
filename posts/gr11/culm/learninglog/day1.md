[back](../index.md)
# Learning Log - Day 1
```
PImage logo; // The games logo
PImage backgroundImage; // the background image of the main menu

boolean won; //whether or not the player has won
boolean inGame; // variable that determines if the player is in the main menu or in game
boolean endScreen; // determines if the end screen (win/death) is enabled
boolean statisticsPageEnabled; // determines if the statistics screen on the main menu is enabled

int[][] bombs; // coordinates of cells that are a bomb
int[][] flags; // coordinates of cells that are flagged
int[][] uncovered; // coordinates of uncovered cells

float time; // the amount of time that the game has been going on / how much time is left
float frames; // used for sin and cos

JSONObject save; // the players save data
```

Minesweeper is a game that's heavily reliant on arrays. This is because of the grid of cells which hold different data within them. Each cell has 3 properties, whether or not it is a bomb, uncovered, or flagged. Each of these 3 properties have their own array; bombs, flags, and uncovered. Inside of these arrays will be another array that will hold the `{X, Y}` values, with one exception; uncovered will have `{X, Y, bombs}`, bombs being the amount of bombs around the cell (this is done for optimization purposes). Another datatype I will be using is the JSONObject datatype. This datatype will help me easily convert an array into a string so I can save the data into a file while still being able to convert the string back into a JSONObject and being able to index what I want from the save data. 
