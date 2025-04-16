<script>
  import Navbar from "./lib/Navbar.svelte";
  import Header from "./lib/Header.svelte";
  import About from "./lib/About.svelte";
  import Services from "./lib/Services.svelte";
  import Footer from "./lib/Footer.svelte";
</script>

<Navbar />
<Header />
<main>
  <About />
  <Services />
</main>
<Footer />

<style>
  main {
    max-width: 1280px;
    margin: 0 auto;
    padding: 1rem;
    text-align: left;
  }
</style>
