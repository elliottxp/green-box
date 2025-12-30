---
layout: default
description: "plan your day"
title: "about"
permalink: /about/
order: 2
---
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>about</title>

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

  .about-container {
    background: #fff;
    border-radius: var(--radius);
    padding: 2rem;
    max-width: 480px;
    width: 100%;
    box-shadow: 0 8px 24px rgba(0,0,0,0.05);
    margin: 0 auto; /* horizontal center */
    position: relative; /* needed for settings button */
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

  p {
    line-height: 1.5;
    margin-bottom: 1rem;
    font-family: 'Aesop';
    font-size: 1rem;
  }

  a {
    color: var(--accent-color);
    text-decoration: none;
    font-family: 'Aesop';
    font-weight: 600;
    border-bottom: 2px solid transparent;
    transition: border-color 0.3s ease;
  }

  a:hover,
  a:focus {
    border-color: var(--accent-color);
    outline: none;
  }

  @media (max-width: 500px) {
    body {
      padding: 1rem;
    }
    .about-container {
      padding: 1.5rem;
      border-radius: 0;
      box-shadow: none;
      min-height: 100vh;
    }
  }
</style>
</head>

<body>
  <section class="about-container" aria-labelledby="aboutTitle">
    <h1 id="aboutTitle">about green-box</h1>

    <p>My wife and I sometimes found ourselves unsure of what to do on weekends or during our spare time. One day, we wanted to add a bit of randomness to our plans. So, I took an old box and covered it in green tissue paper. We often argued about always doing what one of us wanted rather than the other. To solve this, we wrote down activities we each wanted to do with her on small pieces of paper, scrunched them up, and placed them in the box. She did the same. Before long, we had a box full of our ideas. When we were bored or need something to to, we would take turns pulling ideas out of the green box at random. This box became a great decion maker, we could both contribute what we wanted to do, and the final choice would be left up to chance.</p>
    <p>I wanted to share this idea with others, so we created the green-box idea generator.</p>
    <p>My aim is to help you create happier habits by doing small, meaningful activities every day. These small changes made a big difference in our wellbeing, in the prime of our green-box use.</p>
    
    <img src="/img/box.png" alt="Green Box" style="max-width:100%; height:auto; display:block; margin:20px 0;" />

    <h2>What the page does?</h2>
    <p>This website offers daily ideas, lets you submit your own, and helps you build a personalised list of activities to refresh your mind and body.</p>

    <h2>Contact Me</h2>
    <p>Have questions or feedback? Reach out at <a href="mailto:relax@green-box.app">relax@green-box.app</a> — I'd love to hear from you!</p>
  </section>
</body>
</html>
