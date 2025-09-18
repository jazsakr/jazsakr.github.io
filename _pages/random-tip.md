---
title: "Random Tip Generator"
permalink: /random-tip/
---

<div class="tip-generator">
  <h2>Here's a random tip for you:</h2>
  <p id="tip-container" class="tip-text">Loading...</p>
  <button id="new-tip-button" class="btn btn--success">Get Another Tip</button>
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
    min-height: 60px; /* Prevents the button from jumping around */
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>

<script>
  // This listener waits for the entire HTML document to be loaded and ready.
  document.addEventListener('DOMContentLoaded', () => {

    // 1. Get the tips from Jekyll's data file.
    const tips = {{ site.data.tips | jsonify }};

    // 2. Get references to the HTML elements.
    const tipContainer = document.getElementById('tip-container');
    const newTipButton = document.getElementById('new-tip-button');

    // 3. A function to pick and display a random tip.
    function displayRandomTip() {
      const randomIndex = Math.floor(Math.random() * tips.length);
      tipContainer.innerHTML = tips[randomIndex];
    }

    // 4. Add the 'click' event listener to the button.
    newTipButton.addEventListener('click', displayRandomTip);

    // 5. Display the first random tip when the page loads.
    setTimeout(displayRandomTip, 3000);
  });
</script>