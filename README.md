# ReactJs
Tic Tac Toe Game in Reactjs
import React, { useState } from 'react';
import './App.css';

const initialBoard = Array(9).fill(null);

const App = () => {
  const [board, setBoard] = useState(initialBoard);
  const [xIsNext, setXIsNext] = useState(true);

  const handleClick = (index) => {
    if (calculateWinner(board) || board[index]) {
      return;
    }
    const newBoard = [...board];
    newBoard[index] = xIsNext ? 'X' : 'O';
    setBoard(newBoard);
    setXIsNext(!xIsNext);
  };

  const renderSquare = (index) => {
    return (
      <button className="square" onClick={() => handleClick(index)}>
        {board[index]}
      </button>
    );
  };

  const winner = calculateWinner(board);
  let status;
  if (winner) {
    status = `Winner: ${winner}`;
  } else {
    status = `Next player: ${xIsNext ? 'X' : 'O'}`;
  }

  return (
    <div className="game">
      <div className="board">
        {board.map((square, index) => (
          <div key={index} className="square">
            {renderSquare(index)}
          </div>
        ))}
      </div>
      <div className="game-info">{status}</div>
    </div>
  );
};

const calculateWinner = (squares) => {
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
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
};

export default App;
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Arial, sans-serif;
}

.board {
  display: flex;
  flex-wrap: wrap;
  width: 180px;
  margin-bottom: 20px;
}

.square {
  width: 60px;
  height: 60px;
  font-size: 24px;
  font-weight: bold;
  border: 1px solid #999;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.game-info {
  font-size: 18px;
  font-weight: bold;
}
