<script>
  // import Header from './Header.svelte';
  import "./styles.css";
</script>

<div class="app">
  <!-- <Header /> -->

  <main>
    <slot />
  </main>

  <footer>
    <p>
      <a href="https://www.twitter.com/mariepastora">Twitter</a> | <a href="https://www.instagram.com/mariepastora/">Instagram</a> | <a href="https://www.goodreads.com/user/show/123909838-marie">Goodreads</a> | mariepastorapatino at gmail dot com
    </p>
  </footer>
</div>

<style lang="scss">

h1,
  p,
  h3,
  li {
    font-family: Quantico;
    color:black
  }
  a{
    color:black;
  }
  .app {
    display: flex;
    flex-direction: column;
  }
  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 64rem;
    padding: 2rem;
    box-sizing: border-box;
    @media (max-width: 600px) {
      padding: 1rem;
    }
  }

  footer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 12px;
  }

  footer a {
    font-weight: bold;
  }

  @media (min-width: 480px) {
    footer {
      padding: 12px 0;
    }
  }
</style>
