<section id="about">
  <h2>About Us</h2>
  <p>
    With over 15 years of comprehensive experience in providing customer focused
    service in the spa industry backed up by a further eight years
    pharmaceutical and nursing experience, Bilyana is more than qualified to
    meet all your beauty, health and nutrition needs.
  </p>
  <p>
    Born in Macedonia, Bilyana has lived and worked in Barrie for 18 years. She
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
  }
</style>
