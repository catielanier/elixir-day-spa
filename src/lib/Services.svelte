<script>
  import { onMount } from "svelte";
  import { get, getDatabase, ref } from "firebase/database";
  import { firebase } from "../utils/firebase";
  import { writable } from "svelte/store";

  const pricing = writable([]);

  onMount(() => {
    const database = getDatabase(firebase);
    const reference = ref(database, "/pricing");
    get(reference).then((snapshot) => {
      pricing.set(snapshot.val());
    });
  });
</script>

{#if $pricing.length}
  <section id="services">
    <h2>Services</h2>
    {#each $pricing as service}
      <h4>{service.category}</h4>
      {#if service.subcategories}
        <div class="subcategory-grid">
          {#each service.subcategories as subcategory}
            <div class="subcategory">
              <h5>{subcategory.name}</h5>
              <ul>
                {#each subcategory.services as service}
                  <li>{service.name} - ${service.price}</li>
                {/each}
              </ul>
            </div>
          {/each}
        </div>
      {/if}
    {/each}
  </section>
{/if}

<style>
  h2 {
    font-size: 2rem;
    font-family: "Playfair Display", serif;
    margin-bottom: 1rem;
  }
  h4 {
    font-family: "Rouge Script", cursive;
    font-size: 1.8rem;
  }
  h5 {
    font-family: "Playfair Display", serif;
    font-size: 1.5rem;
  }
  ul {
    font-family: "Karla", sans-serif;
  }

  .subcategory-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 22px;
  }

  ul {
    list-style: none;
    padding: 0;
  }
</style>
