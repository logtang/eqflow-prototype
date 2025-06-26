<script>
  // SPA Router for Svelte
  import Router from 'svelte-spa-router';

  // local components
  import NavBar from './lib/NavBar.svelte';

  // route components (screens)
  import HowItWorks from '../routes/HowItWorks.svelte';
  import PolicyGallery from '../routes/PolicyGallery.svelte';
  import Tool from '../routes/Tool.svelte';

  const routes = {
    '/': HowItWorks,
    '/gallery': PolicyGallery,
    '/tool': Tool
  };
</script>

<!-- Static navbar on every page -->
<NavBar />

<!-- This <Router> replaces the content dynamically based on URL -->
<main>
  <Router {routes} />
</main>

<style>
  main {
    padding: 2rem;
    font-family: system-ui, sans-serif;
  }
</style>