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
                {#each subcategory.services as svc}
                  <li>{svc.name}: ${svc.price}</li>
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
              <span class="price">${subservice.price}</span>
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
        <Separator isMainSectionDivider={false} />
      {/if}
    {/each}
  </section>
{/if}

<style>
  /* ───── Container & Base Typography ──────────────────────────────────── */
  #services {
    max-width: 1000px;
    margin: 0 auto;
    padding: 4rem 2rem;
  }

  /* highlight underlined H2 */
  h2 .highlight {
    font-size: 2rem;
    font-family: "Playfair Display", serif;
    position: relative;
    display: inline-block;
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

  /* category heading */
  h4 {
    font-family: "Rouge Script", cursive;
    font-size: 2rem;
    margin: 2rem 0 0.5rem;
    position: relative;
    display: inline-block;
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

  /* subcategory title */
  h5 {
    font-family: "Playfair Display", serif;
    font-size: 1.3rem;
    margin: 1.5rem 0 0.5rem;
    position: relative;
    display: inline-block;
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

  /* service item */
  h6 {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
    margin: 1rem 0 0.3rem;
  }
  h6 .price {
    font-family: "Karla", sans-serif;
  }

  ul,
  p {
    font-family: "Karla", sans-serif;
  }
  p {
    margin: 0.3rem 0 0.8rem;
  }
  ul {
    list-style: none;
    padding: 0;
    margin: 0.3rem 0 1rem;
  }
  .subservice ul {
    padding-left: 1.25rem;
    font-weight: bold;
  }

  /* grid for subcategories */
  .subcategory-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 24px;
    margin-top: 1rem;
  }

  /* ───── Tablet (≤768px) ──────────────────────────────────────────────── */
  @media (max-width: 768px) {
    #services {
      padding: 3rem 1.5rem;
    }
    h2 .highlight {
      font-size: 1.75rem;
    }
    h4 {
      font-size: 1.6rem;
      margin: 1.5rem 0 0.4rem;
    }
    h5 {
      font-size: 1.15rem;
      margin: 1.25rem 0 0.4rem;
    }
    h6 {
      font-size: 0.9rem;
      margin: 0.8rem 0 0.3rem;
    }
    .subcategory-grid {
      gap: 16px;
    }
  }

  /* ───── Phone (≤480px) ───────────────────────────────────────────────── */
  @media (max-width: 480px) {
    #services {
      padding: 2rem 1rem;
    }
    /* collapse grid to a single column */
    .subcategory-grid {
      display: block;
    }
    .subcategory {
      margin-bottom: 2rem;
    }
    h2 .highlight {
      font-size: 1.5rem;
    }
    h4 {
      font-size: 1.4rem;
    }
    h5 {
      font-size: 1.05rem;
    }
    h6 {
      font-size: 0.85rem;
    }
    p,
    ul {
      font-size: . ninerem;
    }
    ul {
      margin-bottom: 0.8rem;
    }
  }
</style>
