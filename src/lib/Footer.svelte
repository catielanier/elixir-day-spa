<script>
  const startYear = 2025;
  const currentYear = new Date().getFullYear();
  const copyright =
    startYear === currentYear
      ? `© ${startYear}`
      : `© ${startYear}-${currentYear}`;
</script>

<footer>
  <div class="container">
    <div>{copyright} Elixir Day Spa. All rights reserved.</div>
    <div>
      Lovingly created by <a href="https://catielanier.ca" target="_blank">
        Catie Lanier
      </a>
    </div>
  </div>
</footer>

<style>
  footer {
    font-family: "Rouge Script", cursive;
    font-weight: bold;
    font-size: 1.2rem;
    background: #525252;
    color: #ff0;
  }

  .container {
    max-width: 1280px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    padding: 1rem 2rem;
  }

  a {
    color: #fff;
  }

  /* left + right alignment on desktop */
  .container > div:first-child {
    text-align: left;
  }
  .container > div:last-child {
    text-align: right;
  }

  /* ─── Tablet (≤768px): single column, centered ─────────────────────── */
  @media (max-width: 768px) {
    .container {
      grid-template-columns: 1fr;
      text-align: center;
      padding: 1rem 1.5rem;
    }
    .container > div {
      margin-bottom: 0.5rem;
    }
  }

  /* ─── Phone (≤480px): smaller text & tighter padding ───────────────── */
  @media (max-width: 480px) {
    footer {
      font-size: 1rem;
    }
    .container {
      padding: 0.75rem 1rem;
      gap: 0.5rem;
    }
  }
</style>
