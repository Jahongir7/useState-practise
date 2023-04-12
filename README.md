import React, { useState } from "react";

function Increment() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState("");

  const addTodo = (todo) => {
    setTodos([...todos, todo]);
  };

  const deleteTodo = (index) => {
    const newTodos = [...todos];
    newTodos.splice(index, 1);
    setTodos(newTodos);
  };

  const completeTodo = (index) => {
    const newTodos = [...todos];
    newTodos[index].isCompleted = true;
    setTodos(newTodos);
  };

  return (
    <div>
      <form
        onSubmit={(e) => {
          e.preventDefault();
          addTodo({ text: input, isCompleted: false });
          setInput("");
        }}
      >
        <input value={input} onChange={(e) => setInput(e.target.value)} />
        <button type="submit">Add Todo</button>
      </form>
      {todos.map((todo, index) => (
        <div key={index}>
          <div
            style={{ textDecoration: todo.isCompleted ? "line-through" : "" }}
          >
            {todo.text}
          </div>
          <button onClick={() => deleteTodo(index)}>Delete</button>
          <button onClick={() => completeTodo(index)}>Complete</button>
        </div>
      ))}
    </div>
  );
}

export default Increment;









import { useState } from "react";

function ChangeChildPosition() {
  const [position, setPosition] = useState("50%");
  const [positionY, setPositionY] = useState("50%");
  const minPosition = 0;
  const maxPosition = 95;

  function handlePositionChange(event) {
    const newPosition = `${event.target.value}%`;
    setPosition(newPosition);
  }

  return (
    <div
      style={{
        position: "relative",
        width: "400px",
        height: "400px",
        border: "1px solid black",
        boxSizing: "border-box",
      }}
    >
      <div style={{ position: "absolute", left: position, top: positionY }}>
        M
      </div>
      <input
        type="range"
        min={minPosition}
        max={maxPosition}
        value={parseInt(position)}
        onChange={handlePositionChange}
      />
      <input
        type="range"
        min={minPosition}
        max={maxPosition}
        value={parseInt(positionY)}
        onChange={(e) => setPositionY(`${e.target.value}%`)}
      />
    </div>
  );
}
export default ChangeChildPosition;









import { useEffect, useState } from "react";

const CatFact = () => {
  const [data, setData] = useState("");

  const handleClick = () => {
    fetch("https://catfact.ninja/fact")
      .then((res) => res.json())
      .then((data) => setData(data.fact))
      .catch((err) => console.log(err));
  };

  useEffect(() => {
    handleClick();
  }, []);

  return (
    <div>
      <button onClick={handleClick}>bosish</button>
      <p>{data}</p>
    </div>
  );
};

export default CatFact;
