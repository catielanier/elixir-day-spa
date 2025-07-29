<script>
  import Carousel from "svelte-carousel/src/components/Carousel/Carousel.svelte";

  const testimonials = [
    {
      url: "https://maps.app.goo.gl/F9AksQbvvu3Ru8sF7",
      sourceName: "Nina Downs",
      paragraphs: [
        "I always look forward to visiting Bilyana at Elixir Day Spa. Her facility is spotlessly, clean and comfortable. She never makes me feel rushed and she does meticulous work. I enjoy her company and our conversations during the service time.",
        "Elixir spa was recommended to me by a friend a couple of years ago and I’m always  pleased and would not change to another provider.",
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

  let carousel;
</script>

<section id="testimonials">
  <h2>Testimonials</h2>
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
              — <a
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
</section>

<style>
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

  /* make the carousel wrapper full width and add side padding */
  .carousel-wrapper {
    width: 100%;
    box-sizing: border-box;
    padding: 0 1rem;
  }

  /* ensure each slide fills its container */
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

  /* blockquote styling */
  .testimonial-slide blockquote {
    margin: 0;
    font-family: "Karla", sans-serif;
    padding: 1.5rem;
    border-left: 4px solid #ddd;
    background: #f9f9f9;
    quotes: "“" "”" "‘" "’";
  }

  /* paragraph spacing */
  .testimonial-slide blockquote p {
    margin: 0 0 1rem;
  }

  /* footer attribution */
  .testimonial-slide blockquote footer {
    margin-top: 1rem;
    text-align: right;
    font-style: italic;
    font-family: "Playfair Display", serif;
  }

  .testimonial-slide blockquote footer a,
  .view-more a {
    position: relative; /* establish local stacking context */
    z-index: 0; /* any non‑auto z‑index works; 0 is enough */
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
    z-index: -1; /* sits _behind_ the link text */
    pointer-events: none; /* lets clicks pass through to the <a> */
  }

  /* -------------------------------------------------------------------
   Responsive tweaks
   ------------------------------------------------------------------- */
  /* Tablets and small desktops */
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

    .testimonial-slide blockquote p {
      font-size: 0.95rem;
    }

    .testimonial-slide blockquote footer {
      font-size: 0.9rem;
    }
  }

  /* Mobile phones */
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

    .testimonial-slide blockquote p {
      font-size: 0.9rem;
      margin-bottom: 0.75rem;
    }

    .testimonial-slide blockquote footer {
      font-size: 0.85rem;
    }
  }
</style>
