<script>
  import { location } from 'svelte-spa-router';
  import { derived } from 'svelte/store';

  const currentRoute = derived(location, $loc => $loc)
</script>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    padding-top: 30px;
    background-color: #0C395A1F;
    border-bottom: 1px solid #ddd;
    font-family: system-ui, sans-serif;
    box-shadow: 0 4px 4px rgba(0, 0, 0, 0.1);
  }

  /* --- Nav Route Highlighting --- */
  nav a { color: #000; font-weight: 500; text-decoration: none; padding: 0.5rem 1rem; transition: color 0.2s ease; }
  nav a.selected { color: #2b99e7; font-weight: 600; }
  nav a:hover { color: #0C395A; }

  
  .logo { font-size: 1.5rem;}
  #icon { position: relative; top: 8px; left: -10px; width: 38px; height: auto; }
  ul { display: flex; gap: 1.5rem; list-style: none; margin: 0; padding: 0; align-items: center; }
  li a:hover { color: #2b99e7; }

  /* --- Contact Button --- */
  #contact-button { background-color: #0C395A; color: white; padding: 0.5rem 1.25rem; border: none; border-radius: 12px; font-size: 1rem; font-weight: 500; cursor: pointer; transition: background-color 0.2s ease, transform 0.1s ease; box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15); }
  #contact-button:hover { background-color: #0A2F4B; transform: translateY(-1px); }
</style>

<nav>
  <div class="logo">
   <img src='../../public/coeqwal-drop.png' id='icon' alt="COEQWAL Logo"> 
   <span id="align">Equiflow Analysis</span>
  </div>
  <ul class="align">
    <li>
      <a href="#/" class:selected={$currentRoute === '/'}>How it Works</a>
    </li>
    
    <li>
      <a href="#/gallery" class:selected={$currentRoute === '/gallery'}>Policy Gallery</a>
    </li>

    <li>
      <a href="#/tool" class:selected={$currentRoute === '/tool'}>Tool</a>
    </li>

    <li>
      <a href="https://live-coeqwal-ca.pantheon.berkeley.edu/contact-us/" target="_blank" rel="noopener noreferrer">
        <button id="contact-button">Contact</button>
      </a>
    </li>
  </ul>
</nav>


