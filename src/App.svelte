<script>
  import { Router, Route } from "svelte-routing";
  import Main from "./lib/Main.svelte";
  import Login from "./lib/Login.svelte";
  import Dashboard from "./lib/Dashboard.svelte";
  import TestimonialQueue from "./lib/TestimonialQueue.svelte";
  import AddItems from "./lib/AddItems.svelte";
</script>

<Router>
  <Route path="/"><Main /></Route>
  <Route path="/admin/login"><Login /></Route>
  <Route path="/admin/dashboard"><Dashboard /></Route>
  <Route path="/admin/testimonials"><TestimonialQueue /></Route>
  <Route path="/admin/prices"><AddItems /></Route>
</Router>
