# Drawing-Board
A drawing board made in p5.js by Billy Mooney

### Code
```js
let paint = [];

function setup(){
   createCanvas(600, 600); 
}

function draw(){
  background(255);
  resetButton(); 
  painting();
  update();
}

function update(){
  for(let i = 0; i < paint.length; i++){
    paint[i].draw();  
  }
}

function painting(){
  if(mouseIsPressed){
    if(!resetPressed()){
      var p = new Paint(mouseX, mouseY);
      print(mouseX + ":" + mouseY);
      paint.push(p);
    }
  }
}

function resetButton(){
  fill(0);
  rect(550, 550, 40, 40);
  fill(255);
  text("Reset", 554, 574);
  if(mouseIsPressed){
    if(resetPressed()){
      clearDrawing();
    }
  }
}

function clearDrawing(){
  print("Cleared drawing board.");
  for(let i = 0; i < paint.length; i++){
    paint[i].remove(); 
  }
}

function resetPressed(){
  let distance = dist(570, 570, mouseX, mouseY);
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
      if(!this.removed){
        fill(0);
        noStroke();
        ellipse(this.x, this.y, 5, 5);
      }
    }
}
```

