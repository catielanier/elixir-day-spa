<script>
  import About from "./lib/About.svelte";
  import Contact from "./lib/Contact.svelte";
  import Footer from "./lib/Footer.svelte";
  import Header from "./lib/Header.svelte";
  import Navbar from "./lib/Navbar.svelte";
  import Services from "./lib/Services.svelte";

  import { get, getDatabase, ref } from "firebase/database";
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import { firebase } from "./utils/firebase";

  const pricing = writable([]);

  onMount(() => {
    const database = getDatabase(firebase);
    const reference = ref(database, "/pricing");
    get(reference).then((snapshot) => {
      pricing.set(snapshot.val());
    });
  });
</script>

<Navbar {pricing} />
<Header />
<main>
  <About />
  <Services {pricing} />
  <Contact />
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
