<script>
  import { get, getDatabase, ref } from "firebase/database";
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
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
      {:else}
        {#each service.subservices as subservice}
          <div class="subservice">
            <h6>
              {subservice.name} -
              <span class="price">
                ${subservice.price}
              </span>
              {subservice.duration && `(${subservice.duration})`}
            </h6>
            <p>{subservice.description}</p>
            {#if subservice.options}
              <ul>
                {#each subservice.options as option}
                  <li>
                    <span class="option-name">{option.name}</span> - +${option.price}
                  </li>
                {/each}
              </ul>
            {/if}
          </div>
        {/each}
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
    font-size: 2rem;
    margin-bottom: 0.1rem;
  }
  h5 {
    font-family: "Playfair Display", serif;
    font-size: 1.3rem;
    margin-bottom: 0.2rem;
    margin-top: 0.9rem;
  }
  h6 {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
    margin-bottom: 0.2rem;
    margin-top: 0.9rem;
  }

  h6 .price {
    font-family: "Karla", sans-serif;
  }

  ul,
  p {
    font-family: "Karla", sans-serif;
  }

  p {
    margin-top: 0.3rem;
    margin-bottom: 0.2rem;
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

  .subservice ul {
    padding-left: 20px;
    font-weight: bold;
  }
</style>
