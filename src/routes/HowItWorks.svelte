<script>
  // State variables for modals
  let showInfo = false;
  let showAnalysis = false;
  let showUpload = false;

  // State variable for selected policy in analysis modal
  let selectedPolicy = null;

  function openAnalysisModal(policy) {
    selectedPolicy = policy;
    showAnalysis = true;
  }

  // File upload handling (currently a placeholder)
  let recentDocs = [
    'D-1641_WaterRights.pdf',
    'Delta-Draft-2025.pdf',
    'Policy_Equity_Framework.pdf'
  ];

  export const policies = [
    {
      fileName: 'California Delta Water Rights',
      description: 'California Delta water allocation policy defining rights and regulations for water distribution across the state.',
      equityTag: ['Recognitional', 'Procedural'],
      summary: "This policy governs the allocation of water resources in California's Delta region, aiming to balance agricultural, urban, and environmental needs. It addresses historical inequities in water access and sets guidelines for sustainable management.",
      vulnerableGroups: ['Low-income households', 'Rural communities', 'Minority populations'],
      severityOfImpact: ['High for water access', 'Moderate for economic stability', 'Low for educational outcomes'],
      mitigationStrategies: ['Targeted subsidies', 'Community engagement', 'Policy revisions']
    },
    {
      fileName: 'Urban Heat Mitigation Strategy',
      description: 'Outlines strategies for heat resilience in underserved neighborhoods.',
      equityTag: 'Procedural',
      summary: "This policy proposes interventions to reduce urban heat in vulnerable neighborhoods, focusing on increasing green spaces and improving infrastructure to protect at-risk populations.",
      vulnerableGroups: ['Elderly residents', 'Outdoor workers', 'Children'],
      severityOfImpact: ['High for health outcomes', 'Moderate for utility costs', 'Low for property values'],
      mitigationStrategies: ['Tree planting', 'Cooling centers', 'Public awareness campaigns']
    },
    {
      fileName: 'Inclusive Public Transport Policy',
      description: 'Policy for equitable access to public transit.',
      equityTag: 'Distributional',
      summary: "Aims to ensure all community members have affordable and reliable access to public transportation, reducing barriers for marginalized groups.",
      vulnerableGroups: ['People with disabilities', 'Low-income commuters', 'Elderly'],
      severityOfImpact: ['High for mobility', 'Moderate for employment access', 'Low for environmental impact'],
      mitigationStrategies: ['Fare subsidies', 'Accessible vehicles', 'Expanded service hours']
    },
    {
      fileName: 'Clean Air Initiative',
      description: 'A policy to improve air quality in urban centers through stricter emissions standards and community monitoring.',
      equityTag: ['Structural', 'Transformational'],
      summary: "This initiative enforces stricter air pollution controls and funds community-led air quality monitoring, prioritizing neighborhoods with historically poor air quality.",
      vulnerableGroups: ['Asthmatic individuals', 'Children', 'Low-income urban residents'],
      severityOfImpact: ['High for respiratory health', 'Moderate for healthcare costs', 'Low for local businesses'],
      mitigationStrategies: ['Emission reduction incentives', 'Community monitoring programs', 'Healthcare support']
    }
  ];

</script>

<style>
  /* --- Main Container --- */
  .container { max-width: 1600px; }
  /* --- Header Styles --- */
  .info-button { position: absolute; top: 2rem; right: 2rem; background: #1d3f67; border: none; border-radius: 50%; width: 2.5em; height: 2.5em; display: flex; align-items: center; justify-content: center; box-shadow: 0 2px 8px rgba(0,0,0,0.12); cursor: pointer; font-size: 1.3em; z-index: 10; }
  /* --- Try EquiFlow Button --- */
  .cta { margin: 1.5rem 0; padding: 0.75rem 1.5rem; background-color: #0C8BA7; color: white; border: none; border-radius: 6px; font-weight: bold; font-size: 1rem; }
  
  /* --- Grid, Policy Cards --- */
  .card-grid { 
    display: grid; 
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); 
    gap: 0.8rem; 
    padding-left: 2.5rem; 
    padding-right: 2.5rem;
  }
  .card { 
    position: relative; 
    background: #0C8BA71C; 
    padding: 0.85rem; 
    border-radius: 10px; 
    box-shadow: 0 4px 10px -3px rgba(0,0,0,0.38);
    transition: transform 0.2s ease; 
    min-height: 290px; 
    display: flex; 
    flex-direction: column; 
    font-size: 1rem; 
  }
  .card:hover { transform: scale(1.01); }
  .card h3 { 
    text-align: center; 
    margin-top: 0.15em;
    margin-bottom: 0.4em;
  }
  .card p { text-align: center; }
  /* --- ./Equity Tag on Card --- */
  .tag { 
    position: static;
    display: inline-flex;
    align-items: center; 
    justify-content: center;
    background: #8b5cf6;
    color: white;
    font-size: 0.75rem;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    max-width: 140px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    vertical-align: middle;
    width: fit-content;
    min-width: 0;
    margin-top: 0;
    margin-bottom: 1.5rem; /* Increased space below tags */
  }
  /* --- ./View Analysis Button on Card --- */
  .analysis-btn {
    position: absolute;
    bottom: 1rem;
    left: 1rem;
    right: 1rem;
    background-color: #0C395A;
    color: white;
    padding: 0.8rem 1.5rem;
    border: none;
    border-radius: 12px;
    font-size: 1.13rem;
    height: 2.7em;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 400;
    max-width: 260px;
    margin-left: auto;
    margin-right: auto;
    font-family: 'Inter', sans-serif;
  }
  /* --- Modal --- */
  .modal-backdrop { position: fixed; inset: 0; background: rgba(0,0,0,0.4); z-index: 50; }
  .modal { position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: white; padding: 3.5rem; border-radius: 18px; width: 99vw; max-width: 1200px; min-height: 80vh; z-index: 100; box-shadow: 0 0 32px rgba(0,0,0,0.28); }
  /* --- ./Upload Area --- */
  .upload-area { background: #D9D9D9; border: 1px dashed #444; padding: 2rem; border-radius: 12px; margin-bottom: 2rem; display: flex; flex-direction: column; align-items: center; justify-content: center; }
  /* --- ./Recent Documents List in Modal --- */
  ul.recent-list { margin-top: 1rem; padding-left: 1rem; }
</style>

<section class="container">
  <!-- Hamburger Menu (Unfinished) 
   Equity Analysis Tool, Learn More -->
  <button aria-label="Menu" class="info-button" title="Open Menu" on:click={() => showInfo = true}>
    <span style="font-weight: bold; color: white; font-size: 1.7em;">
      &#9776;
    </span>
  </button>
  <!-- Headers, Caption -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet">
  <h2
    style="
      font-family: 'Inter', sans-serif;
      font-weight: 400;
      font-size: 72px;
      text-align: center;
      margin-top: -1rem;
      margin-bottom: 2rem;
      line-height: 1.1;
        "
      >
        Policy <span style="color: #0C395A;">Equity</span> Gallery
      </h2>
      <p
        style="
      font-family: 'Inter', sans-serif;
      font-size: 26px;
      text-align: center;
      margin-bottom: 2rem;
      max-width: 1100px;
      margin-left: auto;
      margin-right: auto;
      line-height: 1.3;
        "
      >
        Explore pre-analyzed water policies. 
        Each policy has been automatically evaluated using our Equity Framework, providing instant insights with dynamic visualizations
      </p>
      <h3
        style="
      font-family: 'Inter', sans-serif;
      font-size: 1.75rem;
      font-weight: 500;
      color: black;
      text-align: center;
      margin-bottom: 2.2rem;
      letter-spacing: 0.02em;
        "
      >
        Pre-Analyzed Documents 
        <span style="display: inline-flex; align-items: center; gap: 0.25em; margin-left: -0.15em;">
          <img 
            src="public/down-arrow.png" 
            alt="Down Arrow" 
            style="height: 0.9em; position: relative; top: 0.1em;"
          >
        </span>
      </h3>
  <!-- Removed, CTA Button -->
  <!-- <button class=</div>"cta" on:click={() => showUpload = true}>
    <img src="public/mdi_magic.png" alt="EquiFlow" style="height: 1.2em; vertical-align: middle; margin-right: 0.5em;" />
    Try EquiFlow
  </button> -->

  <!-- Grid-Enabled Gallery View -->
  <div class="card-grid" style="grid-template-columns: repeat(3, 1fr); gap: 2.5rem;">
    {#each policies as policy}
      <div class="card">
        <h3>{policy.fileName}</h3>
        <p>{policy.description}</p>
        <!-- Removed, Tag Row: Place tags in a horizontal row, not absolute -->
        <!-- <div style="display: flex; flex-wrap: wrap; gap: 0.5em; margin-bottom: 2.5rem; margin-top: auto;">
          {#if Array.isArray(policy.equityTag)}
            {#each policy.equityTag as tag}
              <span
                class="tag"
                style="
                  position: static;
                  background: 
                    {tag === 'Recognitional' ? '#8b5cf6' : 
                     tag === 'Procedural' ? '#ef4444' : 
                     tag === 'Distributional' ? '#3b82f6' : 
                     tag === 'Structural' ? '#fde047' : 
                     tag === 'Transformational' ? '#22c55e' : 
                     '#22c55e'};
                  color: {tag === 'Structural' ? '#222' : 'white'};
                "
              >
                {tag}
              </span>
            {/each}
          {:else}
            <span
              class="tag"
              style="
                position: static;
                background: 
                  {policy.equityTag === 'Recognitional' ? '#8b5cf6' : 
                   policy.equityTag === 'Procedural' ? '#ef4444' : 
                   policy.equityTag === 'Distributional' ? '#3b82f6' : 
                   policy.equityTag === 'Structural' ? '#fde047' : 
                   policy.equityTag === 'Transformational' ? '#22c55e' : 
                   '#22c55e'};
                color: {policy.equityTag === 'Structural' ? '#222' : 'white'};
              "
            >
              {policy.equityTag}
            </span>
          {/if}
        </div> -->
        <button class="analysis-btn" on:click={() => openAnalysisModal(policy)}>View Analysis</button>
      </div>
    {/each}
    <!-- Add Policy Card Outline Button-->
    <button
      type="button"
      class="card"
      style="
        border: 2px dashed #0C8BA7;
        background: #f8fafc;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 320px;
        cursor: pointer;
        box-shadow: none;
        position: relative;
      "
      on:click={() => showUpload = true}
      title="Add a new policy"
      aria-label="Add Policy"
    >
      <div
        style="
          width: 3.5em;
          height: 3.5em;
          border-radius: 50%;
          background: #0C8BA7;
          display: flex;
          align-items: center;
          justify-content: center;
          margin-bottom: 1em;
        "
      >
        <span style="color: white; font-size: 2em; font-weight: bold;">+</span>
      </div>
      <div style="text-align: center;">
        <span style="font-size: 1.1em; color: #0C8BA7; font-weight: 500;">Add Policy</span>
        <p style="font-size: 0.95em; color: #444; margin-top: 0.5em;">Upload a new policy for equity analysis</p>
      </div>
    </button>
  </div>

  <!-- Modals!! Yay -->
  <!-- i. Modal, Info/Onboarding -->
  {#if showInfo}
    <div
      class="modal-backdrop"
      role="button"
      tabindex="0"
      aria-label="Close info modal"
      on:click={() => showInfo = false}
      on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') { showInfo = false; } }}
    ></div>
    <div
      class="modal"
      role="dialog"
      aria-modal="true"
      tabindex="0"
      on:click|stopPropagation
      on:keydown|stopPropagation
      style="display: flex; flex-direction: column; align-items: center;"
    >
      <img src="public/info.png" alt="Info Modal" style="max-width: 100%; border-radius: 12px; margin-bottom: 2rem;" />

    </div>
  {/if}

  <!-- 1. Modal, Policy Analysis -->
  {#if showAnalysis}
    <div
      class="modal-backdrop"
      role="button"
      tabindex="0"
      aria-label="Close analysis modal"
      on:click={() => showAnalysis = false}
      on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') { showAnalysis = false; } }}
    ></div>
    <div
      class="modal"
      role="dialog"
      aria-modal="true"
      tabindex="0"
      on:click|stopPropagation
      on:keydown|stopPropagation
      style="display: flex; flex-direction: column; align-items: flex-start;"
    >
      <!-- Dropdowns Row -->
      <div style="display: flex; gap: 1rem; margin-bottom: 1.5rem;">
        <select style="padding: 0.5rem 1rem; border-radius: 6px; border: 1px solid #ccc;">
          <option>Policy Version</option>
          <option>D-1641_WaterRights.pdf</option>
          <option>UrbanHeatMitigation.pdf</option>
          <option>InclusiveTransport.pdf</option>
        </select>
      </div>

      <!-- Executive Summary -->
      <div style="margin-bottom: 2rem; width: 100%;">
        <h2 style="margin-bottom: 0.5rem;">Executive Summary</h2>
        <p style="font-size: 1.1rem; color: #333;">
          {selectedPolicy ? selectedPolicy.summary : ''}
        </p>
      </div>

      <!-- Three Panels Side by Side (Extended Containers) -->
      <div style="display: flex; gap: 1.5rem; width: 100%; justify-content: space-between;">
        <div style="flex: 1 1 0; min-width: 0; background: #f3f4f6; border-radius: 10px; padding: 2.5rem 2rem; min-height: 180px;">
          <h3 style="margin-top: 0;">Vulnerable Groups</h3>
          <p style="margin: 0; padding-left: 1.2em;">
            {selectedPolicy && selectedPolicy.vulnerableGroups ? selectedPolicy.vulnerableGroups.join(', ') : ''}
          </p>
        </div>
        <div style="flex: 1 1 0; min-width: 0; background: #f3f4f6; border-radius: 10px; padding: 2.5rem 2rem; min-height: 180px;">
          <h3 style="margin-top: 0;">Severity of Impact</h3>
          <p style="margin: 0; padding-left: 1.2em;">
            {selectedPolicy && selectedPolicy.severityOfImpact ? selectedPolicy.severityOfImpact.join(', ') : ''}
          </p>
        </div>
        <div style="flex: 1 1 0; min-width: 0; background: #f3f4f6; border-radius: 10px; padding: 2.5rem 2rem; min-height: 180px;">
          <h3 style="margin-top: 0;">Mitigation Strategies</h3>
          <p style="margin: 0; padding-left: 1.2em;">
            {selectedPolicy && selectedPolicy.mitigationStrategies ? selectedPolicy.mitigationStrategies.join(', ') : ''}
          </p>
        </div>
      </div>

      <!-- Action Buttons Row -->
      <div style="display: flex; gap: 1.2rem; position: absolute; bottom: 2.5rem; right: 3.5rem;">
        <button
          class="cta"
          style="background: #0C395A; color: #fff; font-size: 1rem; padding: 0.7rem 1.5rem; border-radius: 6px;"
          on:click={() => { window.location.hash = '#/tool'; showAnalysis = false; }}
        >
          Chat with EquiFlow
        </button>
        <button
          class="cta"
          style="background: #888; color: #fff; font-size: 1rem; padding: 0.7rem 1.5rem; border-radius: 6px;"
          on:click={() => showAnalysis = false}
        >
          Close
        </button>
      </div>
    </div>
  {/if}

  <!-- 2. Modal, Document Upload -->
  {#if showUpload} <!-- Listener -->
    <div
      class="modal-backdrop"
      role="button"
      tabindex="0"
      aria-label="Close upload modal"
      on:click={() => showUpload = false}
      on:keydown={(e) => { if (e.key === 'Enter' || e.key === ' ') { showUpload = false; } }}
    ></div>
    <div
      class="modal"
      role="dialog"
      aria-modal="true"
      tabindex="0"
      on:click|stopPropagation
      on:keydown|stopPropagation
    >
      <p style="font-size: 1.3rem; text-align: center;">
        Upload a policy document and get an interactive, equity-focused analysis with actionable insights, powered by the Equity Framework. 
        Visualize impacts, explore key metrics, and interact with tailored recommendations-- all in one place.
      </p>

      <div style="margin-bottom: 1rem; text-align: center;">
        <img src="public/steps.png" alt="Upload Illustration" style="max-width: 800px; width: 100%; border-radius: 8px;" />
      </div>

      <div class="upload-area">
        <p>No policy uploaded yet.</p>
        <p>Upload a PDF policy document to begin analysis</p>
        <button class="cta" on:click={() => window.location.hash = '#/tool'} style="display: inline-block; cursor: pointer; background: #0f2c54; color: #fff; font-size: 0.95rem; padding: 0.4rem 1rem; border-radius: 5px;">Upload Policy (PDF)</button>
      </div>

      <h4>Recent Documents (Currently Hardcoded)</h4>
      <ul class="recent-list">
        {#each recentDocs as doc}
          <li>{doc}</li>
        {/each}
      </ul>
    </div>
  {/if}

</section>