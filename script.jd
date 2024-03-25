const player = {
  x: 50,
  y: 50,
  speed: 5,
  direction: 'down'
};

const enemies = [];

function movePlayer(direction) {
  player.direction = direction;
  switch(direction) {
    case 'up':
      player.y -= player.speed;
      break;
    case 'down':
      player.y += player.speed;
      break;
    case 'left':
      player.x -= player.speed;
      break;
    case 'right':
      player.x += player.speed;
      break;
  }
}

function spawnEnemy() {
  const enemy = {
    x: Math.random() * 700,
    y: Math.random() * 500
  };
  enemies.push(enemy);
}

function render() {
  const playerElement = document.createElement('div');
  playerElement.className = 'player';
  playerElement.style.left = `${player.x}px`;
  playerElement.style.top = `${player.y}px`;
  playerElement.style.transform = `rotate(${getRotationAngle(player.direction)}deg)`;
  document.getElementById('game-container').appendChild(playerElement);

  enemies.forEach(enemy => {
    const enemyElement = document.createElement('div');
    enemyElement.className = 'enemy';
    enemyElement.style.left = `${enemy.x}px`;
    enemyElement.style.top = `${enemy.y}px`;
    document.getElementById('game-container').appendChild(enemyElement);
  });
}

function getRotationAngle(direction) {
  switch(direction) {
    case 'up':
      return 0;
    case 'down':
      return 180;
    case 'left':
      return -90;
    case 'right':
      return 90;
  }
}

document.addEventListener('keydown', function(event) {
  switch(event.key) {
    case 'ArrowUp':
      movePlayer('up');
      break;
    case 'ArrowDown':
      movePlayer('down');
      break;
    case 'ArrowLeft':
      movePlayer('left');
      break;
    case 'ArrowRight':
      movePlayer('right');
      break;
  }
});

document.addEventListener('touchstart', handleTouchStart, false);
document.addEventListener('touchmove', handleTouchMove, false);

let xDown = null;
let yDown = null;

function handleTouchStart(event) {
  const firstTouch = event.touches[0];
  xDown = firstTouch.clientX;
  yDown = firstTouch.clientY;
}

function handleTouchMove(event) {
  if (!xDown || !yDown) {
    return;
  }

  const xUp = event.touches[0].clientX;
  const yUp = event.touches[0].clientY;

  const xDiff = xDown - xUp;
  const yDiff = yDown - yUp;

  if (Math.abs(xDiff) > Math.abs(yDiff)) { // Horizontal swipe
    if (xDiff > 0) {
      movePlayer('left');
    } else {
      movePlayer('right');
    }
  } else { // Vertical swipe
    if (yDiff > 0) {
      movePlayer('up');
    } else {
      movePlayer('down');
    }
  }

  // Reset values
  xDown = null;
  yDown = null;
}

function updateEnemies() {
  enemies.forEach(enemy => {
    const dx = player.x - enemy.x;
    const dy = player.y - enemy.y;
    const distance = Math.sqrt(dx * dx + dy * dy);

    if (distance < 50) {
      // Player is close to enemy
      // Implement enemy behavior here (e.g., attacking player)
    }

    // Move enemy towards player
    const angle = Math.atan2(dy, dx);
    enemy.x += Math.cos(angle) * player.speed * 0.5;
    enemy.y += Math.sin(angle) * player.speed * 0.5;
  });
}

function gameLoop() {
  document.getElementById('game-container').innerHTML = '';
  render();
  updateEnemies();
  requestAnimationFrame(gameLoop);
}

setInterval(spawnEnemy, 3000); // Spawn a new enemy every 3 seconds
gameLoop();
