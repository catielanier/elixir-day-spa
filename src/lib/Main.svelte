<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import { get, getDatabase, ref } from "firebase/database";

  import About from "./About.svelte";
  import Contact from "./Contact.svelte";
  import Footer from "./Footer.svelte";
  import Header from "./Header.svelte";
  import Navbar from "./Navbar.svelte";
  import Separator from "./Separator.svelte";
  import Services from "./Services.svelte";
  import Testimonials from "./Testimonials.svelte";
  import Gallery from "./Gallery.svelte";
  import MobileNav from "./MobileNav.svelte";
  import { firebase } from "../utils/firebase";

  const pricing = writable([]);

  onMount(() => {
    const database = getDatabase(firebase);
    const reference = ref(database, "/pricing");
    get(reference).then((snapshot) => {
      pricing.set(snapshot.val());
    });
  });
</script>

<Navbar />
<MobileNav />
<Header />
<main>
  <About />
  <Separator isMainSectionDivider={true} />
  <Services {pricing} />
  <Separator isMainSectionDivider={true} />
  <Testimonials />
  <Separator isMainSectionDivider={true} />
  <Gallery />
  <Separator isMainSectionDivider={true} />
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
