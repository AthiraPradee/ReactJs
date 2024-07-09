# ReactJs
Tic Tac Toe Game in Reactjs
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
function Board(props) {
  return (
    <div className="board">
      {props.squares.map((value, index) => (
        <Square
          key={index}
          value={value}
          onClick={() => props.onClick(index)}
        />
      ))}
    </div>
  );
}
function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [stepNumber, setStepNumber] = useState(0);
  const [xIsNext, setXIsNext] = useState(true);

  const handleClick = (i) => {
    const currentHistory = history.slice(0, stepNumber + 1);
    if (calculateWinner(currentSquares) || currentSquares[i]) {
      return;
    }
   
  const jumpTo = (step) => {
    setStepNumber(step);
    setXIsNext(step % 2 === 0);
  };

  const currentSquares = history[stepNumber];
  const winner = calculateWinner(currentSquares);
  const status = winner
    ? `Winner: ${winner}`
    : `Next player: ${xIsNext ? 'X' : 'O'}`;

  return (
    <div className="game">
      <div className="game-board">
        <Board squares={currentSquares} onClick={handleClick} />
      </div>
      <div className="game-info">
        <div>{status}</div>
        <ol>
          {history.map((step, move) => (
            <li key={move}>
              <button onClick={() => jumpTo(move)}>
                {move ? `Go to move ${move}` : 'Go to game start'}
              </button>
            </li>
          ))}
        </ol>
      </div>
    </div>
  );
}
function calculateWinner(squares) {
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
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
