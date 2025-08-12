<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Wellbeing Idea App</title>
<style>
  /* Using Aesop Regular custom font */
  @font-face {
    font-family: 'AesopRegular';
    src: url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.woff2') format('woff2'),
         url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.woff') format('woff'),
         url('https://db.onlinewebfonts.com/t/f013f368755877264cb04fb82a39fc60.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
  }

  :root {
    --bg-color: #fcfbf9;
    --text-color: #2c2a28;
    --accent-color: #c1c0bd;
    --button-bg: #e5e3df;
    --button-hover: #d1cec9;
    --border-color: #bebbb5;
  }

  body {
    margin: 0;
    padding: 20px;
    font-family: 'AesopRegular', serif;
    background-color: var(--bg-color);
    color: var(--text-color);
    line-height: 1.6;
  }

  .container {
    max-width: 500px;
    margin: auto;
  }

  h1 {
    font-size: 1.8rem; /* ~18pt */
    text-align: center;
    margin-bottom: 0.5em;
  }

  .fact {
    background-color: var(--accent-color);
    padding: 12px;
    border-radius: 6px;
    margin-bottom: 1em;
    font-size: 1rem;
  }

  input, button {
    width: 100%;
    padding: 14px;
    margin-bottom: 12px;
    font-size: 1rem;
    border: 1px solid var(--border-color);
    border-radius: 6px;
  }

  button {
    background-color: var(--button-bg);
    cursor: pointer;
    transition: background-color 0.2s ease;
  }
  button:hover {
    background-color: var(--button-hover);
  }

  .ideas-list {
    list-style: none;
    padding: 0;
    margin-bottom: 12px;
  }

  .ideas-list li {
    background: white;
    border: 1px solid var(--border-color);
    border-radius: 6px;
    padding: 10px;
    margin-bottom: 8px;
  }

  .result-box {
    background: white;
    padding: 16px;
    border: 1px solid var(--border-color);
    border-radius: 6px;
    font-size: 1.1rem;
    text-align: center;
    margin-bottom: 12px;
  }

  @media (max-width: 600px) {
    h1 {
      font-size: 1.5rem;
    }
  }
</style>
</head>
<body>
  <div class="container">
    <h1>Wellbeing Idea App</h1>
    <p class="fact">Did you know? Even 10 minutes of stepping away from screens and being active improves your mood and focus.</p>

    <input type="text" id="ideaInput" placeholder="eg. Take a 10-minute walk">
    <button onclick="addIdea()">Add Idea</button>
    <button onclick="pickIdea()">Suggest an Idea</button>
    <button onclick="clearIdeas()">Clear All Ideas</button>

    <ul class="ideas-list" id="ideasList"></ul>

    <div class="result-box" id="resultBox">Your suggestion will appear here.</div>
    <button onclick="addToCalendar()">Add to Calendar</button>
    <button onclick="shareIdea()">Share</button>
  </div>

  <script>
    let ideas = [];

    function addIdea() {
      const input = document.getElementById('ideaInput');
      const val = input.value.trim();
      if (val) {
        ideas.push(val);
        updateList();
        input.value = '';
      }
    }

    function updateList() {
      const list = document.getElementById('ideasList');
      list.innerHTML = '';
      ideas.forEach((idea) => {
        const li = document.createElement('li');
        li.textContent = idea;
        list.appendChild(li);
      });
    }

    function pickIdea() {
      if (!ideas.length) return alert('No ideas available.');
      const rand = ideas[Math.floor(Math.random() * ideas.length)];
      document.getElementById('resultBox').textContent = rand;
    }

    function clearIdeas() {
      if (confirm('Clear all ideas?')) {
        ideas = [];
        updateList();
        document.getElementById('resultBox').textContent = 'Your suggestion will appear here.';
      }
    }

    function addToCalendar() {
      const idea = document.getElementById('resultBox').textContent;
      if (!idea || idea.includes('Your suggestion')) {
        return alert('No idea selected.');
      }
      const start = new Date();
      const end = new Date(start.getTime() + 60 * 60 * 1000);
      const startISO = start.toISOString().replace(/[-:.\d]/g, '');
      const endISO = end.toISOString().replace(/[-:.\d]/g, '');
      const dataUri = `data:text/calendar;charset=utf8,BEGIN:VCALENDAR\nVERSION:2.0\nBEGIN:VEVENT\nDTSTART:${startISO}\nDTEND:${endISO}\nSUMMARY:${idea}\nEND:VEVENT\nEND:VCALENDAR`;
      window.location.href = dataUri;  // Should prompt iOS Calendar
    }

    function shareIdea() {
      const idea = document.getElementById('resultBox').textContent;
      if (navigator.share && idea && !idea.includes('Your suggestion')) {
        navigator.share({ title: 'Wellbeing Idea', text: idea });
      } else {
        alert('Sharing not supported or no idea selected.');
      }
    }
  </script>
</body>
</html>

