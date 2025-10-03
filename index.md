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
    font-size: 1.25rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background-color var(--transition);
  }

  #settingsToggle:hover { background-color: #4b6f56; }

  h1, h2, label { font-family: 'Aesop'; }
  h1 { font-weight: 600; font-size: 2rem; margin-bottom: 0.75rem; text-align: center; }
  h2 { text-align: center; }

  .fact {
    color: var(--accent-color);
    margin-bottom: 1.5rem;
    line-height: 1.4;
    text-align: center;
  }

  input[type="text"], input[type="date"], input[type="time"] {
    width: 100%;
    padding: 0.6rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-family: 'Aesop', serif;
    font-size: 1rem;
    margin-bottom: 1rem;
    transition: border-color var(--transition), box-shadow var(--transition);
  }

  input:focus {
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
  .btn-secondary {
    background: transparent; color: var(--accent-color); border: 1px solid var(--accent-color);
  }
  .btn-secondary:hover { background-color: rgba(90,127,101,0.08); }

  .idea-display {
    margin: 1.5rem 0;
    font-size: 1.3rem;
    color: var(--accent-color);
    font-weight: 600;
    min-height: 2rem;
    opacity: 0;
    transition: opacity 0.4s ease;
  }
  .idea-display.show { opacity: 1; }

  .actions { margin-top: 1rem; display: flex; flex-wrap: wrap; gap: 0.75rem; }

  /* Modal overlay (default desktop) */
  .modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.4);
    justify-content: center;
    align-items: center;
    z-index: 100;
  }
  .modal-content {
    background: #fff;
    border-radius: var(--radius);
    padding: 1.5rem;
    max-width: 400px;
    width: 90%;
    box-shadow: 0 8px 24px rgba(0,0,0,0.15);
    animation: fadeIn 0.3s ease;
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(-10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Inline modal on mobile */
  @media (max-width: 500px) {
    .modal {
      position: static;
      background: none;
      display: none;
      margin-top: 1rem;
      justify-content: initial;
      align-items: initial;
    }
    .modal-content {
      width: 100%;
      max-width: 100%;
      box-shadow: none;
      border: 1px solid var(--border-color);
      padding: 1rem;
      animation: slideDown 0.3s ease;
    }
    @keyframes slideDown {
      from { opacity: 0; transform: translateY(-10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  }
</style>
</head>

<body>
<div class="app-container" role="main" aria-label="Green-box">
  <button id="settingsToggle">&#9881;</button>

  <h1>green-box</h1>
  <h2>Plan for Kindness</h2>
  <p class="fact">Did you know? The average person spends around 3 hours a day on their phone and 5 hours indoors. Let’s add some different moments to your day.</p>

  <label for="ideaInput">Submit your idea:</label>
  <input type="text" id="ideaInput" placeholder="e.g. Take a 10-minute walk" />
  <button id="addIdeaBtn" class="btn-primary">Add to box</button>

  <div class="actions">
    <button id="suggestIdeaBtn" class="btn-secondary">Draw from box</button>
  </div>

  <div class="idea-display" id="ideaDisplay"></div>

  <div class="actions" id="ideaActions" style="display:none;">
    <button id="addToCalendarBtn" class="btn-secondary">Add to Calendar</button>
    <button id="shareIdeaBtn" class="btn-secondary">Share Idea</button>
  </div>

  <!-- Inline/Overlay Modal -->
  <div id="calendarModal" class="modal">
    <div class="modal-content">
      <h3>Choose Date & Time</h3>
      <label for="eventDate">Date:</label>
      <input type="date" id="eventDate" />
      <label for="eventTime">Time:</label>
      <input type="time" id="eventTime" />
      <div class="modal-actions">
        <button id="saveEventBtn" class="btn-primary">Save Event</button>
        <button id="cancelModalBtn" class="btn-secondary">Cancel</button>
      </div>
    </div>
  </div>
</div>

<script>
  const suggestIdeaBtn = document.getElementById('suggestIdeaBtn');
  const ideaDisplay = document.getElementById('ideaDisplay');
  const ideaActions = document.getElementById('ideaActions');
  const addToCalendarBtn = document.getElementById('addToCalendarBtn');
  const shareIdeaBtn = document.getElementById('shareIdeaBtn');
  const calendarModal = document.getElementById('calendarModal');
  const saveEventBtn = document.getElementById('saveEventBtn');
  const cancelModalBtn = document.getElementById('cancelModalBtn');
  const eventDate = document.getElementById('eventDate');
  const eventTime = document.getElementById('eventTime');

  const ideas = ["Go and try a new cafe", "Do some art", "Play basketball", "Meditate for 5 minutes"];

  suggestIdeaBtn.addEventListener('click', () => {
    const idea = ideas[Math.floor(Math.random() * ideas.length)];
    ideaDisplay.textContent = idea;
    ideaDisplay.classList.add('show');
    ideaActions.style.display = 'flex';
    addToCalendarBtn.dataset.idea = idea;
    shareIdeaBtn.dataset.idea = idea;
  });

  addToCalendarBtn.addEventListener('click', () => {
    if (window.innerWidth <= 500) {
      calendarModal.style.display = 'block'; // inline mobile
    } else {
      calendarModal.style.display = 'flex';  // overlay desktop
    }
  });

  cancelModalBtn.addEventListener('click', () => {
    calendarModal.style.display = 'none';
  });

  saveEventBtn.addEventListener('click', () => {
    const idea = addToCalendarBtn.dataset.idea;
    if (!idea) return;
    const dateVal = eventDate.value;
    const timeVal = eventTime.value;
    if (!dateVal || !timeVal) {
      alert("Please select both date and time.");
      return;
    }
    const start = new Date(`${dateVal}T${timeVal}`);
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

    calendarModal.style.display = 'none';
  });
</script>
</body>
</html>
