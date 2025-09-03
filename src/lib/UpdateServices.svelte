<script>
  import { writable } from "svelte/store";
  import Separator from "./Separator.svelte";
  import { firebase } from "../utils/firebase";
  import { get, getDatabase, ref, update } from "firebase/database";
  import { onMount } from "svelte";
  let pricing = writable([]);
  const database = getDatabase(firebase);
  const reference = ref(database, "/pricing");
  let success = false;

  onMount(() => {
    get(reference).then((snapshot) => {
      pricing.set(snapshot.val());
    });
  });

  const submitPrices = () => {
    update(reference, $pricing)
      .then(() => (success = true))
      .finally(() => {
        setTimeout(() => (success = false), 5000);
      });
  };
</script>

{#if $pricing && $pricing.length}
  <section id="services-editor">
    <form on:submit={submitPrices}>
      <!-- Top sticky actions -->
      <div class="actions-top">
        <button class="btn submit" type="submit">
          <span class="highlight">Submit Changes</span>
        </button>
        <span class="hint">All prices are integers.</span>
      </div>

      <h2><span class="highlight">Edit Services & Prices</span></h2>

      {#each $pricing as service, index}
        <h4 id={service.category}>
          {service.category}
        </h4>

        {#if service.subcategories}
          <div class="subcategory-grid">
            {#each service.subcategories as subcategory}
              <div class="subcategory">
                <h5>{subcategory.name}</h5>

                <ul class="svc-list">
                  {#each subcategory.services as svc}
                    <li class="svc-row">
                      <span class="svc-name">{svc.name}</span>

                      <!-- integer price input -->
                      <div class="price-edit">
                        <label
                          class="visually-hidden"
                          for={`price-${service.category}-${subcategory.name}-${svc.name}`}
                          >Price</label
                        >
                        <span class="currency-prefix">$</span>
                        <input
                          id={`price-${service.category}-${subcategory.name}-${svc.name}`}
                          class="price-input"
                          type="number"
                          inputmode="numeric"
                          pattern="\\d*"
                          step="1"
                          min="0"
                          name="price"
                          data-path={`subcategories.${subcategory.name}.services.${svc.name}.price`}
                          placeholder="0"
                          value={svc.price}
                        />
                      </div>
                    </li>
                  {/each}
                </ul>
              </div>
            {/each}
          </div>
        {:else}
          {#if service.description}
            <p class="category-desc">{service.description}</p>
          {/if}

          {#each service.subservices as subservice}
            <div class="subservice">
              <h6 class="subservice-head">
                <span class="subservice-name">{subservice.name}</span>

                <div class="price-edit">
                  <label
                    class="visually-hidden"
                    for={`price-${service.category}-${subservice.name}`}
                    >Price</label
                  >
                  <span class="currency-prefix">$</span>
                  <input
                    id={`price-${service.category}-${subservice.name}`}
                    class="price-input"
                    type="number"
                    inputmode="numeric"
                    pattern="\\d*"
                    step="1"
                    min="0"
                    name="price"
                    data-path={`subservices.${subservice.name}.price`}
                    placeholder="0"
                    value={subservice.price}
                  />
                  {#if subservice.duration}
                    <span class="duration">({subservice.duration})</span>
                  {/if}
                </div>
              </h6>

              {#if subservice.description}
                <p>{subservice.description}</p>
              {/if}

              {#if subservice.options}
                <ul class="options-list">
                  {#each subservice.options as option}
                    <li class="option-row">
                      <span class="option-name">{option.name}</span>
                      <div class="price-edit">
                        <span class="plus">+ $</span>
                        <label
                          class="visually-hidden"
                          for={`opt-${service.category}-${subservice.name}-${option.name}`}
                          >Option Price</label
                        >
                        <input
                          id={`opt-${service.category}-${subservice.name}-${option.name}`}
                          class="price-input"
                          type="number"
                          inputmode="numeric"
                          pattern="\\d*"
                          step="1"
                          min="0"
                          name="option-price"
                          data-path={`subservices.${subservice.name}.options.${option.name}.price`}
                          placeholder="0"
                          value={option.price}
                        />
                      </div>
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

      <!-- Bottom actions -->
      <div class="actions-bottom">
        <button class="btn submit" type="submit">
          <span class="highlight">Submit Changes</span>
        </button>
      </div>
    </form>
  </section>
{/if}

<style>
  /* ───── Container & Base Typography ──────────────────────────────────── */
  #services-editor {
    max-width: 1000px;
    margin: 0 auto;
    padding: 4rem 2rem;
  }

  /* top sticky toolbar */
  .actions-top {
    position: sticky;
    top: 0;
    z-index: 20;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.75rem 0;
    background: linear-gradient(#fff, rgba(255, 255, 255, 0.9));
    backdrop-filter: blur(3px);
    border-bottom: 1px solid #eee;
    margin-bottom: 1rem;
  }
  .actions-bottom {
    display: flex;
    justify-content: flex-end;
    margin-top: 2rem;
  }
  .hint {
    font-family: "Karla", sans-serif;
    font-size: 0.9rem;
    color: #555;
  }

  /* buttons (match site style) */
  .btn {
    color: #e00;
    border: 0;
    font-family: "Playfair Display", serif;
    font-size: 1.05rem;
    background: none;
    cursor: pointer;
    position: relative;
    padding: 0.55rem 1rem;
  }
  .btn .highlight {
    position: relative;
  }
  .btn .highlight::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.5em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
    transition: background 0.2s ease;
  }
  .btn:hover .highlight::before {
    background: #ffe44d;
  }
  .btn.submit {
    color: #1a7f37;
  } /* deep green for “submit” */

  /* headings */
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

  .category-desc {
    font-family: "Karla", sans-serif;
    margin: 0.3rem 0 0.8rem;
  }

  /* lists & rows */
  ul {
    list-style: none;
    padding: 0;
    margin: 0.3rem 0 1rem;
  }
  .svc-list {
    display: grid;
    gap: 0.5rem;
  }
  .svc-row,
  .option-row {
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: center;
    gap: 0.75rem;
    padding: 0.35rem 0;
    border-bottom: 1px dashed #eee;
  }
  .svc-name,
  .option-name {
    font-family: "Karla", sans-serif;
  }

  .subservice {
    margin: 0.75rem 0 1.25rem;
  }
  .subservice-head {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
    margin: 1rem 0 0.3rem;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 0.75rem;
    align-items: center;
  }
  .duration {
    font-family: "Karla", sans-serif;
    margin-left: 0.5rem;
    color: #555;
  }

  /* grid for subcategories */
  .subcategory-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 24px;
    margin-top: 1rem;
  }

  /* price editor */
  .price-edit {
    display: inline-flex;
    align-items: center;
    gap: 0.25rem;
    font-family: "Karla", sans-serif;
    white-space: nowrap;
  }
  .currency-prefix,
  .plus {
    font-weight: 700;
    color: #222;
  }
  .price-input {
    width: 110px;
    max-width: 140px;
    font-family: "Karla", sans-serif;
    font-size: 1rem;
    padding: 8px 10px;
    border: 0;
    border-bottom: 3px solid #ff0;
    background: #fff;
  }
  .price-input:focus {
    outline: none;
    border-color: #e00;
  }

  /* a11y helper */
  .visually-hidden {
    position: absolute !important;
    height: 1px;
    width: 1px;
    overflow: hidden;
    clip: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
    border: 0;
    padding: 0;
    margin: -1px;
  }

  /* ───── Tablet (≤768px) ──────────────────────────────────────────────── */
  @media (max-width: 768px) {
    #services-editor {
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
    .subservice-head {
      grid-template-columns: 1fr;
    }
    .price-input {
      width: 100px;
    }
    .subcategory-grid {
      gap: 16px;
    }
  }

  /* ───── Phone (≤480px) ───────────────────────────────────────────────── */
  @media (max-width: 480px) {
    #services-editor {
      padding: 2rem 1rem;
    }
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
    .price-input {
      width: 90px;
      padding: 6px 8px;
    }
    .actions-top {
      gap: 0.5rem;
    }
    .btn {
      width: 100%;
      text-align: center;
    }
    .actions-bottom {
      justify-content: stretch;
    }
  }
</style>
