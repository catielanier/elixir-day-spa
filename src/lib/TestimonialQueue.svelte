<script>
  import { onMount } from "svelte";
  import { firebase } from "../utils/firebase";
  import {
    child,
    get,
    getDatabase,
    push,
    ref,
    remove,
  } from "firebase/database";

  const database = getDatabase(firebase);
  const referenceQueue = ref(database, "/queue");
  const referenceTestimonials = ref(database, "/testimonials");

  let queue = {};

  onMount(() => {
    get(referenceQueue).then((snapshot) => {
      queue = snapshot.val() ?? {};
    });
  });

  // Normalize any queued item to { sourceName, paragraphs: string[] }
  const toApprovedShape = (q) => {
    const sourceName = q?.sourceName ?? "";

    // prefer paragraphs if already present
    if (Array.isArray(q?.paragraphs) && q.paragraphs.length) {
      return { sourceName, paragraphs: q.paragraphs };
    }

    // fall back to a single text field (could be 'text' or 'testimonial')
    const raw =
      typeof q?.text === "string"
        ? q.text
        : typeof q?.testimonial === "string"
          ? q.testimonial
          : "";

    const paragraphs = raw
      .replace(/\r\n/g, "\n") // normalize CRLF → LF
      .trim()
      .split(/\n{2,}/) // split on blank lines into paragraphs
      .filter((p) => p.trim().length > 0);

    // if nothing after split, at least pass one paragraph (empty string stripped above)
    return {
      sourceName,
      paragraphs: paragraphs.length ? paragraphs : [raw.trim()],
    };
  };

  const approveTestimonial = (refKey) => {
    const queued = queue[refKey];
    if (!queued) return;

    const approvedDoc = toApprovedShape(queued);

    push(referenceTestimonials, approvedDoc)
      .then(() => {
        const queueItem = child(referenceQueue, refKey);
        return remove(queueItem);
      })
      .finally(() => {
        // optimistic UI update
        delete queue[refKey];
        // trigger reactivity
        queue = { ...queue };
      });
  };

  const rejectTestimonial = (refKey) => {
    const childItem = child(referenceQueue, refKey);
    remove(childItem).finally(() => {
      delete queue[refKey];
      queue = { ...queue };
    });
  };
</script>

<section id="testimonial-admin" class="testimonial-admin">
  <h2>Approve/Reject Testimonials</h2>

  {#if queue && Object.keys(queue).length > 0}
    <div class="queue-grid">
      {#each Object.entries(queue) as [ref, item]}
        <article class="testimonial-card">
          <header class="card-head">
            <span class="label">Name</span>
            <p class="value">{item.sourceName}</p>
          </header>

          <div class="card-body">
            <span class="label">Testimonial</span>

            {#if Array.isArray(item.paragraphs) && item.paragraphs.length}
              <div class="paragraphs">
                {#each item.paragraphs as p}
                  <p class="paragraph">{p}</p>
                {/each}
              </div>
            {:else}
              <!-- fall back to a single string; preserve line breaks visually -->
              <p class="testimonial-text">
                {item.text ?? item.testimonial ?? ""}
              </p>
            {/if}
          </div>

          <div class="actions btn-wrap">
            <button
              class="btn approve"
              on:click={() => approveTestimonial(ref)}
            >
              <span class="highlight">Approve</span>
            </button>

            <button class="btn reject" on:click={() => rejectTestimonial(ref)}>
              <span class="highlight">Reject</span>
            </button>
          </div>
        </article>
      {/each}
    </div>
  {:else}
    <p class="muted">Loading queue…</p>
  {/if}
</section>

<style>
  /* ─── section layout ──────────────────────────────────────────────────── */
  #testimonial-admin {
    padding: 4rem 2rem;
    max-width: 1000px;
    margin: 0 auto;
  }

  h2 {
    font-size: 2rem;
    font-family: "Playfair Display", serif;
    margin-bottom: 1.25rem;
    position: relative;
    display: inline-block;
    z-index: 1;
  }
  h2::before {
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

  .muted {
    font-family: "Karla", sans-serif;
    color: #555;
    margin-top: 1rem;
  }

  /* ─── grid of pending testimonials ────────────────────────────────────── */
  .queue-grid {
    margin-top: 2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.25rem;
  }

  /* ─── cards ───────────────────────────────────────────────────────────── */
  .testimonial-card {
    border: 1px solid #eee;
    border-radius: 10px;
    padding: 1rem 1rem 0.75rem;
    background: #fff;
    box-shadow: 0 6px 18px rgba(0, 0, 0, 0.06);
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .card-head,
  .card-body {
    display: grid;
    grid-template-columns: 100px 1fr;
    gap: 0.5rem 1rem;
    align-items: start;
  }

  .label {
    font-family: "Playfair Display", serif;
    font-size: 0.95rem;
    color: #222;
    position: relative;
    display: inline-block;
  }
  .label::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.45em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
  }

  .value,
  .testimonial-text {
    font-family: "Karla", sans-serif;
    margin: 0;
    color: #222;
    line-height: 1.5;
  }

  /* preserves single line breaks when showing a raw string */
  .testimonial-text {
    white-space: pre-wrap;
    word-wrap: break-word;
  }

  /* nice spacing for array paragraphs */
  .paragraphs {
    display: grid;
    gap: 0.75rem;
  }
  .paragraphs .paragraph {
    margin: 0;
    font-family: "Karla", sans-serif;
    line-height: 1.5;
  }

  /* ─── actions / buttons ───────────────────────────────────────────────── */
  .btn-wrap {
    display: flex;
    gap: 0.75rem;
    margin-top: 0.5rem;
    flex-wrap: wrap;
  }

  .btn {
    color: #e00;
    border: 0;
    font-family: "Playfair Display", serif;
    font-size: 1rem;
    background: none;
    cursor: pointer;
    position: relative;
    padding: 0.45rem 0.9rem;
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

  .btn.approve {
    color: #1a7f37;
  } /* deep green */
  .btn.reject {
    color: #b00020;
  } /* deep red */

  .btn:focus {
    outline: none;
    text-decoration: underline;
    text-underline-offset: 4px;
  }
  .btn:hover .highlight::before {
    background: #ffe44d;
  }

  /* ─── responsive tweaks ───────────────────────────────────────────────── */
  @media (max-width: 768px) {
    #testimonial-admin {
      padding: 3rem 1.5rem;
    }
    h2 {
      font-size: 1.75rem;
    }
    .queue-grid {
      gap: 1rem;
    }
    .card-head,
    .card-body {
      grid-template-columns: 90px 1fr;
    }
    .btn {
      font-size: 0.95rem;
      padding: 0.4rem 0.8rem;
    }
  }

  @media (max-width: 480px) {
    #testimonial-admin {
      padding: 2rem 1rem;
    }
    h2 {
      font-size: 1.5rem;
    }
    .card-head,
    .card-body {
      grid-template-columns: 1fr;
    }
    .label {
      margin-bottom: 0.25rem;
      width: max-content;
    }
    .btn-wrap {
      width: 100%;
    }
    .btn {
      display: inline-block;
      width: auto;
    }
  }
</style>
