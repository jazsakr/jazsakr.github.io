---
title: "Random Tip Generator"
permalink: /random-tip/
---

<div class="tip-generator">
  <h2>Here's a random tip for you:</h2>
  <p id="tip-container" class="tip-text loader8"></p>
  <button id="new-tip-button" class="btn btn--primary" disabled>Get Another Tip</button>
</div>

<style>
  /* Styling the generator box */
  .tip-generator {
    text-align: center;
    padding: 2rem 1rem;
    border: 1px solid #e1e4e8;
    border-radius: 6px;
    background-color: #f6f8fa;
  }
  
  .tip-text {
    font-size: 1.2em;
    min-height: 60px; /* Prevents button from shifting */
    display: flex;
    align-items: center;
    justify-content: center;
    white-space: pre-wrap; /* preserves \n line breaks */
  }

  /* Loader animation */
  .loader8 {
    font-size: 28px;
    font-weight: bold;
    animation: loader8-animation 3s infinite linear;
    background: linear-gradient(90deg, #8DB600 47%, #0000 0)right/290%;
  }

  .loader8::before {
    content: "Loading...";
    padding: 0 5px;
    color: #0000;
    background: inherit;
    background-clip: text;
    -webkit-background-clip: text;
    background-image: linear-gradient(90deg, #ffffffd8 35%, #000 0);
  }

  @keyframes loader8-animation {
    100% {
      background-position: left;
    }
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    // 1. Get the tips from Jekyll's data file.
    const tips = {{ site.data.tips | jsonify }};

    // 2. Get references to elements.
    const tipContainer = document.getElementById('tip-container');
    const newTipButton = document.getElementById('new-tip-button');

    // 3. Function to display a random tip.
    function displayRandomTip() {
      const randomIndex = Math.floor(Math.random() * tips.length);
      // Use .innerHTML to correctly render any HTML (like links) in the tips.
      tipContainer.innerHTML = tips[randomIndex];
    }

    // 4. Simulate loading, then show first tip.
    setTimeout(() => {
      tipContainer.classList.remove('loader8');
      displayRandomTip();
      newTipButton.disabled = false;
    }, 3500); // change delay if you want longer/shorter "loading..."

    // 5. Enable button click for new tips.
    newTipButton.addEventListener('click', displayRandomTip);
  });
</script>