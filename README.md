# Drawing-Board
A drawing board made in p5.js by Billy Mooney

### Code
```js
// Collection of paints so it can update every paint.
let paint = [];

function setup(){
   // Create the canvas in p5
   createCanvas(600, 600); 
}

function draw(){
  background(255);
  resetButton(); 
  painting();
  update();
}

function update(){
  // Updates the "paint" every 10 ticks.
  for(let i = 0; i < paint.length; i++){
    paint[i].draw();  
  }
}

function painting(){
  // If M1 is pressed and the cursor isn't in the reset button it will paint.
  if(mouseIsPressed){
    if(!resetPressed()){
      var p = new Paint(mouseX, mouseY);
      print(mouseX + ":" + mouseY);
      paint.push(p);
    }
  }
}

function resetButton(){
  // Reset button creation.
  fill(0);
  rect(550, 550, 40, 40);
  fill(255);
  text("Reset", 554, 574);
  // If M1 is pressed and cursor is ontop of the button it will clear drawing.
  if(mouseIsPressed){
    if(resetPressed()){
      clearDrawing();
    }
  }
}

function clearDrawing(){
  print("Cleared drawing board.");
  // For each Paint they will be removed.
  for(let i = 0; i < paint.length; i++){
    paint[i].remove(); 
  }
}

function resetPressed(){
  // Dist returns a double of how far a point is from another point.
  let distance = dist(570, 570, mouseX, mouseY);
  // If the distance is less than or equal to 20 return true else false.
    if(distance <= 20){
       return true; 
    } else {
       return false; 
    }
}

class Paint {
    constructor(x, y){
      this.x = x;
      this.y = y;
      this.draw();
      this.removed = false;
    }
  
    remove(){
      this.removed = true; 
    }
  
    x(){
      return this.x; 
    }
  
    y(){
      return this.y; 
    }
  
    draw(){
      // If it hasn't been removed draw the paint.
      if(!this.removed){
        fill(0);
        noStroke();
        ellipse(this.x, this.y, 5, 5);
      }
    }
}
```

