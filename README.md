- 👋 Hi, I’m @Datenflix007
- 👀 I’m interested WebDev and Java
- 🌱 I’m currently go on university
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
<!---
Datenflix007/Datenflix007 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->



[![Hey](https://img.youtube.com/vi/V-MX379oGqE/0.jpg)](https://www.youtube.com/watch?v=V-MX379oGqE&autoplay=1)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body { 
            margin: 0; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            height: 100vh; 
            background-color: #000; 
        }
        canvas {
            border: 1px solid white;
            background-color: #111;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        const scale = 20;
        const rows = canvas.height / scale;
        const columns = canvas.width / scale;

        let snake;
        let food;

        (function setup() {
            snake = new Snake();
            food = new Food();
            window.setInterval(game, 100);
        })();

        function game() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            snake.update();
            snake.draw();
            food.draw();

            if (snake.eat(food)) {
                food = new Food();
            }

            if (snake.collide()) {
                window.location.reload();
            }
        }

        function Snake() {
            this.snakeArray = [{x: 5, y: 5}];
            this.direction = "right";

            this.update = function() {
                let head = {x: this.snakeArray[0].x, y: this.snakeArray[0].y};

                if (this.direction === "left") head.x -= 1;
                if (this.direction === "right") head.x += 1;
                if (this.direction === "up") head.y -= 1;
                if (this.direction === "down") head.y += 1;

                this.snakeArray.unshift(head);
                this.snakeArray.pop();
            };

            this.draw = function() {
                ctx.fillStyle = "green";
                for (let i = 0; i < this.snakeArray.length; i++) {
                    ctx.fillRect(this.snakeArray[i].x * scale, this.snakeArray[i].y * scale, scale, scale);
                }
            };

            this.changeDirection = function(event) {
                if (event.keyCode === 37 && this.direction !== "right") this.direction = "left";
                if (event.keyCode === 38 && this.direction !== "down") this.direction = "up";
                if (event.keyCode === 39 && this.direction !== "left") this.direction = "right";
                if (event.keyCode === 40 && this.direction !== "up") this.direction = "down";
            };

            this.eat = function(food) {
                if (this.snakeArray[0].x === food.x && this.snakeArray[0].y === food.y) {
                    this.snakeArray.push({x: food.x, y: food.y});
                    return true;
                }
                return false;
            };

            this.collide = function() {
                for (let i = 1; i < this.snakeArray.length; i++) {
                    if (this.snakeArray[i].x === this.snakeArray[0].x && this.snakeArray[i].y === this.snakeArray[0].y) {
                        return true;
                    }
                }
                if (this.snakeArray[0].x < 0 || this.snakeArray[0].x >= columns || this.snakeArray[0].y < 0 || this.snakeArray[0].y >= rows) {
                    return true;
                }
                return false;
            };
        }

        function Food() {
            this.x = Math.floor(Math.random() * columns);
            this.y = Math.floor(Math.random() * rows);

            this.draw = function() {
                ctx.fillStyle = "red";
                ctx.fillRect(this.x * scale, this.y * scale, scale, scale);
            };
        }

        window.addEventListener("keydown", function(event) {
            snake.changeDirection(event);
        });
    </script>
</body>
</html>
