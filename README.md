let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover(100, 100);
}

function draw() {
  background(51);
  mover.applyForce(createVector(0, 0.2));
  if (mouseIsPressed) mover.applyForce(createVector(0.05, 0));
  mover.update();
  mover.checkEdges();
  mover.display();
}

class Mover {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }
  applyForce(force) {
    this.acceleration.add(p5.Vector.div(force, this.mass));
  }
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }
  display() {
    fill(200, 100, 100);
    noStroke();
    ellipse(this.position.x, this.position.y, this.mass * 16, this.mass * 16);
  }
  checkEdges() {
    if (this.position.y > height) { this.position.y = height; this.velocity.y *= -1; }
    if (this.position.x > width) { this.position.x = width; this.velocity.x *= -1; }
    if (this.position.x < 0) { this.position.x = 0; this.velocity.x *= -1; }
  }
}
