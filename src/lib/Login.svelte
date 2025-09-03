<script>
  import { onMount } from "svelte";
  import { navigate } from "svelte-routing";
  import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
  import { firebase } from "../utils/firebase";
  import { getToken, setToken } from "../utils/tokenService";
  export let setLogin;

  let email = "";
  let password = "";
  let error = "";

  const doLogin = async (e) => {
    e.preventDefault();
    const auth = getAuth(firebase);
    signInWithEmailAndPassword(auth, email, password)
      .then((user) => {
        setToken(JSON.stringify(user));
        setLogin();
      })
      .finally(() => {
        navigate("/admin/dashboard");
      })
      .catch(() => {
        error = "invalid username or password";
      });
  };

  onMount(() => {
    if (getToken()) {
      navigate("/admin/dashboard");
    }
  });
</script>

<section id="login">
  <h2>Login</h2>
  <p>Enter your email and password to access your account.</p>

  <div class="form-wrapper">
    <form>
      {#if error.length}
        <p>[error]</p>
      {/if}
      <div>
        <input
          type="text"
          name="email"
          bind:value={email}
          required
          placeholder="Email"
        />
      </div>
      <div>
        <input
          type="password"
          name="password"
          bind:value={password}
          required
          placeholder="Password"
        />
      </div>
      <div class="btn-wrap">
        <button type="submit" on:submit={doLogin}>
          <span class="highlight">Log In</span>
        </button>
      </div>
    </form>
  </div>
</section>

<style>
  #login {
    padding: 4rem 2rem;
    max-width: 500px;
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
    margin-bottom: 1.5rem;
  }

  .form-wrapper {
    margin-top: 2rem;
  }
  form {
    max-width: 400px;
    width: 100%;
  }

  input {
    width: 100%;
    font-family: "Karla", sans-serif;
    font-size: 1.2rem;
    padding: 10px 15px;
    border: 0;
    border-bottom: 3px solid #ff0;
    margin-bottom: 1rem;
  }
  input::placeholder {
    font-family: "Playfair Display", serif;
    font-size: 1rem;
  }
  input:focus {
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

  /* tablet breakpoint */
  @media (max-width: 768px) {
    #login {
      padding: 3rem 1.5rem;
    }
    h2 {
      font-size: 1.75rem;
    }
    p {
      font-size: 1rem;
    }
    input {
      font-size: 1rem;
      padding: 8px 12px;
    }
    button {
      font-size: 1rem;
      padding: 0.5rem 0.75rem;
    }
  }

  /* phone breakpoint */
  @media (max-width: 480px) {
    #login {
      padding: 2rem 1rem;
    }
    h2 {
      font-size: 1.5rem;
    }
    p {
      font-size: 0.9rem;
    }
    input {
      font-size: 0.9rem;
      padding: 6px 10px;
    }
    button {
      display: block;
      width: 100%;
      text-align: center;
    }
  }
</style>
