<script>
    // Local Modules
    import BackButton from "../lib/BackButton.svelte";
    import InfoTab from "../lib/InfoTab.svelte";

    // // (WIP) Temporarily import currentPolicy from PolicyGallery
    // import { currentPolicy } from '../lib/stores/currentPolicy.js';

    // // currentPolicy Store Variable 
    import analysis from "../lib/data/structured.json";

    // Hardcoded data for testing
    const data = analysis[0];
    const general = data.analysis_sections;

    // // Binding currentPolicy to its JSON
    // $: matched = $currentPolicy && analysis.find(
    //     (p) => p.document.filename === $currentPolicy.document.filename
    // );
    // $: general = matched?.analysis_sections;

    // console.log("Current policy filename:", $currentPolicy?.document?.filename);
    // console.log("Matched policy:", matched);


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
    .container { max-width: 1080; margin: 0 auto; padding: 2rem 1rem; font-family: system-ui, sans-serif; }

    /* Header and Subtitle */
    .header { margin-top: -75px; text-align: center; }

    /* Tab Elements */
    .tab-bar {
        display: flex;
        flex-wrap: nowrap;
        gap: 0.5rem;
        margin-bottom: 2rem;
        justify-content: center;
        background: #EDEDED;
        border-radius: 10px;
        padding: 1rem 2rem; /* Increased left/right padding */
        max-width: 600px;
        box-sizing: border-box;
        margin-left: auto;
        margin-right: auto;
        overflow-x: auto;
    }
    .tab { padding: 0.5rem 1rem; border: 2px solid #ccc; border-radius: 8px; background: #5bcce8; cursor: pointer; }
    .tab.active { background: #0C395A; color: white; border-color: #0C395A; }

    /* Equity Tab, Cards */

    .section-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 1.5rem; }
    .section { background-color: #eee; padding: 2rem; border-radius: 12px; margin-bottom: 2rem; }
    .pill { padding: 0.4rem 0.8rem; font-weight: bold; font-size: 0.95rem; border-radius: 6px; color: #fff; margin-bottom: 0.5rem; display: inline-block; }
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

    <div class="header">
      <h1>
        <img src="public/sel-btn.png" alt="{data.document.title}" style="height: 1em; vertical-align: middle; margin-right: 0.5em;">
        {data.document.title}
        <!-- <img src="public/sel-btn.png" alt="{selectedPolicy?.document?.title}" style="height: 1em; vertical-align: middle; margin-right: 0.5em;">
        {selectedPolicy?.document?.title} -->
      </h1>
    </div>


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

    <!-- General Equity Assessment -->
    {#if activeTab === 'general_equity_assessment'}
      <p class="summary">{general[activeTab].summary}</p>
      <div class="section-grid">
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
      </div>
      
    {:else}
      <p class="summary">{general[activeTab]}</p>
    {/if}

    <!-- Vulnerable Groups Formatting -->
    {#if activeTab === 'vulnerable_groups'}
      <h1>This is the Vulnerable Groups Tab!</h1>
    {/if}

    <!-- Impact Severity Formatting -->
    {#if activeTab === 'impact_severity'}
    <p class="summary">{general.severity_impact_analysis.summary}</p>

    <div class="section">
        <div class="title">
        <span class="pill" style="background-color: #ff7a7a">Impact Severity</span>
        </div>

        <div class="columns">
        <div class="box">
            <strong>
            <img src="public/green-dot.png" alt="High Severity Impacts" style="height: 1em; vertical-align: middle; margin-right: 0.5em;" />
            High Severity Impacts
            </strong>
            <p>{general.severity_impact_analysis.high_severity_impacts}</p>
        </div>

        <div class="box">
            <strong>
            <img src="public/red-dot.png" alt="Equity Implications of Impacts" style="height: 1em; vertical-align: middle; margin-right: 0.5em;" />
            Equity Implications of Impacts
            </strong>
            <p>{general.severity_impact_analysis.equity_implications_of_impacts}</p>
        </div>
        </div>

        <div class="conclusion">
        <strong>Conclusion:</strong> {general.severity_impact_analysis.conclusion}
        </div>
    </div>
    {/if}

    <!-- Mitigation Strategies Formatting -->
    {#if activeTab === 'mitigation_strategies'}
      <h1>This is the Mitigation Strategies Tab!</h1>
    {/if}
    

  </div>

</section>