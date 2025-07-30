<script>
  import dermalogica from "../assets/dermalogica.png";
  import coola from "../assets/coola.png";
  import eltaMd from "../assets/eltamd.png";
  import pinnacle from "../assets/pinnacle.png";

  const imageMap = [
    {
      alt: "Dermalogica",
      image: dermalogica,
    },
    {
      alt: "Coola",
      image: coola,
    },
    {
      alt: "EltaMD",
      image: eltaMd,
    },
    {
      alt: "Pinnacle",
      image: pinnacle,
    },
  ];
</script>

<section id="about">
  <h2>About Us</h2>
  <p>
    Elixir Day Spa is an urban oasis that offers a blend of traditional
    treatments, revolutionary new products and services. At Elixir you will find
    the perfect marriage of hands-on healing techniques mixed with the most
    modern technology to provide the ultimate spa experience. Every treatment
    begins with a free consultation in a private and confidential atmosphere
    culminating in a sense of personal satisfaction and complete well being.
  </p>
  <p>
    With over 20 years of comprehensive experience in providing customer focused
    service in the spa industry backed up by a further eight years
    pharmaceutical and nursing experience, Bilyana is more than qualified to
    meet all your beauty, health and nutrition needs.
  </p>
  <p>
    Born in Macedonia, Bilyana has lived and worked in Barrie for 22 years. She
    loves what she does so much she decided to fulfil her dream of opening a spa
    where her clients weren't just clients—they were friends who left feeling
    pampered and uplifted.
  </p>
  <p>
    The range of services, depth of professional knowledge and meticulous
    attention to detail will leave you with only one problem: what treatment to
    choose first! In 2011, Bilyana's loyal clients collectively voted her
    Barrie's Best Esthetician. Call soon to book an appointment—you will not be
    disappointed!
  </p>
  <h3>I proudly use these products</h3>
  <div class="endorsement-grid">
    {#each imageMap as product}
      <div>
        <img src={product.image} alt={product.alt} />
      </div>
    {/each}
  </div>
</section>

<style>
  /* ─── Container & Typography ───────────────────────────────────────────── */
  #about {
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

  p {
    font-family: "Karla", sans-serif;
    font-size: 1rem;
    line-height: 1.6;
    margin-bottom: 1.5rem;
  }

  /* ─── Subheading ───────────────────────────────────────────────────────── */
  h3 {
    font-size: 1.5rem;
    font-family: "Playfair Display", serif;
    margin-top: 2rem;
    margin-bottom: 1rem;
    position: relative;
    display: inline-block;
    z-index: 1;
  }
  h3::before {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0.2em;
    width: 100%;
    height: 0.4em;
    background: #ff0;
    transform: skew(-10deg);
    z-index: -1;
  }

  /* ─── Endorsement Grid ───────────────────────────────────────────────────── */
  .endorsement-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;
    align-items: center;
    margin-top: 1.5rem;
  }

  .endorsement-grid > div {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .endorsement-grid img {
    max-width: 100%;
    height: auto;
    max-height: 80px;
    object-fit: contain;
    transition: transform 0.3s ease;
  }

  .endorsement-grid img:hover {
    transform: scale(1.05);
  }

  /* ─── Tablet (≤768px) ─────────────────────────────────────────────────── */
  @media (max-width: 768px) {
    #about {
      padding: 3rem 1.5rem;
    }
    h2 {
      font-size: 1.75rem;
    }
    p {
      font-size: 0.95rem;
      margin-bottom: 1.25rem;
    }
    .endorsement-grid {
      grid-template-columns: repeat(2, 1fr);
      gap: 1.5rem;
    }
  }

  /* ─── Phone (≤480px) ──────────────────────────────────────────────────── */
  @media (max-width: 480px) {
    #about {
      padding: 2rem 1rem;
    }
    h2 {
      font-size: 1.5rem;
    }
    p {
      font-size: 0.9rem;
      margin-bottom: 1rem;
    }
    .endorsement-grid {
      grid-template-columns: 1fr;
      gap: 1rem;
    }
  }
</style>
