<script>
  export let title;
  export let summary;
</script>

<style>
  .card {
    background-color: white;
    border-radius: 0.5rem;
    padding: 1rem;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
    border: 1px solid #ddd;
    height: 120px;
  }

  h2 {
    margin: 0 0 0.5rem;
    font-size: 1.1rem;
    color: #333;
  }

  p {
    margin: 0;
    color: #666;
    font-size: 0.9rem;
  }
</style>

<section>
    <div class="card">
        <h2>{title}</h2>
        <p>{summary}</p>
    </div>
</section>
