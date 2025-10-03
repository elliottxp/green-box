<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>green-box</title>

<!-- Load custom font -->
<style>
  @font-face {
    font-family: 'Aesop';
    src: url('Font%20Regular.ttf') format('truetype'); /* URL-encoded space */
    font-weight: normal;
    font-style: normal;
  }

  /* Prevent input overhang */
  *, *::before, *::after {
    box-sizing: border-box;
  }

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
    justify-content: center; /* horizontal centering only */
    min-height: 100vh;
  }

  .app-container {
    background: #fff;
    border-radius: var(--radius);
    padding: 2rem;
    max-width: 480px;
    width: 100%;
    box-shadow: 0 8px 24px rgba(0,0,0,0.05);
    margin: 0 auto; /* horizontal center */
    position: relative; /* needed for settings button */
  }

  /* Settings button in top-right corner of container */
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
  #settingsToggle:hover {
    background-color: #4b6f56;
  }

  h1 {
    font-family: 'Aesop';
    font-weight: 600;
    font-size: 2rem;
    margin-bottom: 0.75rem;
    text-align: center;
  }

  h2 {
    text-align: center;
  }

  .fact {
    font-family: 'Aesop';
    color: var(--accent-color);
    margin-bottom: 1.5rem;
    line-height: 1.4;
    text-align: center;
  }

  label {
    font-family: 'Aesop';
    display: block;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  input[type="text"] {
    width: 100%;
    padding: 0.6rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-family: 'Aesop', serif;
    font-size: 1rem;
    margin-bottom: 1rem;
    transition: border-color var(--transition), box-shadow var(--transition);
    box-sizing: border-box; /* prevents overflow */
  }

  input[type="text"]:focus {
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

  button:active {
    transform: scale(0.97);
  }

  .btn-primary {
    background-color: var(--accent-color);
    color: white;
  }
  .btn-primary:hover {
    background-color: #4b6f56;
  }

  .btn-secondary {
    background: transparent;
    color: var(--accent-color);
    border: 1px solid var(--accent-color);
  }
  .btn-secondary:hover {
    background-color: rgba(90,127,101,0.08);
  }

  .idea-display {
    margin: 1.5rem 0;
    font-family: 'Aesop';
    font-size: 1.3rem;
    color: var(--accent-color);
    font-weight: 600;
    min-height: 2rem;
    opacity: 0;
    transition: opacity 0.4s ease;
  }
  .idea-display.show {
    opacity: 1;
  }

  .actions {
    margin-top: 1rem;
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .idea-list {
    margin-top: 1.5rem;
    border-top: 1px solid var(--border-color);
    padding-top: 0.75rem;
    font-family: 'Aesop';
    font-size: 0.95rem;
  }

  .idea-list strong {
    display: block;
    margin-bottom: 0.5rem;
  }

  .idea-section {
    margin-bottom: 1rem;
  }

  .idea-section ul {
    padding-left: 1.2rem;
    margin-top: 0.25rem;
  }

  .remove-btn {
    background: none;
    border: none;
    color: var(--danger-text);
    font-family: 'Aesop';
    font-size: 0.85rem;
    margin-left: 0.5rem;
    cursor: pointer;
  }
  .remove-btn:hover {
    text-decoration: underline;
  }

  #clearIdeasBtn {
    background-color: var(--danger-bg);
    color: var(--danger-text);
    border: 1px solid var(--danger-border);
    font-family: 'Aesop';
    font-weight: 600;
    margin-top: 0.5rem;
  }
  #clearIdeasBtn:hover {
    background-color: #f8d7da;
  }

  .footer-note {
    margin-top: 2rem;
    font-family: 'Aesop';
    font-size: 0.85rem;
    color: #7a7a75;
    text-align: center;
  }

  #settingsPanel {
    position: absolute;
    top: 3.5rem;
    right: 1rem;
    width: 280px;
    background: #fff;
    border-radius: var(--radius);
    box-shadow: 0 8px 24px rgba(0,0,0,0.1);
    padding: 1rem 1.5rem;
    font-family: 'Aesop';
    font-size: 0.9rem;
    color: var(--text-color);
    display: none;
    z-index: 10;
  }

  #settingsPanel label {
    font-family: 'Aesop';
    font-weight: 600;
    margin-bottom: 0.25rem;
    display: block;
  }

  #settingsPanel input[type="checkbox"] {
    margin-right: 0.5rem;
    transform: scale(1.15);
    cursor: pointer;
  }

  #restoreDefaultsBtn {
    margin-top: 1rem;
    width: 100%;
    background-color: var(--accent-color);
    color: white;
  }
  #restoreDefaultsBtn:hover {
    background-color: #4b6f56;
  }

  @media (max-width: 500px) {
    body {
      padding: 1rem;
    }
    .app-container {
      padding: 1.5rem 1rem;
      border-radius: 0;
      box-shadow: none;
      min-height: 100vh;
    }
    button {
      width: 100%;
    }
    #settingsPanel {
      width: 90vw;
      right: 5vw;
      top: 3.5rem;
    }
  }
</style>
</head>

<body>
<div class="app-container" role="main" aria-label="Green-box">

  <button id="settingsToggle" aria-expanded="false" aria-controls="settingsPanel" aria-label="Open settings">&#9881;</button>

  <h1>green-box</h1>
  <h2>Plan for Kindness</h2>
  <p class="fact">
    Did you know? The average person spends around 3 hours a day on their phone and 5 hours indoors, often sitting inactive. Let’s add some nice moments to your day.
  </p>

  <label for="ideaInput">Submit your idea:</label>
  <input type="text" id="ideaInput" placeholder="e.g. Take a 10-minute walk" />
  <button id="addIdeaBtn" class="btn-primary">Add to box</button>

  <div class="actions">
    <button id="suggestIdeaBtn" class="btn-secondary">Draw from box</button>
  </div>

  <div class="idea-display" id="ideaDisplay" aria-live="polite" aria-atomic="true"></div>

  <div class="actions" id="ideaActions" style="display:none;">
    <button id="addToCalendarBtn" class="btn-secondary">Add to Calendar</button>
    <button id="shareIdeaBtn" class="btn-secondary">Share Idea</button>
  </div>

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

  <div id="settingsPanel" role="region" aria-label="Settings panel">
    <label>
      <input type="checkbox" id="toggleDefaults" />
      Show default ideas
    </label>
    <button id="restoreDefaultsBtn">Restore All Default Ideas</button>
  </div>
</div>

<script>
    const defaultIdeas = [
    "Go and try a new cafe",
    "Do some art",
    "Play basketball",
    "Go to the observatory",
    "Drive somewhere 1 hour away",
    "Meditate for 5 minutes",
    "Play a board game",
    "Go get an ice creamy",
    "Eat pizza and watch the sunset",
    "Go to botanical gardens or arboretum",
    "Go bowling",
    "Read books at the cafe",
    "Play tennis",
    "Go ice skating",
    "Take photos of things outdoors",
    "Go for a walk around the block",
    "Go for a swim at the pool, have salt & vinegar chips as a reward",
    "Cook some muffins",
    "Go to the art gallery",
    "Pick again to add suspense",
    "Cook something new",
    "Go for a bike ride",
    "Take a game to a cafe",
    "Go get Fish and Chips",
    "Hike on the mountain",
    "Listen to some music",
    "Have a picnic"
  ];

  let userIdeas = JSON.parse(localStorage.getItem('userIdeas')) || [];
  let activeDefaultIdeas = JSON.parse(localStorage.getItem('activeDefaultIdeas')) || [...defaultIdeas];
  let showDefaults = JSON.parse(localStorage.getItem('showDefaults'));
  if (showDefaults === null) showDefaults = true; // default true

  const ideaInput = document.getElementById('ideaInput');
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
    userIdeasUl.innerHTML = '';
    defaultIdeasUl.innerHTML = '';

    userIdeas.forEach((idea, index) => {
      const li = document.createElement('li');
      li.textContent = idea;
      const removeBtn = document.createElement('button');
      removeBtn.textContent = 'remove';
      removeBtn.className = 'remove-btn';
      removeBtn.onclick = () => {
        userIdeas.splice(index, 1);
        saveIdeas();
        updateIdeaLists();
      };
      li.appendChild(removeBtn);
      userIdeasUl.appendChild(li);
    });

    if (showDefaults) {
      defaultIdeasSection.style.display = 'block';
      activeDefaultIdeas.forEach((idea, index) => {
        const li = document.createElement('li');
        li.textContent = idea;
        const removeBtn = document.createElement('button');
        removeBtn.textContent = 'remove';
        removeBtn.className = 'remove-btn';
        removeBtn.onclick = () => {
          activeDefaultIdeas.splice(index, 1);
          saveIdeas();
          updateIdeaLists();
        };
        li.appendChild(removeBtn);
        defaultIdeasUl.appendChild(li);
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
    const newIdea = ideaInput.value.trim();
    if (newIdea && !userIdeas.includes(newIdea)) {
      userIdeas.push(newIdea);
      saveIdeas();
      updateIdeaLists();
      ideaInput.value = '';
      ideaInput.focus();
    }
  });

  suggestIdeaBtn.addEventListener('click', () => {
    const allIdeas = [...userIdeas];
    if (showDefaults) allIdeas.push(...activeDefaultIdeas);

    if (allIdeas.length === 0) {
      ideaDisplay.textContent = "No ideas available. Please add some!";
      ideaActions.style.display = 'none';
      return;
    }
    const randomIndex = Math.floor(Math.random() * allIdeas.length);
    const idea = allIdeas[randomIndex];
    ideaDisplay.textContent = idea;
    ideaDisplay.classList.remove('show');
    void ideaDisplay.offsetWidth; // restart animation
    ideaDisplay.classList.add('show');
    ideaActions.style.display = 'flex';
    addToCalendarBtn.dataset.idea = idea;
    shareIdeaBtn.dataset.idea = idea;
  });

  addToCalendarBtn.addEventListener('click', () => {
    const idea = addToCalendarBtn.dataset.idea;
    if (!idea) return;
    const now = new Date();
    const start = new Date(now.getTime() + 60 * 60 * 1000);
    const end = new Date(start.getTime() + 30 * 60 * 1000);
    function formatDate(d) {
      return d.toISOString().replace(/[-:]|\.\d{3}/g, '');
    }
    const icsContent = `BEGIN:VCALENDAR
VERSION:2.0
BEGIN:VEVENT
SUMMARY:${idea}
DTSTART:${formatDate(start)}
DTEND:${formatDate(end)}
DESCRIPTION:${idea}
END:VEVENT
END:VCALENDAR`;
    const blob = new Blob([icsContent], {type: 'text/calendar'});
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = 'wellbeing-idea.ics';
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    URL.revokeObjectURL(url);
  });

  shareIdeaBtn.addEventListener('click', async () => {
    const idea = shareIdeaBtn.dataset.idea;
    if (!idea) return;
    if (navigator.share) {
      try {
        await navigator.share({ title: 'Wellbeing Idea', text: idea });
      } catch (err) {
        alert('Sharing cancelled or not supported.');
      }
    } else {
      navigator.clipboard.writeText(idea).then(() => {
        alert('Idea copied to clipboard!');
      }, () => {
        alert('Failed to copy idea.');
      });
    }
  });

  clearIdeasBtn.addEventListener('click', () => {
    if (confirm("Are you sure you want to bin all your personal ideas?")) {
      userIdeas = [];
      saveIdeas();
      updateIdeaLists();
    }
  });

  // Settings toggle
  settingsToggle.addEventListener('click', () => {
    const expanded = settingsToggle.getAttribute('aria-expanded') === 'true';
    if (expanded) {
      settingsPanel.style.display = 'none';
      settingsToggle.setAttribute('aria-expanded', 'false');
    } else {
      settingsPanel.style.display = 'block';
      settingsToggle.setAttribute('aria-expanded', 'true');
    }
  });

  // Toggle default ideas visibility
  toggleDefaultsCheckbox.checked = showDefaults;
  toggleDefaultsCheckbox.addEventListener('change', () => {
    showDefaults = toggleDefaultsCheckbox.checked;
    saveIdeas();
    updateIdeaLists();
  });

  // Restore all default ideas button
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
