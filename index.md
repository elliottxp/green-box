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
    margin: 0 auto; /* ensures horizontal center */
  }

  h1 {
    font-family: 'Aesop';
    font-weight: 600;
    font-size: 2rem;
    margin-bottom: 0.75rem;
  }

  .fact {
    font-family: 'Aesop';
    color: var(--accent-color);
    margin-bottom: 1.5rem;
    line-height: 1.4;
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

  /* Settings panel */
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

<h1 style="text-align:center;">green-box</h1>
  <h2 style="text-align:center;">Plan for Kindness</h2>
<p class="fact" style="text-align:center;">
    Did you know? The average person spends over 3 hours a day on their phone and 5 hours indoors, often sitting inactive. Let’s add more meaningful, healthy moments to your day.
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
  /* Your JavaScript remains unchanged */
</script>

</body>
</html>
