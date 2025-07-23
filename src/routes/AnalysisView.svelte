<script>
    // Local Modules
    import BackButton from "../lib/BackButton.svelte";
    import InfoTab from "../lib/InfoTab.svelte";

    // (WIP) Temporarily import currentPolicy from PolicyGallery
    // import { currentPolicy } from 'src/routes/PolicyGallery.svelte';
    // (WIP) Staticly Referencing Analysis Data
    import analysis from "../lib/data/analysis_results.json";
    const data = analysis[0];
    const general = data.analysis_sections;

    // State Variables
    let activeTab = 'general_equity_assessment';
    const tabOptions = [
        { key: 'general_equity_assessment', label: 'Equity Assessment', image: 'public/eq-asmnt.png' },
        { key: 'vulnerable_groups', label: 'Vulnerable Groups', image: 'public/vgroups.png' },
        { key: 'impact_severity', label: 'Impact Severity', image: 'public/sev.png' },
        { key: 'mitigation_strategies', label: 'Mitigation Strategies', image: 'public/mstrats.png' }
    ];
    const equitySections = [
        { key: 'recognitional_equity', label: 'Recognitional', color: '#F4A3A3' },
        { key: 'procedural_equity', label: 'Procedural', color: '#3B88A6' },
        { key: 'structural_equity', label: 'Structural', color: '#2AA78D' },
        { key: 'distributional_equity', label: 'Distributional', color: '#F0B340' }
    ];

</script>

<style>
    /* Container for the main content */
    .container { max-width: 960px; margin: 0 auto; padding: 2rem 1rem; font-family: system-ui, sans-serif; }

    /* Tab Elements */
    .tab-bar {
        display: flex;
        gap: 1rem;
        margin-bottom: 2rem;
        justify-content: center;
        background: #EDEDED;
        border-radius: 10px;
        padding: 1rem 0;
        width: 100%;
        box-sizing: border-box;
    }
    .tab { padding: 0.5rem 1rem; border: 2px solid #ccc; border-radius: 8px; background: #5bcce8; cursor: pointer; }
    .tab.active { background: #0C395A; color: white; border-color: #0C395A; }

    /* Equity Tab, Cards */
    .pill { padding: 0.4rem 0.8rem; font-weight: bold; font-size: 0.95rem; border-radius: 6px; color: #fff; margin-bottom: 0.5rem; display: inline-block; }
    .section { background-color: #eee; padding: 2rem; border-radius: 12px; margin-bottom: 2rem; }
    .title { font-size: 1.25rem; font-weight: 600; margin-bottom: 0.5rem; }
    .columns { display: flex; flex-wrap: wrap; gap: 1.5rem; margin-top: 1rem; }
    /* Pos. & Neg. Sections */
    .box { flex: 1 1 45%; background-color: #fff; padding: 1rem; border-radius: 8px; box-shadow: 0 0 2px rgba(0,0,0,0.1); min-height: 120px; }
    .box strong { display: block; margin-bottom: 0.4rem; font-size: 0.95rem; }
    /* Conclusion text styling */
    .conclusion { margin-top: 1rem; font-style: italic; color: #444; }

    h1 { font-size: 1.75rem; font-weight: 700; margin-bottom: 0.75rem; }
    .summary { color: #444; font-size: 1rem; margin-bottom: 2rem; line-height: 1.6; }
</style>

<section>
  <BackButton destination="#/" />
  <InfoTab />

  <div class="container">
    <h1>
      <img src="public/sel-btn.png" alt="{data.document.title}" style="height: 1em; vertical-align: middle; margin-right: 0.5em;">
      {data.document.title}
    </h1>


    <!-- Tab Bar -->
    <div class="tab-bar">
        {#each tabOptions as t}
        <button
            type="button"
            class="tab {activeTab === t.key ? 'active' : ''}"
            on:click={() => activeTab = t.key}
            aria-pressed={activeTab === t.key}
        >
            <img src={t.image} alt={t.label} style="height: 1em; vertical-align: middle; margin-right: 0.5em;">
            {t.label}
        </button>
        {/each}
    </div>

    {#if activeTab === 'general_equity_assessment'}
      <p class="summary">{general[activeTab].summary}</p>
      {#each equitySections as s}
        <div class="section">
          <div class="title">
            <span class="pill" style="background-color: {s.color}">{s.label}</span>
          </div>

          <div class="columns">
            <div class="box">
              <strong><img src="public/green-dot.png" alt="Positive Findings" style="height: 1em; vertical-align: middle; margin-right: 0.5em;"> Positive Findings</strong>
              <p>{general[activeTab][s.key].positive_findings}</p>
            </div>
            <div class="box">
              <strong><img src="public/red-dot.png" alt="Areas of Concern" style="height: 1em; vertical-align: middle; margin-right: 0.5em;"> Areas of Concern</strong>
              <p>{general[activeTab][s.key].concerns}</p>
            </div>
          </div>

          <div class="conclusion">
            <strong>Conclusion:</strong> {general[activeTab][s.key].conclusion}
          </div>
        </div>
      {/each}
    {:else}
      <p class="summary">{general[activeTab]}</p>
    {/if}

    <!-- Other Formats Will be Written -->

  </div>
</section>