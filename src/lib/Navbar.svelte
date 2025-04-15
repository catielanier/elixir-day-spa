<div class="header">
  <nav>
    <ul>
      <a href="#top"><li>Home</li></a>
      <a href="#about"><li>About</li></a>
      <a href="#services"><li>Services</li></a>
      <a href="#gallery"><li>Gallery</li></a>
      <a href="#contact"><li>Contact</li></a>
    </ul>
  </nav>
</div>

<style>
  nav {
    display: block;
    position: fixed;
    top: 15px;
    left: 50%;
    transform: translateX(-50%);
    background: #fff;
    border-radius: 10px;
    border: 1px solid #ffff00;
    padding: 10px 20px;
    color: #000;
    width: 540px;
    font-family: "Playfair Display", serif;
    font-size: 1.2rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }
  nav ul {
    display: flex;
    list-style: none;
    padding: 0;
    margin: 0;
    justify-content: space-around;
  }

  nav ul a {
    display: inline-block;
    position: relative;
    color: #000;
  }

  nav ul a::after {
    content: "";
    position: absolute;
    width: 100%;
    transform: scaleX(0);
    height: 2px;
    bottom: 0;
    left: 0;
    background-color: #ffff00;
    transition: transform 0.25s ease-out;
  }

  nav ul a:hover::after {
    transform: scaleX(1);
    transform-origin: bottom center;
  }
</style>
