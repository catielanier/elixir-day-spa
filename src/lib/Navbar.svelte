<script>
  const subMenu = [
    {
      id: "hair-removal",
      category: "Hair Removal",
    },
    {
      id: "nails",
      category: "Nails",
    },
    {
      id: "skincare",
      category: "Skincare",
    },
    {
      id: "body",
      category: "Body",
    },
  ];
</script>

<div class="header">
  <nav>
    <ul>
      <li><a href="#top">Home</a></li>
      <li><a href="#about">About</a></li>
      <li class="has-submenu">
        <a href="#services">Services</a>
        <ul class="submenu">
          {#each subMenu as item}
            <li>
              <a href={`#${item.id}`}>{item.category}</a>
            </li>
          {/each}
        </ul>
      </li>
      <li><a href="#testimonials">Testimonials</a></li>
      <li><a href="#gallery">Gallery</a></li>
      <li><a href="#contact">Contact</a></li>
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
    width: 680px;
    font-family: "Playfair Display", serif;
    font-size: 1.2rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    z-index: 99;
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

  nav ul li {
    position: relative;
  }

  nav ul li a {
    display: inline-block;
    position: relative;
    padding: 5px 10px;
    color: #000;
    text-decoration: none;
  }

  nav ul li a::after {
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

  nav ul li a:hover::after {
    transform: scaleX(1);
    transform-origin: bottom center;
  }

  .has-submenu .submenu {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    background: #fff;
    list-style: none;
    margin: 0;
    padding: 0.5rem 0;
    border: 1px solid #ddd;
    border-radius: 4px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    white-space: nowrap;
  }

  .has-submenu:hover .submenu {
    display: block;
  }

  .has-submenu .submenu li a {
    display: block;
    padding: 0.5rem 1.5rem;
  }

  .has-submenu .submenu li a:hover {
    background: #f4f4f4;
  }

  @media (max-width: 768px) {
    .header {
      display: none;
    }
  }
</style>
