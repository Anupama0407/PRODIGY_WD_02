<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            justify-content: center;
            margin-top: 20px;
        }
        .cell {
            width: 100px;
            height: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
            background-color: #eee2e1;
            border: 2px solid #890808;
            cursor: pointer;
        }
        .cell.taken {
            cursor: not-allowed;
        }
        #status {
            margin-top: 20px;
            font-size: 1.2em;
        }
        button {
            margin-top: 15px;
            padding: 10px;
            font-size: 1em;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Tic-Tac-Toe</h1>
    <div id="status">Player X's turn</div>
    <div class="board" id="board"></div>
    <button onclick="resetGame()">Restart</button>

    <script>
        const board = document.getElementById("board");
        let cells = [];
        let currentPlayer = "X";
        let gameActive = true;
        const status = document.getElementById("status");
        const winningCombinations = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ];
        
        function createBoard() {
            board.innerHTML = "";
            cells = [];
            for (let i = 0; i < 9; i++) {
                let cell = document.createElement("div");
                cell.classList.add("cell");
                cell.dataset.index = i;
                cell.addEventListener("click", handleMove);
                board.appendChild(cell);
                cells.push(cell);
            }
        }
        
        function handleMove(event) {
            if (!gameActive) return;
            const cell = event.target;
            if (cell.textContent !== "") return;
            
            cell.textContent = currentPlayer;
            cell.classList.add("taken");
            
            if (checkWinner()) {
                status.textContent = `Player ${currentPlayer} wins!`;
                gameActive = false;
                return;
            }
            
            if ([...cells].every(cell => cell.textContent !== "")) {
                status.textContent = "It's a draw!";
                gameActive = false;
                return;
            }
            
            currentPlayer = currentPlayer === "X" ? "O" : "X";
            status.textContent = `Player ${currentPlayer}'s turn`;
        }
        
        function checkWinner() {
            return winningCombinations.some(combination => {
                const [a, b, c] = combination;
                return cells[a].textContent !== "" &&
                       cells[a].textContent === cells[b].textContent &&
                       cells[a].textContent === cells[c].textContent;
            });
        }
        
        function resetGame() {
            gameActive = true;
            currentPlayer = "X";
            status.textContent = "Player X's turn";
            createBoard();
        }
        
        createBoard();
    </script>
</body>
</html>
