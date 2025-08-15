<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>green-box</title>

<style>
  @font-face {
    font-family: 'Aesop';
    src: url('Font%20Regular.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
  }

  *, *::before, *::after { box-sizing: border-box; }
  :root {
    --bg-color: #f9f9f9;
    --text-color: #2c2c2c;
    --accent-color: #5a7f65;
    --border-color: #e0e0e0;
    --danger-bg: #fdeaea;
    --danger-border: #f5c6cb;
    --danger-text: #a94442;
    --radius: 14px;
    --transition: 0.25s ease;
  }

  body {
    background-color: var(--bg-color);
    color: var(--text-color);
    font-family: 'Aesop', serif;
    margin: 0;
    padding: 2rem;
    display: flex;
    justify-content: center;
    min-height: 100vh;
  }

  .app-container {
    background: #fff;
    border-radius: var(--radius);
    padding: 2rem;
    max-width: 480px;
    width: 100%;
    box-shadow: 0 8px 24px rgba(0,0,0,0.05);
    margin: 0 auto;
    position: relative;
  }

  #settingsToggle {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    border-radius: 50%;
    width: 36px;
    height: 36px;
    color: white;
    font-family: 'Aesop';
    font-size: 1.25rem;
    cursor: pointer;
    line-height: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 2px 8px rgba(0,0,0,0.15);
    transition: background-color var(--transition);
  }
  #settingsToggle:hover { background-color: #4b6f56; }

  h1 { font-weight: 600; font-size: 2rem; margin-bottom: 0.75rem; text-align: center; }
  h2 { text-align: center; }
  .fact { color: var(--accent-color); margin-bottom: 1.5rem; line-height: 1.4; text-align: center; }

  label { display: block; font-weight: 600; margin-bottom: 0.5rem; }
  input[type="text"], select {
    width: 100%;
    padding: 0.6rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-family: 'Aesop', serif;
    font-size: 1rem;
    margin-bottom: 1rem;
    transition: border-color var(--transition), box-shadow var(--transition);
  }
  input[type="text"]:focus, select:focus {
    outline: none;
    border-color: var(--accent-color);
    box-shadow: 0 0 0 3px rgba(90,127,101,0.15);
  }

  button {
    padding: 0.65rem 1.2rem;
    border-radius: var(--radius);
    font-family: 'Aesop', serif;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    border: none;
    transition: background-color var(--transition), transform var(--transition);
  }
  button:active { transform: scale(0.97); }
  .btn-primary { background-color: var(--accent-color); color: white; }
  .btn-primary:hover { background-color: #4b6f56; }
  .btn-secondary { background: transparent; color: var(--accent-color); border: 1px solid var(--accent-color); }
  .btn-secondary:hover { background-color: rgba(90,127,101,0.08); }

  .idea-display { margin: 1.5rem 0; font-size: 1.3rem; color: var(--accent-color); font-weight: 600; min-height: 2rem; opacity: 0; transition: opacity 0.4s ease; }
  .idea-display.show { opacity: 1; }
  .actions { margin-top: 1rem; display: flex; flex-wrap: wrap; gap: 0.75rem; }

  .idea-list { margin-top: 1.5rem; border-top: 1px solid var(--border-color); padding-top: 0.75rem; font-size: 0.95rem; }
  .idea-list strong { display: block; margin-bottom: 0.5rem; }
  .idea-section { margin-bottom: 1rem; }
  .idea-section ul { padding-left: 1.2rem; margin-top: 0.25rem; }
  .remove-btn { background: none; border: none; color: var(--danger-text); font-size: 0.85rem; margin-left: 0.5rem; cursor: pointer; }
  .remove-btn:hover { text-decoration: underline; }

  #clearIdeasBtn { background-color: var(--danger-bg); color: var(--danger-text); border: 1px solid var(--danger-border); margin-top: 0.5rem; }
  #clearIdeasBtn:hover { background-color: #f8d7da; }

  .footer-note { margin-top: 2rem; font-size: 0.85rem; color: #7a7a75; text-align: center; }

  #settingsPanel {
    position: absolute;
    top: 3.5rem;
    right: 1rem;
    width: 280px;
    background: #fff;
    border-radius: var(--radius);
    box-shadow: 0 8px 24px rgba(0,0,0,0.1);
    padding: 1rem 1.5rem;
    font-size: 0.9rem;
    display: none;
    z-index: 10;
  }
  #settingsPanel label { font-weight: 600; margin-bottom: 0.25rem; display: block; }
  #settingsPanel input[type="checkbox"] { margin-right: 0.5rem; transform: scale(1.15); cursor: pointer; }
  #restoreDefaultsBtn { margin-top: 1rem; width: 100%; background-color: var(--accent-color); color: white; }
  #restoreDefaultsBtn:hover { background-color: #4b6f56; }

  @media (max-width: 500px) {
    body { padding: 1rem; }
    .app-container { padding: 1.5rem 1rem; border-radius: 0; box-shadow: none; min-height: 100vh; }
    button { width: 100%; }
    #settingsPanel { width: 90vw; right: 5vw; top: 3.5rem; }
  }
</style>
</head>

<body>
<div class="app-container">

  <button id="settingsToggle" aria-expanded="false" aria-controls="settingsPanel">&#9881;</button>

  <h1>green-box</h1>
  <h2>Plan for Kindness</h2>
  <p class="fact">
    Did you know? The average person spends over 3 hours a day on their phone and 5 hours indoors, often sitting inactive. Let’s add more meaningful, healthy moments to your day.
  </p>

  <label for="ideaInput">Submit your idea:</label>
  <input type="text" id="ideaInput" placeholder="e.g. Take a 10-minute walk" />
  <label for="ideaDuration">Time required:</label>
  <select id="ideaDuration">
    <option value="5 min">5 min</option>
    <option value="10 min">10 min</option>
    <option value="30 min">30 min</option>
    <option value="1 hour">1 hour</option>
    <option value="2+ hours">2+ hours</option>
  </select>
  <button id="addIdeaBtn" class="btn-primary">Add to box</button>

  <div class="actions">
    <button id="suggestIdeaBtn" class="btn-secondary">Draw from box</button>
  </div>

  <div class="idea-display" id="ideaDisplay"></div>
  <div class="actions" id="ideaActions" style="display:none;">
    <button id="addToCalendarBtn" class="btn-secondary">Add to Calendar</button>
    <button id="shareIdeaBtn" class="btn-secondary">Share Idea</button>
  </div>

  <label for="timeFilter">Filter by time:</label>
  <select id="timeFilter">
    <option value="">All</option>
    <option value="5 min">5 min</option>
    <option value="10 min">10 min</option>
    <option value="30 min">30 min</option>
    <option value="1 hour">1 hour</option>
    <option value="2+ hours">2+ hours</option>
  </select>

  <div class="idea-list">
    <div class="idea-section">
      <strong>Your ideas:</strong>
      <ul id="userIdeasUl"></ul>
      <button id="clearIdeasBtn">Bin My Ideas</button>
    </div>
    <div class="idea-section" id="defaultIdeasSection">
      <strong>Default ideas:</strong>
      <ul id="defaultIdeasUl"></ul>
    </div>
  </div>

  <p class="footer-note">Ideas are stored locally in the box. Refreshing will keep your list of ideas.</p>

  <div id="settingsPanel">
    <label><input type="checkbox" id="toggleDefaults" />Show default ideas</label>
    <button id="restoreDefaultsBtn">Restore All Default Ideas</button>
  </div>
</div>

<script>
  const defaultIdeas = [
    { text: "Go and try a new cafe", duration: "1 hour" },
    { text: "Do some art", duration: "30 min" },
    { text: "Play basketball", duration: "1 hour" },
    { text: "Meditate for 5 minutes", duration: "5 min" },
    { text: "Go for a walk around the block", duration: "10 min" },
    { text: "Cook some muffins", duration: "1 hour" }
    // ...add the rest
  ];

  let userIdeas = JSON.parse(localStorage.getItem('userIdeas')) || [];
  let activeDefaultIdeas = JSON.parse(localStorage.getItem('activeDefaultIdeas')) || [...defaultIdeas];
  let showDefaults = JSON.parse(localStorage.getItem('showDefaults'));
  if (showDefaults === null) showDefaults = true;

  const ideaInput = document.getElementById('ideaInput');
  const ideaDuration = document.getElementById('ideaDuration');
  const timeFilter = document.getElementById('timeFilter');
  const addIdeaBtn = document.getElementById('addIdeaBtn');
  const suggestIdeaBtn = document.getElementById('suggestIdeaBtn');
  const ideaDisplay = document.getElementById('ideaDisplay');
  const ideaActions = document.getElementById('ideaActions');
  const addToCalendarBtn = document.getElementById('addToCalendarBtn');
  const shareIdeaBtn = document.getElementById('shareIdeaBtn');
  const userIdeasUl = document.getElementById('userIdeasUl');
  const defaultIdeasUl = document.getElementById('defaultIdeasUl');
  const clearIdeasBtn = document.getElementById('clearIdeasBtn');
  const defaultIdeasSection = document.getElementById('defaultIdeasSection');
  const settingsToggle = document.getElementById('settingsToggle');
  const settingsPanel = document.getElementById('settingsPanel');
  const toggleDefaultsCheckbox = document.getElementById('toggleDefaults');
  const restoreDefaultsBtn = document.getElementById('restoreDefaultsBtn');

  function updateIdeaLists() {
    const filterValue = timeFilter.value;
    userIdeasUl.innerHTML = '';
    defaultIdeasUl.innerHTML = '';

    userIdeas.forEach((idea, index) => {
      if (!filterValue || idea.duration === filterValue) {
        const li = document.createElement('li');
        li.textContent = `${idea.text} (${idea.duration})`;
        const removeBtn = document.createElement('button');
        removeBtn.textContent = 'remove';
        removeBtn.className = 'remove-btn';
        removeBtn.onclick = () => { userIdeas.splice(index, 1); saveIdeas(); updateIdeaLists(); };
        li.appendChild(removeBtn);
        userIdeasUl.appendChild(li);
      }
    });

    if (showDefaults) {
      defaultIdeasSection.style.display = 'block';
      activeDefaultIdeas.forEach((idea, index) => {
        if (!filterValue || idea.duration === filterValue) {
          const li = document.createElement('li');
          li.textContent = `${idea.text} (${idea.duration})`;
          const removeBtn = document.createElement('button');
          removeBtn.textContent = 'remove';
          removeBtn.className = 'remove-btn';
          removeBtn.onclick = () => { activeDefaultIdeas.splice(index, 1); saveIdeas(); updateIdeaLists(); };
          li.appendChild(removeBtn);
          defaultIdeasUl.appendChild(li);
        }
      });
    } else {
      defaultIdeasSection.style.display = 'none';
    }
  }

  function saveIdeas() {
    localStorage.setItem('userIdeas', JSON.stringify(userIdeas));
    localStorage.setItem('activeDefaultIdeas', JSON.stringify(activeDefaultIdeas));
    localStorage.setItem('showDefaults', JSON.stringify(showDefaults));
  }

  addIdeaBtn.addEventListener('click', () => {
    const newIdeaText = ideaInput.value.trim();
    const newDuration = ideaDuration.value;
    if (newIdeaText && !userIdeas.some(i => i.text === newIdeaText)) {
      userIdeas.push({ text: newIdeaText, duration: newDuration });
      saveIdeas();
      updateIdeaLists();
      ideaInput.value = '';
    }
  });

  suggestIdeaBtn.addEventListener('click', () => {
    const filterValue = timeFilter.value;
    let allIdeas = [...userIdeas];
    if (showDefaults) allIdeas.push(...activeDefaultIdeas);
    if (filterValue) allIdeas = allIdeas.filter(i => i.duration === filterValue);

    if (!allIdeas.length) {
      ideaDisplay.textContent = "No ideas for that time.";
      ideaActions.style.display = 'none';
      return;
    }
    const idea = allIdeas[Math.floor(Math.random() * allIdeas.length)];
    ideaDisplay.textContent = `${idea.text} (${idea.duration})`;
    ideaDisplay.classList.remove('show');
    void ideaDisplay.offsetWidth;
    ideaDisplay.classList.add('show');
    ideaActions.style.display = 'flex';
    addToCalendarBtn.dataset.idea = idea.text;
    shareIdeaBtn.dataset.idea = idea.text;
  });

  timeFilter.addEventListener('change', updateIdeaLists);

  clearIdeasBtn.addEventListener('click', () => {
    if (confirm("Delete all personal ideas?")) {
      userIdeas = [];
      saveIdeas();
      updateIdeaLists();
    }
  });

  settingsToggle.addEventListener('click', () => {
    const expanded = settingsToggle.getAttribute('aria-expanded') === 'true';
    settingsPanel.style.display = expanded ? 'none' : 'block';
    settingsToggle.setAttribute('aria-expanded', !expanded);
  });

  toggleDefaultsCheckbox.checked = showDefaults;
  toggleDefaultsCheckbox.addEventListener('change', () => { showDefaults = toggleDefaultsCheckbox.checked; saveIdeas(); updateIdeaLists(); });

  restoreDefaultsBtn.addEventListener('click', () => {
    activeDefaultIdeas = [...defaultIdeas];
    showDefaults = true;
    toggleDefaultsCheckbox.checked = true;
    saveIdeas();
    updateIdeaLists();
  });

  updateIdeaLists();
</script>

</body>
</html>
