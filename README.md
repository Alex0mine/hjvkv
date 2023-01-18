<!DOCTYPE html>
<html>
<head>
    <title>Tic-Tac-Toe</title>
    <style>
        /* Styling for the game board */
        .board {
            display: flex;
            flex-wrap: wrap;
            width: 300px;
            height: 300px;
            border: 1px solid black;
            margin: 0 auto;
        }
        /* Styling for each cell on the game board */
        .cell {
            width: 100px;
            height: 100px;
            text-align: center;
            font-size: 50px;
            line-height: 100px;
        }
        /* Styling for the result message */
        .result {
            text-align: center;
            font-size: 20px;
            margin-top: 20px;
        }
        /* Styling for the new game button */
        .new-game-btn {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 18px;
            border: 1px solid black;
            border-radius: 5px;
            text-align: center;
            cursor: pointer;
        }
    </style>
    </head>
<body>
    <div class="board">
        <div class="cell" id="0-0"></div>
        <div class="cell" id="0-1"></div>
        <div class="cell" id="0-2"></div>
        <div class="cell" id="1-0"></div>
        <div class="cell" id="1-1"></div>
        <div class="cell" id="1-2"></div>
        <div class="cell" id="2-0"></div>
        <div class="cell" id="2-1"></div>
        <div class="cell" id="2-2"></div>
    </div>
    <script>
    // Game state
    let board = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
    ];
    let currentPlayer = "X";
    let winner = null;
    let resultMessage = document.querySelector('.result');
    let newGameButton = document.querySelector('.new-game-btn');

    // Function to handle a move
    function handleMove(row, col) {
        if (winner) {
            return;
        }
        if (board[row][col]) {
            console.log("That cell is already occupied");
            return;
        }
        board[row][col] = currentPlayer;
        checkForWinner();
        if (!winner) {
            currentPlayer = currentPlayer === "X" ? "O" : "X";
        }
    }
// Function to check for a winner
    function checkForWinner() {
        const winningCombinations = [
            [[0, 0], [0, 1], [0, 2]],
            [[1, 0], [1, 1], [1, 2]],
            [[2, 0], [2, 1], [2, 2]],
            [[0, 0], [1, 0], [2, 0]],
            [[0, 1], [1, 1], [2, 1]],
            [[0, 2], [1, 2], [2, 2]],
            [[0, 0], [1, 1], [2, 2]],
            [[0, 2], [1, 1], [2, 0]]
        ];

        for (let i = 0; i < winningCombinations.length; i++) {
            const [a, b, c] = winningCombinations[i];
            if (board[a[0]][a[1]] && board[a[0]][a[1]] === board[b[0]][b[1]] && board[a[0]][a[1]] === board[c[0]][c[1]]) {
                winner = board[a[0]][a[1]];
                resultMessage.textContent = winner + " won!";
                break;
            }
        }
        if (!winner && board.flat().filter(cell => cell === null).length === 0) {
            resultMessage.textContent = "It's a tie!";
        }
    }

    // Get the cells on the game board
    const cells = document.querySelectorAll('.cell');
    // Attach a click event listener to each cell
    cells.forEach(cell => {
        cell.addEventListener('click', event => {
            // Get the row and column of the clicked cell
            const [row, col] = event.target.id.split('-').map(Number);
            // Pass the row and column to the handleMove function
            handleMove(row, col);
            // Update the cell's text with the current player's symbol
            event.target.textContent = currentPlayer;
        });
    });
    
    newGameButton.addEventListener('click', () => {
    board = [
      [null, null, null],
      [null, null, null],
      [null, null, null]
    ];
    currentPlayer = "X";
    winner = null;
    resultMessage.textContent = "";
    cells.forEach(cell => (cell.textContent = ""));
  });
</script>
</body>
</html>
