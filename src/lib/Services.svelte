<script>
  import Separator from "./Separator.svelte";

  export let pricing;
</script>

{#if $pricing.length}
  <section id="services">
    <h2><span class="highlight">Services</span></h2>
    {#each $pricing as service, index}
      <h4 id={service.category.toLowerCase().replace(" ", "-")}>
        {service.category}
      </h4>
      {#if service.subcategories}
        <div class="subcategory-grid">
          {#each service.subcategories as subcategory}
            <div class="subcategory">
              <h5>{subcategory.name}</h5>
              <ul>
                {#each subcategory.services as service}
                  <li>{service.name}: ${service.price}</li>
                {/each}
              </ul>
            </div>
          {/each}
        </div>
      {:else}
        {#if service.description}
          <p>{service.description}</p>
        {/if}
        {#each service.subservices as subservice}
          <div class="subservice">
            <h6>
              {subservice.name}:
              <span class="price">
                ${subservice.price}
              </span>
              {subservice.duration && `(${subservice.duration})`}
            </h6>
            {#if subservice.description}
              <p>{subservice.description}</p>
            {/if}
            {#if subservice.options}
              <ul>
                {#each subservice.options as option}
                  <li>
                    <span class="option-name">{option.name}</span>: +${option.price}
                  </li>
                {/each}
              </ul>
            {/if}
          </div>
        {/each}
      {/if}
      {#if index < $pricing.length - 1}
        <Separator />
      {/if}
    {/each}
  </section>
{/if}

<style>
  h2 .highlight {
    font-size: 2rem;
    font-family: "Playfair Display", serif;
    margin-bottom: 1rem;
    position: relative;
    display: inline-block;
    z-index: 1;
  }
  h2 .highlight::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.5em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
  }
  h4 {
    font-family: "Rouge Script", cursive;
    font-size: 2rem;
    margin-bottom: 0.1rem;
    position: relative;
    display: inline-block;
    z-index: 1;
  }
  h4::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.5em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
  }
  h5 {
    font-family: "Playfair Display", serif;
    font-size: 1.3rem;
    margin-bottom: 0.2rem;
    margin-top: 0.9rem;
    position: relative;
    display: inline-block;
    z-index: 1;
  }
  h5::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.5em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
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
