const width = 21;
const height = 21;

const game = document.getElementById("game");
const scoreDisplay = document.getElementById("score");
let score = 0;
let cells = [];
let map = [];
let pacmanPos = { x: 1, y: 1 };
let enemyPos = { x: width - 2, y: height - 2 }; // 初期位置：右下

function generateMaze() {
  map = Array.from({ length: height }, () => Array(width).fill("#"));

  function carve(x, y) {
    const dirs = [
      [0, -2], [0, 2], [-2, 0], [2, 0]
    ].sort(() => Math.random() - 0.5);

    for (const [dx, dy] of dirs) {
      const nx = x + dx;
      const ny = y + dy;
      if (nx > 0 && ny > 0 && nx < width - 1 && ny < height - 1 && map[ny][nx] === "#") {
        map[ny][nx] = ".";
        map[y + dy / 2][x + dx / 2] = ".";
        carve(nx, ny);
      }
    }
  }

  map[1][1] = ".";
  carve(1, 1);

  map[height - 2][width - 2] = ".";
  pacmanPos = { x: 1, y: 1 };
  enemyPos = { x: width - 2, y: height - 2 };
}

function drawMap() {
  game.innerHTML = "";
  cells = [];
  game.style.gridTemplateColumns = `repeat(${width}, 20px)`;
  game.style.gridTemplateRows = `repeat(${height}, 20px)`;

  for (let y = 0; y < height; y++) {
    for (let x = 0; x < width; x++) {
      const cell = document.createElement("div");
      cell.classList.add("cell");

      if (map[y][x] === "#") {
        cell.classList.add("wall");
      } else {
        const dot = document.createElement("div");
        dot.classList.add("dot");
        cell.appendChild(dot);
      }

      cells.push(cell);
      game.appendChild(cell);
    }
  }
  updateCharacters();
}

function updateCharacters() {
  cells.forEach(cell => {
    cell.classList.remove("pacman");
    cell.classList.remove("enemy");
  });

  // パックマン
  const pacIndex = pacmanPos.y * width + pacmanPos.x;
  const pacCell = cells[pacIndex];
  pacCell.classList.add("pacman");

  const dot = pacCell.querySelector(".dot");
  if (dot) {
    dot.remove();
    score += 10;
    scoreDisplay.textContent = `スコア: ${score}`;
  }

  // 敵
  const enemyIndex = enemyPos.y * width + enemyPos.x;
  cells[enemyIndex].classList.add("enemy");

  // 当たり判定
  if (pacmanPos.x === enemyPos.x && pacmanPos.y === enemyPos.y) {
    alert("ゲームオーバー！");
    location.reload();
  }
}

function move(dx, dy) {
  const newX = pacmanPos.x + dx;
  const newY = pacmanPos.y + dy;
  if (map[newY][newX] !== "#") {
    pacmanPos.x = newX;
    pacmanPos.y = newY;
    updateCharacters();
  }
}

document.addEventListener("keydown", e => {
  if (e.key === "ArrowUp") move(0, -1);
  if (e.key === "ArrowDown") move(0, 1);
  if (e.key === "ArrowLeft") move(-1, 0);
  if (e.key === "ArrowRight") move(1, 0);
});

// 敵のランダム移動
function moveEnemy() {
  const dirs = [
    [0, -1],
    [0, 1],
    [-1, 0],
    [1, 0]
  ];

  const possibleMoves = dirs.filter(([dx, dy]) => {
    const nx = enemyPos.x + dx;
    const ny = enemyPos.y + dy;
    return map[ny][nx] !== "#";
  });

  if (possibleMoves.length > 0) {
    const [dx, dy] = possibleMoves[Math.floor(Math.random() * possibleMoves.length)];
    enemyPos.x += dx;
    enemyPos.y += dy;
    updateCharacters();
  }
}

// 毎秒敵を移動
setInterval(moveEnemy, 500);

// 初期化
generateMaze();
drawMap();
