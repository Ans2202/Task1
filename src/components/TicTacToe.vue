<template>
    <div class="game-container">
      <h1 class="game-title">Tic Tac Toe</h1>
      <div class="board">
        <div v-for="(cell, index) in cells" :key="index" class="cell" @click="makeMove(index)">
          {{ cell }}
        </div>
      </div>
      <div class="status">{{ status }}</div>
      <button class="reset-button" @click="resetGame">Reset Game</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cells: Array(9).fill(null),
        xIsNext: true,
        status: 'Next player: X',
      };
    },
    computed: {
      winner() {
        const lines = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6],
        ];
        for (const [a, b, c] of lines) {
          if (this.cells[a] && this.cells[a] === this.cells[b] && this.cells[a] === this.cells[c]) {
            return this.cells[a];
          }
        }
        return null;
      },
      isDraw() {
        return !this.winner && this.cells.every(cell => cell);
      }
    },
    watch: {
      winner(newWinner) {
        if (newWinner) {
          this.status = `Winner: ${newWinner}`;
        } else if (this.isDraw) {
          this.status = 'It\'s a draw!';
        } else {
          this.status = `Next player: ${this.xIsNext ? 'X' : 'O'}`;
        }
      }
    },
    methods: {
      makeMove(index) {
        if (this.cells[index] || this.winner) return;
  
        this.$set(this.cells, index, this.xIsNext ? 'X' : 'O');
        this.xIsNext = !this.xIsNext;
      },
      
      resetGame() {
        this.cells = Array(9).fill(null);
        this.xIsNext = true;
        this.status = 'Next player: X';
      },
    },
  };
  </script>
  
  <style scoped>
  .game-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 50px;
    font-family: 'Arial', sans-serif;
    background-color: #e0f7fa; /* Light blue background */
    color: #01579b; /* Dark blue text */
    height: 100vh;
    width: 100vw;
    overflow: hidden;
  }
  
  .game-title {
    font-size: 36px;
    font-weight: bold;
    color: #0277bd; /* Medium blue title */
    margin-bottom: 20px;
  }
  
  .board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    gap: 5px;
    background-color: #b3e5fc; /* Light blue board background */
    border: 3px solid #039be5; /* Blue border */
    border-radius: 10px;
  }
  
  .cell {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 36px;
    font-weight: bold;
    color: #0277bd; /* Medium blue cell text */
    border: 2px solid #81d4fa; /* Light blue cell border */
    background-color: #e1f5fe; /* Very light blue cell background */
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
    border-radius: 8px;
  }
  
  .cell:hover {
    background-color: #b3e5fc; /* Light blue hover effect */
    color: #01579b; /* Dark blue text on hover */
  }
  
  .status {
    margin-top: 20px;
    font-size: 24px;
    font-weight: bold;
  }
  
  .reset-button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 16px;
    font-weight: bold;
    color: #fff;
    background-color: #0288d1; /* Darker blue button background */
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .reset-button:hover {
    background-color: #01579b; /* Even darker blue on hover */
  }
  
  .reset-button:focus {
    outline: none;
  }
  </style>
  