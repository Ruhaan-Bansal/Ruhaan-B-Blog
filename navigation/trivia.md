---
layout: base
title: Two-Player Q&A Game
permalink: /qna-game/
description: A fun two-player question and answer game.
hide: false
---

## Two-Player Question & Answer Game

### How to Play
1. **Setup**: Each player takes turns answering a question.
2. **Taking Turns**:
   - Player 1 asks a question from the list.
   - Player 2 types their answer.
   - If the answer is correct, Player 2 earns 1 point.
   - If incorrect, Player 1 provides the correct answer.
3. **Switch Roles**: Player 2 now asks a question for Player 1.
4. **Repeat** until all questions have been asked.
5. **Scoring**: The player with the most points at the end wins!

### Game Interface
**Question:**
<p id="question-text">Question will appear here</p>

**Enter your answer:**
<input type="text" id="answer" placeholder="Type your answer here">

<button id="submit-btn" onclick="checkAnswer()">Submit Answer</button>

### Scoreboard
<table>
  <tr><th>Player</th><th>Score</th></tr>
  <tr><td>Player 1</td><td id="player1-score">0</td></tr>
  <tr><td>Player 2</td><td id="player2-score">0</td></tr>
</table>

<style>
/* General Styling */
body {
    font-family: 'Arial', sans-serif;
    background-color: #f7f7f7;
    text-align: center;
    margin: 0;
    padding: 0;
}

/* Title and Instructions */
h1 {
    color: #333;
    font-size: 2.5em;
    margin-top: 20px;
}

h2 {
    color: #007BFF;  /* Set rules color to blue */
    font-size: 1.2em;
    margin-top: 10px;
}

/* Question Styling */
#question-text {
    font-size: 1.5em;
    color: #333;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 10px;
    margin-top: 30px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Input Box Styling */
input[type="text"] {
    width: 70%;
    padding: 10px;
    margin-top: 20px;
    font-size: 1em;
    border: 2px solid #ddd;
    border-radius: 5px;
    transition: 0.3s ease-in-out;
}

input[type="text"]:focus {
    border-color: #4CAF50;
    outline: none;
}

/* Button Styling */
#submit-btn {
    background-color: white;
    color: #007BFF;
    font-size: 1.2em;
    padding: 12px 24px;
    border: 2px solid #007BFF;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 20px;
    transition: 0.3s;
}

#submit-btn:hover {
    background-color: #007BFF;
    color: white;
    transform: scale(1.1);
}

#submit-btn:active {
    background-color: #0056b3;
    border-color: #0056b3;
}

/* Table Styling */
table {
    margin-top: 40px;
    margin-left: auto;
    margin-right: auto;
    font-size: 1.2em;
    background-color: #ffffff;
    border-collapse: collapse;
    width: 50%;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

table th, table td {
    padding: 10px;
    text-align: center;
  
