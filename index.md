<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Idea Randomizer</title>

<style>
  /* Load Aesop Regular font */
  @font-face {
    font-family: 'AesopRegular';
    src: url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.woff2') format('woff2'),
         url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.woff') format('woff'),
         url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
  }

  :root {
    --bg-color: #f8f6f3;
    --text-color: #2e2c29;
    --accent-color: #c8c2b3;
    --button-bg: #dcd6cc;
    --button-hover: #c2b9ad;
    --border-color: #b5afa4;
  }

  body {
    font-family: 'AesopRegular', serif;
    background-color: var(--bg-color);
    color: var(--text-color);
    margin: 0;
    padding: 0;
  }

  .container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
  }

  h1 {
    text-align: center;
    font-size: 2rem;
    margin-bottom: 0.5em;
  }

  p {
    line-height: 1.5;
  }

  input, button {
    font-family: inherit;
    padding: 10px;
    margin: 5px 0;
    width: 100%;
    border: 1px solid var(--border-color);
    border-radius: 5px;
    box-sizing: border-box;
  }

  button {
    background-color: var(--button-bg);
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: var(--button-hover);
  }

  .ideas-list {
    margin-top: 1em;
    padding: 0;
    list-style: none;
  }

  .ideas-list li {
    background: #fff;
    border: 1px solid var(--border-color);
    padding: 8px;
    margin-bottom: 5px;
    border-radius: 5px;
  }

  .result-box {
    background: #fff;
    padding: 15px;
    border: 1px solid var(--border-color);
    border-radius: 5px;
    margin-top: 1em;
    font-size: 1.2em;
    text-align: center;
  }

  .facts {
    background-color: var(--accent-color);
    padding: 15px;
    border-radius: 5px;
    margin-top: 2em;
  }

  @media (max-width: 600px) {
    h1 {
      font-size: 1.5rem;
    }
    .result-box {
      font-size: 1em;
    }
  }
</style>
</head>
<body>
  <div class="container">
    <h1>Idea Randomizer</h1>
    <p>Submit ideas for things to do, then randomize and share them. Store them, add to your calendar, or invite friends!</p>
    <input type="text" id="ideaInput" placeholder="Enter your idea" />
    <button onclick="addIdea()">Add Idea</button>
    <button onclick="randomizeIdea()">Randomize</button>
    <button onclick="clearIdeas()">Clear Ideas</button>
    <ul class="ideas-list" id="ideasList"></ul>

    <div class="result-box" id="resultBox">Your random idea will appear here.</div>
    <button onclick="addToCalendar()">Add to Calendar</button>
    <button onclick="shareIdea()">Share</button>

    <div class="facts">
      <h2>Did you know?</h2>
      <ul>
        <li>The average person spends over 3 hours a day on their phone.</li>
        <li>We spend roughly 90% of our time indoors.</li>
        <li>Watching TV takes up about 2.5 hours of the average day.</li>
        <li>Breaking routine with new activities boosts creativity and happiness.</li>
      </ul>
    </div>
  </div>

<script>
  let ideas = [];

  function addIdea() {
    const input = document.getElementById('ideaInput');
    const idea = input.value.trim();
    if (idea) {
      ideas.push(idea);
      updateIdeasList();
      input.value = '';
    }
  }

  function updateIdeasList() {
    const list = document.getElementById('ideasList');
    list.innerHTML = '';
    ideas.forEach((idea, index) => {
      const li = document.createElement('li');
      li.textContent = idea;
      list.appendChild(li);
    });
  }

  function randomizeIdea() {
    if (ideas.length === 0) {
      alert('No ideas to randomize!');
      return;
    }
    const randomIndex = Math.floor(Math.random() * ideas.length);
    document.getElementById('resultBox').textContent = ideas[randomIndex];
  }

  function clearIdeas() {
    if (confirm('Clear all ideas?')) {
      ideas = [];
      updateIdeasList();
      document.getElementById('resultBox').textContent = 'Your random idea will appear here.';
    }
  }

  function addToCalendar() {
    const idea = document.getElementById('resultBox').textContent;
    if (!idea || idea === 'Your random idea will appear here.') {
      alert('No idea selected to add to calendar.');
      return;
    }
    const start = new Date();
    const end = new Date(start.getTime() + 60 * 60 * 1000);
    const startStr = start.toISOString().replace(/-|:|\.\d\d\d/g,"");
    const endStr = end.toISOString().replace(/-|:|\.\d\d\d/g,"");
    const href = `data:text/calendar;charset=utf-8,BEGIN:VCALENDAR
VERSION:2.0
BEGIN:VEVENT
DTSTART:${startStr}
DTEND:${endStr}
SUMMARY:${idea}
END:VEVENT
END:VCALENDAR`;
    const link = document.createElement('a');
    link.href = href;
    link.download = 'idea.ics';
    link.click();
  }

  function shareIdea() {
    const idea = document.getElementById('resultBox').textContent;
    if (navigator.share) {
      navigator.share({
        title: 'Idea',
        text: idea
      });
    } else {
      alert('Sharing not supported on this device.');
    }
  }
</script>
</body>
</html>
