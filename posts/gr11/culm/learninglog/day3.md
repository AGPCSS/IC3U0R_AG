# Learning Log - Day 3
Today, I completed the main gameplay and also added one of my three gamemodes, inverted. To start with, I implemented the usage of switch cases (selection structure) multiple times throughout my code. This was done to simplify my code and make it look better rather than having multiple else if statements (to fit my taste in “good looking code”).

```
  for (int i = 0; i < 4; i++) {
    if (mouseButtonClick(X, 560 + sY + 10, sX, sY)) {
      println("SET DIFF TO " + buttonNames[i]);
      
      switch(buttonNames[i]) {
        case "Easy":
          nextGridSize = 8;
          nextTotalBombs = 10;
          nextMode = "Easy";
          
          break;
        case "Medium":
          nextGridSize = 10;
          nextTotalBombs = 25;
          nextMode = "Medium";
          
          break;
        case "Hard":
          nextGridSize = 20;
          nextTotalBombs = 100;
          nextMode = "Hard";
          
          break;
        case "Restart":
          restart();
          
          break;
        default:
          break;
      }
    };
    
    X += padding + sX;
  }
  ```

This code is part of the handleInGameButtons method which registers the clicks of the in-game screen buttons at the bottom of the screen. This code specifically manages the difficulty and restart buttons. The code uses a for loop (repetition) to iterate through 0 to 3, which can be used to calculate the position of the buttons and also give each button a unique id (the i variable). After checking if the button is pressed, the switch case is initiated and translates the id to text via usage of the buttonNames array, which the switch case goes off of to determine what to do next. Each case represents a button with their corresponding names (variables and data tracking), which makes the rest self explanatory.

I also was able to complete saving data with these two methods:

```
JSONObject readData() {
  try {  
    BufferedReader file = createReader("save.txt");
    
    if (file == null) {
      throw new IOException("save file not found");
    }
    
    String data = file.readLine();
   
    JSONObject json = JSONObject.parse(data);
    
    file.close();
    
    currentSave = json;
    
    return json;    
  } catch(IOException error) {
    JSONObject newData = new JSONObject();
    JSONObject easy = new JSONObject();
    JSONObject medium = new JSONObject();
    JSONObject hard = new JSONObject();
    
    easy.setFloat("time", 0.0);
    easy.setInt("modifierPoints", 0);
    easy.setBoolean("inverted", false);
    easy.setBoolean("fogOfWar", false);
    easy.setBoolean("greenLightRedLight", false);
    
    medium.setFloat("time", 0.0);
    medium.setInt("modifierPoints", 0);
    medium.setBoolean("inverted", false);
    medium.setBoolean("fogOfWar", false);
    medium.setBoolean("greenLightRedLight", false);
    
    hard.setFloat("time", 0.0);
    hard.setInt("modifierPoints", 0);
    hard.setBoolean("inverted", false);
    hard.setBoolean("fogOfWar", false);
    hard.setBoolean("greenLightRedLight", false);
    
    newData.setJSONObject("Easy", easy);
    newData.setJSONObject("Medium", medium);
    newData.setJSONObject("Hard", hard);
    
    currentSave = newData;
    
    saveData();
    
    println("no save data found, creating new data.");
    
    return currentSave;
  }
}

boolean saveData() {
  PrintWriter writer = createWriter("save.txt");
  
  String json = currentSave.toString();
  
  // stupid bug fix
  json = json.replace("\n", " ");
  
  writer.println(json);
  writer.flush();
  writer.close();
  
  println("saved data!");
  
  return true;
}
```

All that these two methods do is; get the saved data (JSONObject) and also save the players data. First, the readData method. Using a try catch block (error checking/restrictions), it checks if the file exists by stopping the code from erroring “file not found”. If it errors, that means the file was not found, so in the catch block it creates a blank save file with no stats and saves it. From there, the save method creates/edits a file called save.txt and updates its contents to a JSON, which can easily be turned back into a JSONObject via the method JSONObject.parse. However, this is where I ran into an issue. For some reason, the JSON string was formatted, which caused problems with reading the file and putting it through JSONObject.parse. To solve this problem, I partially got rid of the formatting as seen under the “stupid bug fix” comment, where I got rid of all new lines. This made it easier to put the files contents through JSONObject.parse, in other words, read the saved data.
