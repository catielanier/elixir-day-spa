<svelte:head>
  <!-- make sure your page actually scales to device-width -->
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<header id="top">
  <div class="hero-text">
    <h1>Elixir Day Spa</h1>
    <h3>Where beauty is an art</h3>
  </div>
</header>

<style>
  /* ───────────────────────────────────────────────────────────────────────── */
  /* global reset and no horizontal scroll */
  :global(html, body) {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
  }

  /* ───────────────────────────────────────────────────────────────────────── */
  header {
    width: 100vw; /* full viewport width */
    height: 100vh;
    position: relative;
    background:
      linear-gradient(
        to bottom,
        rgba(255, 255, 255, 0.5),
        rgba(255, 255, 255, 0.5)
      ),
      url("../assets/hero.jpg") no-repeat center center;
    background-size: cover;
    background-attachment: scroll; /* never fixed on mobile */
  }

  .hero-text {
    position: absolute;
    bottom: 5%;
    left: 15%;
    max-width: 70%; /* keep it from growing too wide */
  }

  .hero-text h1 {
    font-family: "Rouge Script", cursive;
    font-size: 6rem;
    color: #ff0;
    margin: 0;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
  }

  .hero-text h3 {
    font-family: "Playfair Display", serif;
    font-size: 2rem;
    color: #525252;
    margin: 0;
    text-align: right;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.3);
  }

  /* ───────────────────────────────────────────────────────────────────────── */
  /* Large tablets / small desktops */
  @media (max-width: 1024px) {
    .hero-text {
      bottom: 7%;
      left: 12%;
      max-width: 76%;
    }
    .hero-text h1 {
      font-size: 5rem;
    }
    .hero-text h3 {
      font-size: 1.75rem;
    }
  }

  /* ───────────────────────────────────────────────────────────────────────── */
  /* Tablets */
  @media (max-width: 768px) {
    header {
      height: 60vh;
    }
    .hero-text {
      /* center the box */
      bottom: 50%;
      left: 50%;
      transform: translate(-50%, 50%);
      text-align: center;
      max-width: 90%;
    }
    .hero-text h1 {
      font-size: 3.5rem;
    }
    .hero-text h3 {
      font-size: 1.25rem;
    }
  }

  /* ───────────────────────────────────────────────────────────────────────── */
  /* Phones */
  @media (max-width: 480px) {
    header {
      height: 50vh;
    }
    .hero-text {
      bottom: 45%;
      left: 50%;
      transform: translate(-50%, 45%);
      padding: 0 1rem; /* prevent text hugging the very edge */
    }
    .hero-text h1 {
      font-size: 2.5rem;
      line-height: 1.1;
    }
    .hero-text h3 {
      font-size: 1rem;
      line-height: 1.2;
    }
  }
</style>
