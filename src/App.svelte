<script>
  import Navbar from "./lib/Navbar.svelte";
  import Header from "./lib/Header.svelte";
  import About from "./lib/About.svelte";
</script>

<Navbar />
<Header />
<main>
  <About />
</main>

<style>
  main {
    max-width: 1280px;
    margin: 0 auto;
    padding: 1rem;
    text-align: left;
  }
</style>
