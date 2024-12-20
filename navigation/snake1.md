---
layout: page
title: Snake
permalink: /snake/
---

<style>
    body {}
    .wrap {
        margin-left: auto;
        margin-right: auto;
    }
    canvas {
        display: none;
        border-style: solid;
        border-width: 30px;
        border-color: rgb(3, 79, 27);
    }
    canvas:focus {
        outline: none;
    }
    #gameover p, #setting p, #menu p {
        font-size: 20px;
    }
    #gameover a, #setting a, #menu a {
        font-size: 30px;
        display: block;
    }
    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
    }
    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before {
        content: ">";
        margin-right: 10px;
    }
    #menu {
        display: block;
    }
    #gameover {
        display: none;
    }
    #setting {
        display: none;
    }
    #setting input {
        display: none;
    }
    #setting label {
        cursor: pointer;
    }
    #setting input:checked + label {
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: rgb(220,37,37); color: #000000">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color:rgb(220, 37, 37); color: #000000">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <canvas id="snake" class="wrap" width="600" height="600" tabindex="1"></canvas>
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color:rgb(220, 37, 37); color: #000000">space</span> to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="120" checked />
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75" />
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35" />
                <label for="speed3">Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked />
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0" />
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
(function () {
    const canvas = document.getElementById("snake");
    const ctx = canvas.getContext("2d");
    const SCREEN_MENU = -1, SCREEN_GAME_OVER = 1, SCREEN_SETTING = 2, SCREEN_SNAKE = 0;
    const BLOCK = 30;
    let SCREEN = SCREEN_MENU;
    let snake, snake_dir, snake_next_dir, snake_speed, food = { x: 0, y: 0 }, score, wall;

    const santaImage = new Image();
    santaImage.src = "https://github.com/user-attachments/assets/1be77c5c-202c-4155-a0f4-d973fb74a193"; // Replace with actual image URL
    const foodImage = new Image();
    foodImage.src = "https://github.com/user-attachments/assets/286593fc-4872-4d79-9ae8-c389d7d49ca2"; // Replace with actual image URL

    function mainLoop() {
        snake_dir = snake_next_dir;

        const _x = snake[0].x + (snake_dir === 1) - (snake_dir === 3);
        const _y = snake[0].y + (snake_dir === 2) - (snake_dir === 0);

        if (wall && (_x < 0 || _y < 0 || _x >= canvas.width / BLOCK || _y >= canvas.height / BLOCK)) {
            showScreen(SCREEN_GAME_OVER);
            return;
        }

        const head = { x: (_x + canvas.width / BLOCK) % (canvas.width / BLOCK), y: (_y + canvas.height / BLOCK) % (canvas.height / BLOCK) };
        if (snake.some(({ x, y }) => x === head.x && y === head.y)) {
            showScreen(SCREEN_GAME_OVER);
            return;
        }

        snake.unshift(head);
        if (head.x === food.x && head.y === food.y) {
            score++;
            document.getElementById("score_value").textContent = score;
            addFood();
        } else {
            snake.pop();
        }

        ctx.clearRect(0, 0, canvas.width, canvas.height);
        ctx.drawImage(santaImage, snake[0].x * BLOCK, snake[0].y * BLOCK, BLOCK, BLOCK);
        snake.slice(1).forEach(({ x, y }) => ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK));
        ctx.drawImage(foodImage, food.x * BLOCK, food.y * BLOCK, BLOCK, BLOCK);

        setTimeout(mainLoop, snake_speed);
    }

    function newGame() {
        snake = [{ x: 10, y: 10 }];
        snake_dir = 1;
        snake_next_dir = 1;
        snake_speed = parseInt(document.querySelector('input[name="speed"]:checked').value);
        wall = document.querySelector('input[name="wall"]:checked').value === "1";
        score = 0;
        document.getElementById("score_value").textContent = score;
        addFood();
        showScreen(SCREEN_SNAKE);
        canvas.focus();
        mainLoop();
    }

    function addFood() {
        do {
            food.x = Math.floor(Math.random() * canvas.width / BLOCK);
            food.y = Math.floor(Math.random() * canvas.height / BLOCK);
        } while (snake.some(({ x, y }) => x === food.x && y === food.y));
    }

    function showScreen(screen) {
        document.getElementById("menu").style.display = screen === SCREEN_MENU ? "block" : "none";
        document.getElementById("gameover").style.display = screen === SCREEN_GAME_OVER ? "block" : "none";
        document.getElementById("setting").style.display = screen === SCREEN_SETTING ? "block" : "none";
        canvas.style.display = screen === SCREEN_SNAKE ? "block" : "none";
        SCREEN = screen;
    }

    window.onload = function () {
        document.getElementById("new_game").onclick = newGame;
        document.getElementById("new_game1").onclick = newGame;
        document.getElementById("new_game2").onclick = newGame;
        window.onkeydown = (e) => {
            if ([37, 38, 39, 40].includes(e.keyCode)) {
                const nextDir = [2, 0, 3, 1][e.keyCode - 37];
                if (Math.abs(snake_dir - nextDir) !== 2) snake_next_dir = nextDir;
            }
        };
    };
})();
</script>
