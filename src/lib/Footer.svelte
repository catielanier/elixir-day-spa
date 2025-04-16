<script>
  const startYear = 2025;
  const currentYear = new Date().getFullYear();
  const copyright =
    startYear === currentYear
      ? `© ${startYear}`
      : `© ${startYear}-${currentYear}`;
</script>

<footer>
  <div>{copyright} Elixir Day Spa. All rights reserved.</div>
  <div>
    Lovingly created by <a href="https://catielanier.ca" target="_blank">
      Catie Lanier
    </a>
  </div>
</footer>

<style>
  footer {
    max-width: 1280px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 1rem;
    padding: 1rem;
  }

  footer div:first-child {
    text-align: left;
  }

  footer div:last-child {
    text-align: right;
  }
</style>
