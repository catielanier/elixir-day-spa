<script>
  import { Router, Route } from "svelte-routing";
  import Main from "./lib/Main.svelte";
</script>

<Router>
  <Route path="/"><Main /></Route>
</Router>
