<script>
  import { Router, Route } from "svelte-routing";
  import Main from "./lib/Main.svelte";
  import Login from "./lib/Login.svelte";
  import Dashboard from "./lib/Dashboard.svelte";
  import TestimonialQueue from "./lib/TestimonialQueue.svelte";
  import UpdateServices from "./lib/UpdateServices.svelte";
  let loggedIn = false;

  const setLogin = () => {
    loggedIn = !loggedIn;
  };
</script>

<Router>
  <Route path="/"><Main /></Route>
  <Route path="/admin/login"><Login {setLogin} /></Route>
  {#if loggedIn}
    <Route path="/admin/dashboard"><Dashboard /></Route>
    <Route path="/admin/testimonials"><TestimonialQueue /></Route>
    <Route path="/admin/prices"><UpdateServices /></Route>
  {/if}
</Router>
