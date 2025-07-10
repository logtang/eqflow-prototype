<script>
  // You can add routing support later if you're using something like `svelte-routing`
</script>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: white;
    border-bottom: 1px solid #ddd;
    font-family: system-ui, sans-serif;
  }

  .logo {
    font-weight: bold;
    font-size: 1.25rem;
  }

  .coeqwaldrop {
    height: 25px;
    vertical-align: middle;
  }

  ul {
    display: flex;
    gap: 1.5rem;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  li a {
    text-decoration: none;
    color: black;
    font-weight: 500;
  }

  li a:hover {
    color: #0070f3;
  }
</style>

<nav>
  <div class="logo"> 
    <img src="/assets/coeqwaldrop.png" alt="COEQWAL Logo" class="coeqwaldrop"> 
    EQUIFLOW
  </div>

  <ul>
    <li><a href="#/">Home</a></li>
    <li><a href="#/gallery">Policy Gallery</a></li>
    <li><a href="#/tool">Tool</a></li>
  </ul>
</nav>