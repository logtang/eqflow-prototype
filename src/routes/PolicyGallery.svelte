<script>
  let selectedDoc = null;

  function openModal(doc) {
    selectedDoc = doc;
  }

  function closeModal() {
    selectedDoc = null;
  }

  const policies = [
    {
      id: 1,
      title: 'D-1641_WaterRights.pdf',
      summary: 'Defines rights and regulations for water distribution in the California Delta.',
      tags: ['Farmers', 'Urban'],
      image: 'public/waterlaw.png'
    },
    {
      id: 2,
      title: 'Policy_ElRio.pdf',
      summary: 'Water equity policy for El Rio region prioritizing distributive fairness.',
      tags: ['Low-income', 'Suburban'],
      image: '/documents/preview-2.png'
    },
    {
      id: 3,
      title: 'NileAccessFramework.pdf',
      summary: 'Procedural equity guidelines in multi-state water access along the Nile.',
      tags: ['Multinational', 'Indigenous'],
      image: '/documents/preview-3.png'
    },
    {
      id: 4,
      title: 'UrbanWaterAct2022.pdf',
      summary: 'Revises urban water regulations for housing developments and usage.',
      tags: ['Urban', 'Housing'],
      image: '/documents/preview-4.png'
    },
    {
      id: 5,
      title: 'AgriStreamRights.pdf',
      summary: 'Allocation strategy for agricultural irrigation streams across farmlands.',
      tags: ['Farmers', 'Agriculture'],
      image: '/documents/preview-5.png'
    },
    {
      id: 6,
      title: 'DeltaCommonsPlan.pdf',
      summary: 'Water policy co-developed with communities in delta zones.',
      tags: ['Community-led', 'Rural'],
      image: '/documents/preview-2.png'
    }
  ];
</script>

<section class="policy-gallery">
  <h2>Analyzed Water Policies</h2>
  <p class="subtext">
    Learn from examples and understand how different policies impact various communities.
  </p>

  <div class="card-grid">
    {#each policies as doc}
      <div class="policy-card">
        <img src={doc.image} alt={"Preview of " + doc.title} class="doc-preview" />

        <div class="card-header">
          <div>
            <strong>{doc.title}</strong>
            <div class="rating">High</div>
          </div>
          <p class="description">{doc.summary}</p>
        </div>

        <div class="tags">
          {#each doc.tags as tag}
            <span>{tag}</span>
          {/each}
        </div>

        <button class="view-btn" on:click={() => openModal(doc)}>View Analysis</button>
      </div>
    {/each}
  </div>
</section>

{#if selectedDoc}
  <div class="modal-overlay" on:click|self={closeModal}>
    <div class="modal-content">
      <button class="close-btn" on:click={closeModal}>✕</button>
      <div class="modal-grid">
        <img src={selectedDoc.image} alt={"Preview of " + selectedDoc.title} class="modal-doc" />
        <div class="modal-analysis">
          <h3>{selectedDoc.title}</h3>
          <p class="modal-summary">{selectedDoc.summary}</p>
          <div class="modal-tags">
            {#each selectedDoc.tags as tag}
              <span>{tag}</span>
            {/each}
          </div>
          <p class="modal-text">Coming soon: AI-generated policy analysis 🤖</p>
        </div>
      </div>
    </div>
  </div>
{/if}

<style>
.policy-gallery {
  text-align: center;
  max-width: 1100px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.policy-gallery h2 {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

.subtext {
  color: #555;
  margin-bottom: 2rem;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 24px;
  justify-items: center;
}

.policy-card {
  background: #f9f9f9;
  border-radius: 12px;
  padding: 1.25rem;
  width: 100%;
  max-width: 340px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.doc-preview {
  width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 12px;
  object-fit: cover;
}

.card-header > div {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.rating {
  background-color: #e5ecf9;
  color: #123d6a;
  font-size: 0.75rem;
  padding: 2px 8px;
  border-radius: 8px;
  font-weight: 600;
}

.description {
  font-size: 0.85rem;
  color: #444;
  margin: 8px 0;
  text-align: left;
}

.tags {
  display: flex;
  gap: 6px;
  margin: 10px 0;
  flex-wrap: wrap;
}

.tags span {
  background: #e3e3e3;
  border-radius: 999px;
  padding: 4px 10px;
  font-size: 0.75rem;
  color: #333;
}

.view-btn {
  margin-top: auto;
  padding: 10px;
  background: #0c395a;
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.2s ease-in-out;
}

.view-btn:hover {
  background: #0a2f4a;
}

/* Modal styling */
.modal-overlay {
  position: fixed;
  top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(3, 10, 30, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 999;
}

.modal-content {
  background: white;
  border-radius: 10px;
  max-width: 900px;
  width: 90%;
  padding: 24px;
  position: relative;
  box-shadow: 0 12px 30px rgba(0,0,0,0.2);
}

.modal-grid {
  display: flex;
  flex-direction: row;
  gap: 24px;
  align-items: flex-start;
}

.modal-doc {
  width: 45%;
  border-radius: 8px;
  object-fit: cover;
}

.modal-analysis {
  flex: 1;
  text-align: left;
}

.modal-summary {
  font-weight: 500;
  color: #444;
}

.modal-tags {
  display: flex;
  gap: 8px;
  margin: 12px 0;
}

.modal-tags span {
  background: #e3e3e3;
  border-radius: 999px;
  padding: 4px 10px;
  font-size: 0.75rem;
  color: #333;
}

.modal-text {
  font-size: 0.95rem;
  line-height: 1.5;
  color: #222;
}

.close-btn {
  position: absolute;
  top: 12px;
  right: 12px;
  background: none;
  border: none;
  font-size: 1.2rem;
  color: #333;
  cursor: pointer;
}
</style>