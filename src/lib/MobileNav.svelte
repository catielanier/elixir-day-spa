<script>
  import { writable } from "svelte/store";
  import { fade } from "svelte/transition";
  import menuIcon from "../assets/menu.png";

  const isOpen = writable(false);
  const toggleOpen = () => isOpen.update((n) => !n);

  // close menu when clicking a nav link
  const navigate = (e) => {
    toggleOpen();
    // let the browser scroll to the anchor…
  };
</script>

<div class="mobile-nav" class:open={$isOpen}>
  {#if !$isOpen}
    <div class="hamburger" on:click={toggleOpen}>
      <img src={menuIcon} alt="Menu" />
    </div>
  {:else}
    <div class="menu-content" transition:fade>
      <button class="close-btn" on:click={toggleOpen}>✕</button>
      <nav>
        <ul class="menu-list">
          <li><a href="#home" on:click={navigate}>Home</a></li>
          <li><a href="#about" on:click={navigate}>About</a></li>
          <li>
            <a href="#hair-removal" on:click={navigate}>Hair Removal</a>
          </li>
          <li><a href="#nails" on:click={navigate}>Nails</a></li>
          <li><a href="#skincare" on:click={navigate}>Skincare</a></li>
          <li><a href="#body" on:click={navigate}>Body</a></li>
          <li><a href="#contact" on:click={navigate}>Contact</a></li>
        </ul>
      </nav>
    </div>
  {/if}
</div>

<style>
  .mobile-nav {
    display: none;
  }

  @media (max-width: 768px) {
    .mobile-nav {
      display: block;
      position: fixed;
      top: 10px;
      left: 15px;
      width: 40px;
      height: 40px;
      overflow: hidden;
      background: rgba(255, 255, 255, 0.9);
      border-radius: 4px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
      transition:
        top 0.3s ease,
        left 0.3s ease,
        right 0.3s ease,
        bottom 0.3s ease,
        width 0.3s ease,
        height 0.3s ease,
        border-radius 0.3s ease;
      z-index: 1000;
    }
    .mobile-nav.open {
      top: 10px;
      left: 15px;
      right: 15px;
      width: auto;
      height: auto;
      border-radius: 8px;
    }

    .hamburger {
      width: 100%;
      height: 100%;
      cursor: pointer;
      z-index: 50;
    }
    .hamburger img {
      display: block;
      width: 100%;
      height: 100%;
    }

    .menu-content {
      display: flex;
      flex-direction: column;
      height: 100%;
      padding: 1rem;
      box-sizing: border-box;
    }

    .close-btn {
      align-self: flex-end;
      background: none;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
      margin-bottom: 1rem;
    }

    nav {
      flex: 1;
      overflow-y: auto;
    }

    .menu-list,
    .menu-list ul {
      list-style: none;
      margin: 0;
      padding: 0;
    }

    .menu-list > li {
      margin: 0.5rem 0;
    }

    .menu-list a {
      text-decoration: none;
      color: #333;
      font-size: 1.2rem;
    }

    .services-label {
      display: inline-block;
      cursor: pointer;
    }

    .submenu {
      padding-left: 1rem;
      margin-top: 0.25rem;
    }

    .submenu li {
      margin: 0.25rem 0;
    }
  }
</style>
