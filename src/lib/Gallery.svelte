<script>
  import Carousel from "svelte-carousel/src/components/Carousel/Carousel.svelte";
  import galleryImage01 from "../assets/gallery_image-01.jpeg";
  import galleryImage02 from "../assets/gallery_image-02.jpeg";
  import galleryImage03 from "../assets/gallery_image-03.jpeg";
  import galleryImage04 from "../assets/gallery_image-04.jpeg";
  import galleryImage05 from "../assets/gallery_image-05.jpeg";
  import galleryImage06 from "../assets/gallery_image-06.jpeg";
  import galleryImage07 from "../assets/gallery_image-07.jpeg";
  import galleryImage08 from "../assets/gallery_image-08.jpeg";
  import galleryImage09 from "../assets/gallery_image-09.jpeg";
  import galleryImage10 from "../assets/gallery_image-10.jpeg";
  import galleryImage11 from "../assets/gallery_image-11.jpeg";
  import galleryImage12 from "../assets/gallery_image-12.jpeg";
  import galleryImage13 from "../assets/gallery_image-13.jpeg";
  import galleryImage14 from "../assets/gallery_image-14.jpeg";
  import galleryImage15 from "../assets/gallery_image-15.jpeg";
  import galleryImage16 from "../assets/gallery_image-16.jpeg";

  const galleryArr = [
    galleryImage01,
    galleryImage02,
    galleryImage03,
    galleryImage04,
    galleryImage05,
    galleryImage06,
    galleryImage07,
    galleryImage08,
    galleryImage09,
    galleryImage10,
    galleryImage11,
    galleryImage12,
    galleryImage13,
    galleryImage14,
    galleryImage15,
    galleryImage16,
  ];
  let carousel;
</script>

<section id="gallery">
  <h2>Gallery</h2>
  <div class="carousel-wrapper">
    <Carousel
      bind:this={carousel}
      autoplay
      pauseOnFocus
      autoplayDuration={5000}
    >
      {#each galleryArr as image, i}
        <img src={image} alt="Elixir Day Spa Facilities" />
      {/each}
    </Carousel>
  </div>
</section>

<style>
  #gallery {
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

  /* full‑width wrapper with side padding */
  .carousel-wrapper {
    width: 100%;
    box-sizing: border-box;
    padding: 0 1rem;
    text-align: center;
  }

  /* each slide/image */
  .carousel-wrapper img {
    display: block;
    width: 100%;
    height: 720px; /* uniform desktop height */
    object-fit: contain; /* preserves aspect ratio */
    object-position: center;
    margin: 0 auto;
    box-sizing: border-box;
  }

  /* -------------------------------------------------------------------
   Responsive tweaks
   ------------------------------------------------------------------- */
  /* Tablets and small desktops */
  @media (max-width: 768px) {
    #gallery {
      padding: 3rem 1rem;
    }

    h2 {
      font-size: 1.75rem;
    }

    .carousel-wrapper img {
      height: 480px; /* shorter on tablets */
    }
  }

  /* Mobile phones */
  @media (max-width: 480px) {
    #gallery {
      padding: 2rem 0.5rem;
    }

    h2 {
      font-size: 1.5rem;
    }

    .carousel-wrapper img {
      height: 240px; /* even shorter on phones */
    }
  }
</style>
