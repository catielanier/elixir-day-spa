<script>
  import axios from "axios";
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

<section id="about">
  <h2>Contact Us</h2>
  <p>
    Have a question about a treatment or ready to book your appointment? I’d
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
  <div>
    <form on:submit|preventDefault={sendMessage}>
      {#if success}
        Your email was successfully sent!
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
          cols="30"
          rows="10"
        />
      </div>
      <div><button type="submit">Send email</button></div>
    </form>
  </div>
</section>

<style>
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
  a {
    position: relative;
    display: inline-block;
    color: #e00;
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
  p {
    font-family: "Karla", sans-serif;
  }
</style>
