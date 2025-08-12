<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Wellbeing Idea Generator</title>

<!-- Boska Font from Fontshare -->
<link href="https://api.fontshare.com/v2/css?f[]=boska@400,600&display=swap" rel="stylesheet">

<style>
  :root {
    --bg-color: #f9f9f9;
    --text-color: #2c2c2c;
    --accent-color: #5a7f65;
    --border-color: #e0e0e0;
    --danger-bg: #fdeaea;
    --danger-border: #f5c6cb;
    --danger-text: #a94442;
    --radius: 14px;
    --transition: 0.2s ease;
  }

  body {
    background-color: var(--bg-color);
    color: var(--text-color);
    font-family: 'Boska', serif;
    margin: 0;
    padding: 2rem;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: 100vh;
  }

  .app-container {
    background: #fff;
    border-radius: var(--radius);
    padding: 2rem;
    max-width: 480px;
    width: 100%;
    box-shadow: 0 8px 24px rgba(0,0,0,0.05);
  }

  h1 {
    font-weight: 600;
    font-size: 2rem;
    margin-bottom: 0.75rem;
  }

  .fact {
    font-style: italic;
    color: var(--accent-color);
    margin-bottom: 1.5rem;
    line-height: 1.4;
  }

  label {
    display: block;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }

  input[type="text"] {
    width: 100%;
    padding: 0.75rem 1rem;
    border: 1px solid var(--border-color);
    border-radius: var(--radius);
    font-family: 'Boska', serif;
    font-size: 1rem;
    margin-bottom: 1rem;
    transition: border-color var(--transition), box-shadow var(--transition);
  }

  input[type="text"]:focus {
    outline: none;
    border-color: var(--accent-color);
    box-shadow: 0 0 0 3px rgba(90,127,101,0.15);
  }

  button {
    padding: 0.75rem 1.4rem;
    border-radius: var(--radius);
    font-family: 'Boska', serif;
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
    font-size: 1.3rem;
    color: var(--accent-color);
    font-weight: 600;
    min-height: 2rem;
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
    font-size: 0.95rem;
  }

  .idea-list strong {
    display: block;
    margin-bottom: 0.5rem;
  }

  #clearIdeasBtn {
    background-color: var(--danger-bg);
    color: var(--danger-text);
    border: 1px solid var(--danger-border);
    font-weight: 600;
  }
  #clearIdeasBtn:hover {
    background-color: #f8d7da;
  }

  .footer-note {
    margin-top: 2rem;
    font-size: 0.85rem;
    color: #7a7a75;
    text-align: center;
  }

  /* Mobile-first adjustments */
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
  }
</style>
</head>

<body>
<div class="app-container" role="main" aria-label="Wellbeing Idea Generator App">
  <h1>Wellbeing Idea Generator</h1>
  <p class="fact">
    Did you know? The average person spends over 3 hours a day on their phone and 5 hours indoors, often sitting inactive. Let’s add more meaningful, healthy moments to your day.
  </p>

  <label for="ideaInput">Submit your idea of something to do:</label>
  <input type="text" id="ideaInput" placeholder="e.g. Take a 10-minute walk" aria-describedby="ideaHelp" />
  <button id="addIdeaBtn" class="btn-primary">Add Idea</button>

  <div class="actions">
    <button id="suggestIdeaBtn" class="btn-secondary">Suggest an Idea</button>
  </div>

  <div class="idea-display" id="ideaDisplay" aria-live="polite" aria-atomic="true"></div>

  <div class="actions" id="ideaActions" style="display:none;">
    <button id="addToCalendarBtn" class="btn-secondary">Add to Calendar</button>
    <button id="shareIdeaBtn" class="btn-secondary">Share Idea</button>
  </div>

  <div class="idea-list" id="ideaList" aria-label="List of your ideas">
    <strong>Your ideas:</strong>
    <ul id="ideasUl" style="padding-left: 1.2rem; margin-top: 0;"></ul>
    <button id="clearIdeasBtn">Clear Ideas</button>
  </div>

  <p class="footer-note">Ideas are stored locally in your browser. Refreshing will keep your list.</p>
</div>

<script>
  // Predefined suggestions
  const suggestedIdeas = [
    "Take a 10-minute mindful walk outside",
    "Try a new healthy recipe",
    "Call a friend or family member",
    "Do a 5-minute stretching routine",
    "Write down three things you’re grateful for",
    "Read a chapter of a book",
    "Meditate for 5 minutes",
    "Drink a glass of water",
    "Spend 10 minutes journaling",
    "Declutter a small area of your home"
  ];

  let ideas = JSON.parse(localStorage.getItem('wellbeingIdeas')) || [...suggestedIdeas];

  const ideaInput = document.getElementById('ideaInput');
  const addIdeaBtn = document.getElementById('addIdeaBtn');
  const suggestIdeaBtn = document.getElementById('suggestIdeaBtn');
  const ideaDisplay = document.getElementById('ideaDisplay');
  const ideaActions = document.getElementById('ideaActions');
  const addToCalendarBtn = document.getElementById('addToCalendarBtn');
  const shareIdeaBtn = document.getElementById('shareIdeaBtn');
  const ideasUl = document.getElementById('ideasUl');
  const clearIdeasBtn = document.getElementById('clearIdeasBtn');

  function updateIdeaList() {
    ideasUl.innerHTML = '';
    ideas.forEach((idea) => {
      const li = document.createElement('li');
      li.textContent = idea;
      ideasUl.appendChild(li);
    });
  }

  function saveIdeas() {
    localStorage.setItem('wellbeingIdeas', JSON.stringify(ideas));
  }

  addIdeaBtn.addEventListener('click', () => {
    const newIdea = ideaInput.value.trim();
    if(newIdea && !ideas.includes(newIdea)) {
      ideas.push(newIdea);
      saveIdeas();
      updateIdeaList();
      ideaInput.value = '';
      ideaInput.focus();
    }
  });

  suggestIdeaBtn.addEventListener('click', () => {
    if (ideas.length === 0) {
      ideaDisplay.textContent = "No ideas available. Please add some!";
      ideaActions.style.display = 'none';
      return;
    }
    const randomIndex = Math.floor(Math.random() * ideas.length);
    const idea = ideas[randomIndex];
    ideaDisplay.textContent = idea;
    ideaActions.style.display = 'flex';

    addToCalendarBtn.dataset.idea = idea;
    shareIdeaBtn.dataset.idea = idea;
  });

  addToCalendarBtn.addEventListener('click', () => {
    const idea = addToCalendarBtn.dataset.idea;
    if(!idea) return;

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
    if(!idea) return;

    if (navigator.share) {
      try {
        await navigator.share({
          title: 'Wellbeing Idea',
          text: idea,
        });
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
    if (confirm("Are you sure you want to clear all your ideas? This action cannot be undone.")) {
      ideas = [...suggestedIdeas];
      saveIdeas();
      updateIdeaList();
      ideaDisplay.textContent = '';
      ideaActions.style.display = 'none';
    }
  });

  // Initialize
  updateIdeaList();
</script>
</body>
</html>
