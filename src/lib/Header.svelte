<header id="top">
  <div>
    <h1>Elixir Day Spa</h1>
    <h3>Where beauty is an art</h3>
  </div>
</header>

<style>
  header {
    max-width: 1920px;
    width: 100%;
    height: 100vh;
    background:
      linear-gradient(
        to bottom,
        rgba(255, 255, 255, 0.5),
        rgba(255, 255, 255, 0.5)
      ),
      url("../assets/hero.jpg") no-repeat center center fixed;
    background-size: cover;
  }

  header div {
    position: absolute;
    bottom: 5%;
    left: 15%;
  }

  header div h1 {
    font-family: "Rouge Script", cursive;
    font-size: 6rem;
    color: #ff0;
    margin: 0;
    text-align: left;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
  }

  header div h3 {
    font-family: "Playfair Display", serif;
    font-size: 2rem;
    color: #525252;
    margin: 0;
    text-align: right;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.3);
  }
</style>
