<script>
  import { links } from "svelte-routing";
</script>

<h2>Admin Dashboard</h2>
<ul use:links>
  <li><a href="/admin/testimonials">Approve Testimonials</a></li>
  <li><a href="/admin/pricing">Updating Pricing and Items</a></li>
</ul>
