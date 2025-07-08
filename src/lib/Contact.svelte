<script>
  import axios from "axios";

  // FontAwesome setup
  import { library } from "@fortawesome/fontawesome-svg-core";
  import { faFacebookF, faInstagram } from "@fortawesome/free-brands-svg-icons";
  import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";

  // add the icons to the library
  library.add(faFacebookF, faInstagram);

  let [contactName, email, phone, message] = Array(4).fill("");
  let success = false;

  const sendMessage = () => {
    axios
      .post(
        "https://formcarry.com/s/pZ2B97h0FXh",
        { contactName, email, phone, message },
        { headers: { Accept: "application/json" } }
      )
      .then((_) => {
        success = true;
        setTimeout(() => {
          success = false;
        }, 5000);
      })
      .catch((err) => {
        console.error(err);
      });
  };
</script>

<svelte:head>
  <!-- meta for responsive -->
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<section id="contact">
  <h2>Contact Us</h2>
  <p>
    Have a question about a treatment or ready to book your appointment? I'd
    love to hear from you!
  </p>
  <p>
    Give me a call or text message at
    <a href="tel:+1-705-770-9936">(705) 770-9936</a>
    to chat directly—I'm happy to help you choose the right service or find a time
    that works for you.
  </p>
  <p>
    Prefer to email instead? Just fill out the contact form, and I'll get back
    to you personally as soon as I can.
  </p>

  <div class="form-wrapper">
    <form on:submit|preventDefault={sendMessage}>
      {#if success}
        <p class="success">Your email was successfully sent!</p>
      {/if}
      <div>
        <input
          type="text"
          name="name"
          bind:value={contactName}
          required
          placeholder="Your name"
        />
      </div>
      <div>
        <input
          type="email"
          name="email"
          bind:value={email}
          required
          placeholder="Email address"
        />
      </div>
      <div>
        <input
          type="text"
          name="phone"
          bind:value={phone}
          required
          placeholder="Phone number"
        />
      </div>
      <div>
        <textarea
          placeholder="Your message"
          name="message"
          bind:value={message}
          required
        />
      </div>
      <div class="btn-wrap">
        <button type="submit"><span class="highlight">Send email</span></button>
      </div>
    </form>
  </div>

  <!-- social links -->
  <div class="social-media">
    <span>Follow us:</span>
    <a
      href="https://www.facebook.com/yourpage"
      target="_blank"
      rel="noopener"
      aria-label="Facebook"
    >
      <FontAwesomeIcon icon={faFacebookF} size="2x" />
    </a>
    <a
      href="https://www.instagram.com/youraccount"
      target="_blank"
      rel="noopener"
      aria-label="Instagram"
    >
      <FontAwesomeIcon icon={faInstagram} size="2x" />
    </a>
  </div>
</section>

<style>
  /* ─── global reset & box-sizing ───────────────────────────────────────── */
  :global(html, body) {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
    box-sizing: border-box;
  }
  :global(*),
  :global(*::before),
  :global(*::after) {
    box-sizing: inherit;
  }

  /* ─── section layout ──────────────────────────────────────────────────── */
  #contact {
    padding: 4rem 2rem;
    max-width: 1000px;
    margin: 0 auto;
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
    line-height: 1.5;
    margin-bottom: 1rem;
  }

  a {
    position: relative;
    display: inline-block;
    color: #e00;
    text-decoration: none;
  }
  a::before {
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

  .form-wrapper {
    margin-top: 2rem;
  }
  form {
    max-width: 540px;
    width: 100%;
  }
  .success {
    color: green;
    margin-bottom: 1rem;
  }

  input,
  textarea {
    width: 100%;
    font-family: "Karla", sans-serif;
    font-size: 1.2rem;
    padding: 10px 15px;
    border: 0;
    border-bottom: 3px solid #ff0;
    margin-bottom: 1rem;
    resize: vertical;
  }
  textarea {
    min-height: 150px;
  }
  input::placeholder,
  textarea::placeholder {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
  }
  input:focus,
  textarea:focus {
    outline: none;
    border-color: #e00;
  }

  .btn-wrap {
    position: relative;
  }
  button {
    color: #e00;
    border: 0;
    font-family: "Playfair Display", serif;
    font-size: 1.1rem;
    background: none;
    cursor: pointer;
    position: relative;
    padding: 0.5rem 1rem;
  }
  button .highlight {
    position: relative;
  }
  button .highlight::before {
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

  /* ─── social media icons ───────────────────────────────────────────────── */
  .social-media {
    margin-top: 2rem;
    display: flex;
    align-items: center;
    gap: 1rem;
    font-family: "Karla", sans-serif;
  }
  .social-media span {
    font-size: 1.1rem;
  }
  .social-media a :global(svg) {
    /* let size="2x" handle dimensions */
    vertical-align: middle;
  }
  .social-media a:hover :global(svg) {
    color: #ff0;
  }

  /* ─── tablet breakpoint ───────────────────────────────────────────────── */
  @media (max-width: 768px) {
    #contact {
      padding: 3rem 1.5rem;
    }
    h2 {
      font-size: 1.75rem;
    }
    p {
      font-size: 1rem;
    }
    input,
    textarea {
      font-size: 1rem;
      padding: 8px 12px;
    }
    button {
      font-size: 1rem;
      padding: 0.5rem 0.75rem;
    }
    .social-media span {
      font-size: 1rem;
    }
  }

  /* ─── phone breakpoint ─────────────────────────────────────────────────── */
  @media (max-width: 480px) {
    #contact {
      padding: 2rem 1rem;
    }
    h2 {
      font-size: 1.5rem;
    }
    p {
      font-size: 0.9rem;
    }
    input,
    textarea {
      font-size: 0.9rem;
      padding: 6px 10px;
    }
    textarea {
      min-height: 120px;
    }
    button {
      display: block;
      width: 100%;
      text-align: center;
    }
    .social-media {
      justify-content: center;
    }
    .social-media span {
      display: none;
    }
  }
</style>
