let playerX, playerY, playerSize;
let obstacleSpeed, obstacleSize, obstacleCount;
let obstacles = [];
let score;

function setup() {
  createCanvas(400, 400);
  playerX = width / 2;
  playerY = height - 30;
  playerSize = 20;
  obstacleSpeed = 3;
  obstacleSize = 30;
  obstacleCount = 5;
  score = 0;

  for (let i = 0; i < obstacleCount; i++) {
    obstacles.push({
      x: random(width),
      y: random(height),
      direction: random() > 0.5 ? 1 : -1 // Define direção do obstáculo
    });
  }
}

function draw() {
  background(220);

  // Desenha o jogador
  fill(0, 0, 255);
  rect(playerX, playerY, playerSize, playerSize);

  // Movimentação dos obstáculos
  for (let i = 0; i < obstacles.length; i++) {
    obstacles[i].x += obstacleSpeed * obstacles[i].direction;

    if (obstacles[i].x > width + obstacleSize) {
      obstacles[i].x = -obstacleSize;
    } else if (obstacles[i].x < -obstacleSize) {
      obstacles[i].x = width + obstacleSize;
    }

    fill(255, 0, 0);
    rect(obstacles[i].x, obstacles[i].y, obstacleSize, obstacleSize);

    // Verifica colisão
    if (
      playerX < obstacles[i].x + obstacleSize &&
      playerX + playerSize > obstacles[i].x &&
      playerY < obstacles[i].y + obstacleSize &&
      playerY + playerSize > obstacles[i].y
    ) {
      // Colisão: volta ao início e reinicia a pontuação
      playerX = width / 2;
      score = 0;
    }
  }

  // Verifica se o jogador alcançou o outro lado
  if (playerY < 0) {
    playerY = height - 30;
    score++;
  }

  // Exibe a pontuação
  textSize(20);
  text(`Pontuação: ${score}`, 10, 30);
}

function keyPressed() {
  if (keyCode === LEFT_ARROW || key === 'a' || keyCode === 65) {
    playerX -= 10;
  } else if (keyCode === RIGHT_ARROW || key === 'd' || keyCode === 68) {
    playerX += 10;
  }
}

COMEÇAAAAAAAAAA

let balls = []; // Array para armazenar as bolinhas

function setup() {
  createCanvas(800, 400);
  for (let i = 0; i < 20; i++) {
    // Bolinhas que se movem da esquerda para a direita
    balls.push(new Ball(width * 0.25, random(height), 1));
    // Bolinhas que se movem da direita para a esquerda
    balls.push(new Ball(width * 0.75, random(height), -1));
  }
}

function draw() {
  background(220);
  for (let i = 0; i < balls.length; i++) {
    balls[i].move();
    balls[i].display();
  }
}

class Ball {
  constructor(x, y, direction) {
    this.x = x;
    this.y = y;
    this.diameter = 20;
    this.speed = 2;
    this.direction = direction;
  }

  move() {
    this.x += this.speed * this.direction;
    if (this.x > width || this.x < 0) {
      this.x = this.x > width ? 0 : width;
      this.y = random(height);
    }
  }

  display() {
    fill(255, 0, 0);
    ellipse(this.x, this.y, this.diameter);
  }
}

