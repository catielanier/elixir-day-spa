<script>
  import { getDatabase, push, ref } from "firebase/database";
  import Carousel from "svelte-carousel/src/components/Carousel/Carousel.svelte";
  import { firebase } from "../utils/firebase";

  let isModalOpen = false;
  let success = false;
  let sourceName = "";
  let testimonial = "";
  const database = getDatabase(firebase);
  const referenceTestimonials = ref(database, "/testimonials");

  const testimonials = [
    {
      url: "https://maps.app.goo.gl/F9AksQbvvu3Ru8sF7",
      sourceName: "Nina Downs",
      paragraphs: [
        "I always look forward to visiting Bilyana at Elixir Day Spa. Her facility is spotlessly, clean and comfortable. She never makes me feel rushed and she does meticulous work. I enjoy her company and our conversations during the service time.",
        "Elixir spa was recommended to me by a friend a couple of years ago and I'm always  pleased and would not change to another provider.",
      ],
    },
    {
      url: "https://maps.app.goo.gl/BvoFzzpGiDwuZKei7",
      sourceName: "Upali Choden",
      paragraphs: [
        "Bilyana was so professional and welcoming. I simply loved her service. She perfectly did my eyebrows. She takes her time and does her work fabulously.",
        "Also, her space is so clean and neat and I felt so comfortable.",
        "Thank you so much for your service.",
      ],
    },
    {
      url: "https://maps.app.goo.gl/DVA4Tq5R9k4Bngka7",
      sourceName: "China Westcott",
      paragraphs: [
        "Bilyana is incredible! I have been to many places for waxing and she is by far the best! She makes you feel so comfortable and safe and her waxing is next level, she is fast and there is little to no pain she is amazing at what she does. She pays great attention to detail and truly is the best! I will never go anywhere else.",
      ],
    },
    {
      url: "https://maps.app.goo.gl/jb79a22FfKx5RkjY7",
      sourceName: "Jillian Wilson",
      paragraphs: [
        "Elixir Day Spa has been my go-to spot for years now! Bilyana is super kind and welcoming, and explains the process of the treatment. She always goes above and beyond and has truly given me so much confidence through every appointment.",
      ],
    },
    {
      url: "https://maps.app.goo.gl/XVKrjYRN84dgXDM98",
      sourceName: "Jennifer van Tol",
      paragraphs: [
        "Bilyana offers absolute professional services.   She takes time with each client to ensure complete satisfaction.",
        "I trust her with my skin.  That says a lot.",
        "I have been going to Elixir for over 5 years and have now stared bringing my teenage sons.",
        "We love Bilyana!!!!",
      ],
    },
    {
      url: "https://maps.app.goo.gl/Y6uKGQzaKK3m3eh66",
      sourceName: "Camille Romero",
      paragraphs: [
        "Elixir Day Spa offers a range of professional treatments and caters to diverse needs. I visit primarily for the facials which always leave my skin looking and feeling refreshed and radiant. Hands down best place ever.",
        "Bilyana utilizes the latest techniques and high-quality products to deliver exceptional results. Whether you are looking for a deep cleansing facial, anti-aging treatment, or a relaxing and pampering experience, Bilyana has you covered! I highly recommend!",
      ],
    },
    {
      url: "https://maps.app.goo.gl/m2fMYgEfVXPj4RkW9",
      sourceName: "Jacob Proctor",
      paragraphs: [
        "I recently was fortunate enough to experience my first facial with Bilyana. I am a 24 year-old male who has been dealing with ongoing acne since I was probably around 19 years old and in university. I am pretty self conscious about my skin and I really wanted to find a solution to my breakouts.",
        "I've been on a journey ever since to maintain my skin care, eating, and have seen numerous esthetician’s, but I can say with sincerity that Bilyana is among the best. Not second best, but THE best. You can tell she cares by the time she takes to discuss your skins history,  describing how the products she uses function, and by her knowledge.",
        "It was evident to see Bilyana's passion towards her work and commitment towards her clients. She is great at recommending products but did not make it feel like I have felt, where I need to make a purchase. All in all it was a truly great experience and I look forward to seeing Bilyana again soon.",
      ],
    },
    {
      url: "https://maps.app.goo.gl/WdszTF13XHd3Geyu6",
      sourceName: "Candace Campbell",
      paragraphs: [
        "Bilyana is extremely knowledgeable and professional and has a beautiful, clean space. Highly recommend for facials, waxing and spray tans.",
      ],
    },
  ];

  const toggleModal = () => (isModalOpen = !isModalOpen);

  let carousel;

  const submitTestimonial = () => {
    const newTestimonial = {
      sourceName,
      testimonial,
    };
    const referenceQueue = ref(database, "/queue");
    push(referenceQueue, newTestimonial)
      .then(() => {
        success = true;
        toggleModal();
      })
      .finally(() => {
        setTimeout(() => {
          success = false;
        }, 5000);
      });
  };
</script>

<section id="testimonials">
  <h2>Testimonials</h2>

  <!-- write-a-testimonial CTA -->
  <div class="testimonial-cta">
    <button class="btn open-modal" on:click={toggleModal}>
      <span class="highlight">Write a testimonial</span>
    </button>
  </div>

  <!-- Success toast (toggle visibility in logic) -->
  {#if success}
    <p class="success">Thank you! Your testimonial has been submitted.</p>
  {/if}

  <div class="carousel-wrapper">
    <Carousel
      bind:this={carousel}
      autoplay
      pauseOnFocus
      autoplayDuration={8000}
    >
      {#each testimonials as testimonial}
        <div class="testimonial-slide">
          <blockquote>
            {#each testimonial.paragraphs as paragraph}
              <p>{paragraph}</p>
            {/each}
            <footer>
              — <a
                href={testimonial.url}
                target="_blank"
                rel="noopener noreferrer"
              >
                {testimonial.sourceName}
              </a>
            </footer>
          </blockquote>
        </div>
      {/each}
    </Carousel>
  </div>

  <div class="view-more">
    <a
      href="https://maps.app.goo.gl/26iH3T4HWR4YhrSd7"
      target="_blank"
      rel="noopener noreferrer"
    >
      View all my Google Maps reviews
    </a>
  </div>

  <!-- Modal (add/remove .open class in your logic to show/hide) -->
  <div class="modal" id="testimonial-modal" aria-hidden="true">
    <div class="modal__overlay" data-close></div>

    <div
      class="modal__dialog"
      role="dialog"
      aria-modal="true"
      aria-labelledby="testimonial-modal-title"
    >
      <button
        class="modal__close"
        type="button"
        on:click={toggleModal}
        aria-label="Close"
        data-close
      >
        &times;
      </button>

      <h3 id="testimonial-modal-title">Share your experience</h3>
      <p class="modal__subtitle">Tell us about your visit.</p>

      <form class="testimonial-form">
        <div>
          <input
            type="text"
            name="sourceName"
            required
            placeholder="Your name"
            autocomplete="name"
          />
        </div>

        <div>
          <textarea name="text" required placeholder="Your testimonial"
          ></textarea>
        </div>

        <div class="btn-wrap">
          <button type="submit" class="btn submit">
            <span class="highlight">Submit testimonial</span>
          </button>
        </div>
      </form>
    </div>
  </div>
</section>

<style>
  /* ---------- existing styles (unchanged) ---------- */
  #testimonials {
    max-width: 1000px;
    margin: 0 auto;
    padding: 4rem 2rem;
  }

  h2 {
    font-size: 2rem;
    font-family: "Playfair Display", serif;
    margin-bottom: 1rem;
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

  .carousel-wrapper {
    width: 100%;
    box-sizing: border-box;
    padding: 0 1rem;
  }

  .carousel-wrapper :global(.testimonial-slide) {
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
    padding: 1.5rem;
    background: #fff;
    border-radius: 0.5rem;
    text-align: left;
    box-sizing: border-box;
  }

  .testimonial-slide blockquote {
    margin: 0;
    font-family: "Karla", sans-serif;
    padding: 1.5rem;
    border-left: 4px solid #ddd;
    background: #f9f9f9;
    quotes: "“" "”" "‘" "’";
  }

  .testimonial-slide blockquote p {
    margin: 0 0 1rem;
  }

  .testimonial-slide blockquote footer {
    margin-top: 1rem;
    text-align: right;
    font-style: italic;
    font-family: "Playfair Display", serif;
  }

  .testimonial-slide blockquote footer a,
  .view-more a {
    position: relative;
    z-index: 0;
    color: #e00;
    text-decoration: none;
    display: inline-block;
  }

  .view-more {
    margin-top: 2rem;
    text-align: right;
    font-family: "Playfair Display", serif;
  }

  .testimonial-slide blockquote footer a::before,
  .view-more a::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.15em;
    width: 100%;
    height: 0.5em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
    pointer-events: none;
  }

  /* ---------- CTA button (matches site buttons) ---------- */
  .testimonial-cta {
    margin: 0 0 1.25rem;
    text-align: right;
  }
  .btn {
    color: #e00;
    border: 0;
    font-family: "Playfair Display", serif;
    font-size: 1.05rem;
    background: none;
    cursor: pointer;
    position: relative;
    padding: 0.5rem 1rem;
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

  /* ---------- Modal ---------- */
  .modal {
    position: fixed;
    inset: 0;
    display: none; /* hidden by default; add .open to show */
    align-items: center;
    justify-content: center;
    padding: 1rem;
    z-index: 1000;
  }
  .modal.open {
    display: flex;
  }

  .modal__overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.45);
    backdrop-filter: blur(2px);
  }

  .modal__dialog {
    position: relative;
    width: 100%;
    max-width: 640px;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.25);
    padding: 1.25rem 1.25rem 1rem;
    z-index: 1;
  }

  .modal__close {
    position: absolute;
    top: 0.6rem;
    right: 0.6rem;
    border: 0;
    background: none;
    font-size: 1.75rem;
    line-height: 1;
    color: #222;
    cursor: pointer;
  }
  .modal__close:focus {
    outline: 2px solid #e00;
    outline-offset: 2px;
  }

  .modal h3 {
    font-family: "Playfair Display", serif;
    font-size: 1.5rem;
    margin: 0 0 0.5rem;
    position: relative;
    display: inline-block;
  }
  .modal h3::before {
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

  .modal__subtitle {
    margin: 0 0 1rem;
    font-family: "Karla", sans-serif;
    color: #444;
  }

  .testimonial-form {
    margin-top: 0.5rem;
  }

  .testimonial-form input,
  .testimonial-form textarea {
    width: 100%;
    font-family: "Karla", sans-serif;
    font-size: 1.05rem;
    padding: 10px 14px;
    border: 0;
    border-bottom: 3px solid #ff0;
    margin-bottom: 1rem;
    resize: vertical;
    background: #fff;
  }
  .testimonial-form textarea {
    min-height: 140px;
  }
  .testimonial-form input::placeholder,
  .testimonial-form textarea::placeholder {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
  }
  .testimonial-form input:focus,
  .testimonial-form textarea:focus {
    outline: none;
    border-color: #e00;
  }

  .testimonial-form .btn-wrap {
    display: flex;
    justify-content: flex-end;
  }
  .btn.submit {
    color: #1a7f37;
  } /* deep green accent for submit */

  .success {
    font-family: "Karla", sans-serif;
    color: #1a7f37; /* deep green */
    background: #e7f9ed; /* soft green background */
    border: 1px solid #b6e2c1;
    padding: 0.75rem 1rem;
    margin: 0 0 1rem;
    border-radius: 6px;
    font-size: 1rem;
    text-align: center;
    animation: fadeIn 0.4s ease-out;
  }

  /* little fade-in animation */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(-6px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  /* ---------- Responsive ---------- */
  @media (max-width: 768px) {
    #testimonials {
      padding: 3rem 1rem;
    }
    h2 {
      font-size: 1.75rem;
    }

    .testimonial-slide blockquote {
      padding: 1rem;
      border-left-width: 3px;
    }

    .modal__dialog {
      padding: 1rem;
      max-width: 560px;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 1.5rem;
    }

    .testimonial-slide {
      padding: 1rem;
    }
    .testimonial-slide blockquote {
      padding: 0.75rem;
      border-left-width: 2px;
    }

    .modal__dialog {
      padding: 0.9rem;
    }
    .testimonial-form input,
    .testimonial-form textarea {
      font-size: 0.95rem;
      padding: 8px 10px;
    }
    .btn {
      font-size: 1rem;
      width: 100%;
      text-align: center;
    }
  }
</style>
