<script>
  import { Router, Route } from "svelte-routing";
  import Main from "./lib/Main.svelte";
  import Login from "./lib/Login.svelte";
</script>

<Router>
  <Route path="/"><Main /></Route>
  <Route path="/admin/login"><Login /></Route>
</Router>
