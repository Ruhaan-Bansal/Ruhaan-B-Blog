---
layout: Snake
title: Snake Game
search_exclude: true
permalink: /snake
---

<style>
    body {
        background-color: black;
    }
    .wrap {
        margin-left: auto;
        margin-right: auto;
    }

    canvas {
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
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
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #FFFFFF; color: #000000">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color: #FFFFFF; color: #000000">space</span> to go back to playing</p>
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
    const BLOCK = 10;
    let snake = [];
    let snake_dir;
    let snake_next_dir;
    let food = { x: 0, y: 0 };
    let score = 0;
    let snake_speed = 150;

    const drawCircle = (x, y, color) => {
        ctx.fillStyle = color;
        ctx.beginPath();
        ctx.arc(x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2, BLOCK / 2, 0, Math.PI * 2);
        ctx.fill();
    };

    const drawTriangle = (x, y, color) => {
        ctx.fillStyle = color;
        ctx.beginPath();
        ctx.moveTo(x * BLOCK + BLOCK / 2, y * BLOCK);
        ctx.lineTo(x * BLOCK, y * BLOCK + BLOCK);
        ctx.lineTo(x * BLOCK + BLOCK, y * BLOCK + BLOCK);
        ctx.closePath();
        ctx.fill();
    };

    const mainLoop = () => {
        let _x = snake[0].x;
        let _y = snake[0].y;
        snake_dir = snake_next_dir;

        switch (snake_dir) {
            case 0: _y--; break;
            case 1: _x++; break;
            case 2: _y++; break;
            case 3: _x--; break;
        }

        snake.pop();
        snake.unshift({ x: _x, y: _y });

        if (snake[0].x < 0 || snake[0].x >= canvas.width / BLOCK || snake[0].y < 0 || snake[0].y >= canvas.height / BLOCK) {
            alert("Game Over!");
            return;
        }

        if (snake.some((part, index) => index !== 0 && part.x === _x && part.y === _y)) {
            alert("Game Over!");
            return;
        }

        if (snake[0].x === food.x && snake[0].y === food.y) {
            snake.push({ ...snake[snake.length - 1] });
            score++;
            placeFood();
        }

        ctx.clearRect(0, 0, canvas.width, canvas.height);

        snake.forEach(part => drawCircle(part.x, part.y, "white"));
        drawTriangle(food.x, food.y, "green");

        setTimeout(mainLoop, snake_speed);
    };

    const placeFood = () => {
        food.x = Math.floor(Math.random() * (canvas.width / BLOCK));
        food.y = Math.floor(Math.random() * (canvas.height / BLOCK));
    };

    const newGame = () => {
        snake = [{ x: 5, y: 5 }];
        snake_dir = 1;
        snake_next_dir = 1;
        score = 0;
        placeFood();
        mainLoop();
    };

    document.addEventListener("keydown", (e) => {
        switch (e.key) {
            case "ArrowUp": if (snake_dir !== 2) snake_next_dir = 0; break;
            case "ArrowRight": if (snake_dir !== 3) snake_next_dir = 1; break;
            case "ArrowDown": if (snake_dir !== 0) snake_next_dir = 2; break;
            case "ArrowLeft": if (snake_dir !== 1) snake_next_dir = 3; break;
        }
    });

    newGame();
})();
</script>
