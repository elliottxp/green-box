<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Wellbeing Idea Generator</title>
  <!-- Boska Font -->
  <link href="https://api.fontshare.com/v2/css?f[]=boska@400,600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-color: #f9f9f9;
      --text-color: #2c2c2c;
      --accent-color: #5a7f65;
      --border-color: #e0e0e0;
      --button-radius: 12px;
    }

    body {
      font-family: 'Boska', serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 2rem;
      display: flex;
      justify-content: center;
      min-height: 100vh;
    }

    .app-container {
      background: #fff;
      border-radius: 20px;
      padding: 2rem;
      max-width: 480px;
      width: 100%;
      box-shadow: 0 6px 20px rgba(0,0,0,0.05);
    }

    h1 {
      font-size: 2rem;
      font-weight: 600;
      margin-bottom: 0.75rem;
    }

    .fact {
      font-style: italic;
      color: var(--accent-color);
      margin-bottom: 1.5rem;
    }

    input[type="text"] {
      width: 100%;
      padding: 0.75rem 1rem;
      border: 1px solid var(--border-color);
      border-radius: var(--button-radius);
      font-size: 1rem;
      margin-bottom: 1rem;
      transition: border-color 0.2s ease;
    }

    input[type="text"]:focus {
      outline: none;
      border-color: var(--accent-color);
      box-shadow: 0 0 0 3px rgba(90,127,101,0.15);
    }

    button {
      padding: 0.7rem 1.4rem;
      border-radius: var(--button-radius);
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: transform 0.1s ease, background-color 0.2s ease;
      border: none;
    }

    button:active {
      transform: scale(0.97);
    }

    /* Primary Button */
    .btn-primary {
      background-color: var(--accent-color);
      color: white;
    }
    .btn-primary:hover {
      background-color: #4b6f56;
    }

    /* Secondary Button */
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

    .idea-list {
      margin-top: 1.5rem;
      border-top: 1px solid var(--border-color);
      padding-top: 0.75rem;
      font-size: 0.95rem;
    }

    #clearIdeasBtn {
      margin-top: 1rem;
      background-color: #fdeaea;
      color: #a94442;
      border: 1px solid #f5c6cb;
    }
    #clearIdeasBtn:hover {
      background-color: #f8d7da;
    }

    @media (max-width: 500px) {
      .app-container {
        padding: 1.5rem 1rem;
        border-radius: 0;
        box-shadow: none;
      }
      button {
        width: 100%;
        margin-bottom: 0.75rem;
      }
    }
  </style>
</head>
