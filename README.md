# A-team-Game-of-Codecool
week0 TW source code

//item and char size variables
var characterSize = 0.2;
var collectibleSize = 0.2;

//timer
var timer = 120;

//edges
createEdgeSprites();

//our forest and end screen
var background_forest = createSprite(200, 200);
background_forest.setAnimation("forest");

var endScreen = createSprite(200, 200);
endScreen.setAnimation("endscreen");
endScreen.visible = false;
endScreen.depth = 100;

//character scores
var score = 0;

//characters
var student1 = createSprite(50, 325);
student1.setAnimation("student1");
student1.scale = characterSize;

var student2 = createSprite(90, 325);
student2.setAnimation("student2");
student2.scale = characterSize;

var mentor = createSprite(420, 325);
mentor.setAnimation("mentor");
mentor.scale = characterSize;

var dementor = createSprite(420, randomNumber(25, 375));
dementor.setAnimation("dementor");
dementor.scale = characterSize;

//collectables
var lang_css = createSprite(randomNumber(420, 500), randomNumber(50, 350));
lang_css.setAnimation("css");
lang_css.scale = collectibleSize;

var lang_javascript = createSprite(randomNumber(420, 500), randomNumber(50, 350));
lang_javascript.setAnimation("javascript");
lang_javascript.scale = collectibleSize;

var lang_html = createSprite(randomNumber(420, 500), randomNumber(50, 350));
lang_html.setAnimation("html");
lang_html.scale = collectibleSize;

var lang_java = createSprite(randomNumber(420, 500), randomNumber(50, 350));
lang_java.setAnimation("java");
lang_java.scale = collectibleSize;

var lang_csharp = createSprite(randomNumber(420, 500), randomNumber(50, 350));
lang_csharp.setAnimation("csharp");
lang_csharp.scale = collectibleSize;

//hitboxes
student1.setCollider("rectangle", 0, 10, 100, 330);
student2.setCollider("rectangle", 0, 10, 100, 330);
mentor.setCollider("rectangle", 0, 10, 100, 330);
dementor.setCollider("rectangle", 0, -20, 100, 260);

//screen refresh (main)

dementor_movement();
collectible_movement();

function draw() {
  student1_movement();
  student2_movement();
  collectible_regen();
  dementor_regen();
  mentor_regen();
  dementor_touch();
  mentor_touch();
  collectible_touch();
  drawSprites();
  showScore();
  showTimer();
  show_endScreen();
}

function student1_movement() {
  if (keyDown("up")) {
  (student1.y) = student1.y - 5;
  }
  if (keyDown("down")) {
    student1.y = student1.y + 5;
  }
  if (keyDown("left")) {
    student1.x = student1.x - 5;
  }
  if (keyDown("right")) {
    student1.x = student1.x + 5;
  }
  student1.collide(bottomEdge);
  student1.collide(topEdge);
  student1.collide(leftEdge);
  student1.collide(rightEdge);
}

function student2_movement() {
  if (keyDown("w")) {
  student2.y = student2.y - 5;
}
  if (keyDown("s")) {
    student2.y = student2.y + 5;
  }
  if (keyDown("a")) {
  student2.x = student2.x - 5;
}
if (keyDown("d")) {
  student2.x = student2.x + 5;
}
  student2.collide(bottomEdge);
  student2.collide(topEdge);
  student2.collide(leftEdge);
  student2.collide(rightEdge);
}
//collectible movement from right to left
function collectible_movement(){
  lang_css.velocityX = randomNumber(-1, -10);
  lang_javascript.velocityX = randomNumber(-1, -10);
  lang_html.velocityX = randomNumber(-1, -10);
  lang_java.velocityX = randomNumber(-1, -10);
  lang_csharp.velocityX = randomNumber(-1, -10);
  mentor.velocityX = randomNumber(-0.01, -5);
}

//collectible spawn loop when reaching pre-specified x axis coordinate
function collectible_regen() {
  if (lang_css.x < -50) {
    lang_css.x = randomNumber(420, 600);
    lang_css.y = randomNumber(50, 350);
    lang_css.velocityX = randomNumber(-1, -10);
  }
  if (lang_html.x < -50) {
    lang_html.x = randomNumber(420, 600);
    lang_html.y = randomNumber(50, 350);
    lang_html.velocityX = randomNumber(-1, -10);
  }
  if (lang_java.x < -50) {
    lang_java.x = randomNumber(420, 600);
    lang_java.y = randomNumber(50, 350);
    lang_java.velocityX = randomNumber(-1, -10);
  }
  if (lang_javascript.x < -50) {
    lang_javascript.x = randomNumber(420, 600);
    lang_javascript.y = randomNumber(50, 350);
    lang_javascript.velocityX = randomNumber(-1, -10);
  }
  if (lang_csharp.x < -50) {
    lang_csharp.x = randomNumber(420, 600);
    lang_csharp.y = randomNumber(50, 350);
    lang_csharp.velocityX = randomNumber(-1, -10);
  }
}

//dementor movement
function dementor_movement() {
  dementor.velocityX = randomNumber(-1, -10);
}

//dementor spawn loop when reaching pre-specified x axis coordinate
function dementor_regen() {
 if (dementor.x < -50) {
    dementor.x = randomNumber(420, 600);
    dementor.y = randomNumber(50, 350);
    dementor.velocityX = randomNumber(-1, -10);
  } 
}
// mentor spawn loop when reaching pre-specified x axis coordinate
function mentor_regen() {
  if (mentor.x < -200) {
    mentor.x = randomNumber(420, 800);
    mentor.velocityX = randomNumber(-4, -6);
  }
}

// dementor touch decreases score
function dementor_touch() {
  if (dementor.isTouching(student1) || dementor.isTouching(student2)) {
    dementor.x = randomNumber(420, 600);
    dementor.y = randomNumber(50, 350);
    dementor.velocityX = randomNumber(-1, -10);
    score = score - 50;
  }
}

//mentor touch increases score
function mentor_touch() {
  if (mentor.isTouching(student1) || mentor.isTouching(student2)) {
    score = score + 1;
  }
}

//collectible touch increases score
function collectible_touch() {
  if (lang_css.isTouching(student1) || lang_css.isTouching(student2)) {
    lang_css.x = randomNumber(420, 600);
    lang_css.y = randomNumber(50, 350);
    lang_css.velocityX = randomNumber(-1, -10);
    score = score + 10; 
  }
  if (lang_html.isTouching(student1) || lang_html.isTouching(student2)) {
    lang_html.x = randomNumber(420, 600);
    lang_html.y = randomNumber(50, 350);
    lang_html.velocityX = randomNumber(-1, -10);
    score = score + 10; 
  }
  if (lang_javascript.isTouching(student1) || lang_javascript.isTouching(student2)) {
    lang_javascript.x = randomNumber(420, 600);
    lang_javascript.y = randomNumber(50, 350);
    lang_javascript.velocityX = randomNumber(-1, -10);
    score = score + 10; 
  }
  if (lang_java.isTouching(student1) || lang_java.isTouching(student2)) {
    lang_java.x = randomNumber(420, 600);
    lang_java.y = randomNumber(50, 350);
    lang_java.velocityX = randomNumber(-1, -10);
    score = score + 10; 
  }
  if (lang_csharp.isTouching(student1) || lang_csharp.isTouching(student2)) {
    lang_csharp.x = randomNumber(420, 600);
    lang_csharp.y = randomNumber(50, 350);
    lang_csharp.velocityX = randomNumber(-1, -10);
    score = score + 10; 
  }
}

//timer function
function showTimer() {
  if (timer > 0) {
    fill("white");
    textSize(30);
    text(Math.round(timer), 335, 50);
    timer = timer - 0.033;
    textSize(15);
    text("TIME LEFT", 310, 20);
  }
} 

function show_endScreen() {
  if (timer <= 0) {
   endScreen.visible = true;
   student1.velocityY = 0;
   student1.velocityX = 0;
   student1.x = -50;
   student1.y = -50;
   
   student2.velocityY = 0;
   student2.velocityX = 0;
   student2.x = -50;
   student2.y = -50;
   
   mentor.velocityY = 0;
   mentor.velocityX = 0;
   mentor.x = 450;
   mentor.y = 450;
   
   dementor.velocityY = 0;
   dementor.velocityX = 0;
   dementor.x = 450;
   dementor.y = 450;
   
   lang_css.velocityY = 0;
   lang_css.velocityX = 0;
   lang_css.x = 450;
   lang_css.y = 450;
   
   lang_html.velocityY = 0;
   lang_html.velocityX = 0;
   lang_html.x = 450;
   lang_html.y = 450;
   
   lang_javascript.velocityY = 0;
   lang_javascript.velocityX = 0;
   lang_javascript.x = 450;
   lang_javascript.y = 450;
   
   lang_java.velocityY = 0;
   lang_java.velocityX = 0;
   lang_java.x = 450;
   lang_java.y = 450;
   
   lang_csharp.velocityY = 0;
   lang_csharp.velocityX = 0;
   lang_csharp.x = 450;
   lang_csharp.y = 450;
   
  }
}

//score function
function showScore() {
  if (timer > 0) {
    fill("white");
    textSize(15);
    text("SCORE", 15, 20);
    textSize(30);
    text(score, 15, 50);
  } else {
    fill("white");
    textSize(40);
    text(score, 280, 373); 
  }
  if (score < 0) {
    score = 0;
  }
}

playSound("The_Seatbelts_-_Cats_on_Mars_(getmp3.pro).mp3");
