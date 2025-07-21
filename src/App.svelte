<script>
  // SPA Router for Svelte, Navbar
  import Router from 'svelte-spa-router';

  // Navbar, Routing
  import LogoBar from './lib/LogoBar.svelte';
  import HowItWorks from './routes/HowItWorks.svelte';
  import PolicyGallery from './routes/PolicyGallery.svelte';
  import Tool from './routes/Tool.svelte';
  const routes = { '/': HowItWorks, '/gallery': PolicyGallery, '/tool': Tool };
</script>

<style>
  main {
    padding: 1.75rem;
    font-family: 'Inter', system-ui, sans-serif;
  }
</style>

<!-- Static navbar on every page -->
<!-- Temporarily Removing NavBar
<NavBar /> -->
<LogoBar />

<!-- This <Router> replaces the content dynamically based on URL -->
<main>
  <Router {routes} />
</main>

