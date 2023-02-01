 <!DOCTYPE html>
<html>
  <head>
    <style>
      table {
        border-collapse: collapse;
      }
      td {
        width: 50px;
        height: 50px;
        text-align: center;
        vertical-align: middle;
        border: 1px solid black;
      }
    </style>
  </head>
  <body>
    <table id="game">
      <tr>
        <td id="0"></td>
        <td id="1"></td>
        <td id="2"></td>
      </tr>
      <tr>
        <td id="3"></td>
        <td id="4"></td>
        <td id="5"></td>
      </tr>
      <tr>
        <td id="6"></td>
        <td id="7"></td>
        <td id="8"></td>
      </tr>
    </table>
    <script>
      const cells = document.querySelectorAll("td");
      let currentPlayer = "X";
      
      for (const cell of cells) {
        cell.addEventListener("click", handleClick);
      }
      
      function handleClick() {
        if (this.textContent === "") {
          this.textContent = currentPlayer;
          
          if (checkWin(currentPlayer)) {
            alert(`Jogador ${currentPlayer} venceu!`);
            reset();
          } else if (checkDraw()) {
            alert("Empate!");
            reset();
          } else {
            switchPlayer();
          }
        }
      }
      
      function checkWin(player) {
        const winCombinations = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6]
        ];
        
        for (const combination of winCombinations) {
          const [a, b, c] = combination;
          
          if (cells[a].textContent === player &&
              cells[b].textContent === player &&
              cells[c].textContent === player) {
            return true;
          }
        }
        
        return false;
      }
      
      function checkDraw() {
        for (const cell of cells) {
          if (cell.textContent === "") {
            return false;
          }
        }
        
        return true;
      }
      
      function switchPlayer() {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
      }
      
      function reset() {
        for (const cell of cells) {
          cell.textContent = "";
        }
        
        currentPlayer = "X";
      }
    </script>
  </body>
</html>
