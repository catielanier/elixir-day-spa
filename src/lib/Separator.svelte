<script>
  export let isMainSectionDivider;
</script>

<div class={isMainSectionDivider ? 'main-divider' : ''}>
  <svg
    viewBox="0 0 1200 20"
    xmlns="http://www.w3.org/2000/svg"
    aria-hidden="true"
  >
    <path
      d="M0,10 C150,0 350,20 600,10 S1050,0 1200,10"
      stroke="#FFFF00"
      stroke-width="2"
      fill="none"
    />
  </svg>
</div>

<style>
  svg {
    margin-top: 1.3rem;
  }
  div {
    max-width:1000px;
    margin: 0 auto;
  }
  div.main-divider {
    padding: 0 2rem;
  }
</style>
