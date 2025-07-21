<script>
  import LogoBar from "../lib/LogoBar.svelte";
  let documents = ['D-1641_WaterRights.pdf', 'Draft-2025.pdf'];
  let inputText = '';
</script>

<style>
  /* --- Layout --- */
  .screen-layout { position: absolute; top: 0; left: 0; right: 0; bottom: 0; display: flex; font-family: system-ui, sans-serif; background: #ffffff; color: #1f2937; }

  /* --- (1) Panel, Sidebar --- */
  .sidebar { width: 320px; padding: 24px; display: flex; flex-direction: column; justify-content: space-between; border-right: 1px dotted #ccc; background-color: #fff; }
  .sidebar h2 { font-size: 16px; font-weight: 600; margin-top: 36px; margin-bottom: 12px; }
  /* --- ./Sidebar Buttons --- */
  .buttons { display: flex; gap: 8px; margin-bottom: 24px; }
  .buttons button { font-size: 13px; padding: 8px 12px; border-radius: 6px; cursor: pointer; }
  .primary { background-color: #0F3C5F; color: white; border: none; }
  .primary:hover { background-color: #0d304f; }
  .secondary { background-color: transparent; color: #0F3C5F; border: 1px solid #0F3C5F; }
  .secondary:hover { background-color: #f0f8ff; }
  /* --- ./No Document Message --- */
  .no-doc {
    text-align: center;
    color: #666;
    font-size: 14px;
    padding-top: 275px;
  }
  .no-doc a {
    color: #0F3C5F;
    text-decoration: underline;
    font-size: 13px;
  }
  /* --- ./Recent Documents --- */
  .recent { font-size: 13px; }
  .recent-header { display: flex; justify-content: space-between; margin-bottom: 8px; color: #444; }
  .clear { background: none; color: #0F3C5F; border: none; font-size: 12px; cursor: pointer; }
  .recent ul { list-style: none; padding-left: 0; color: #222; }
  .recent li { margin-bottom: 4px; }

  /* --- (2) Panel, Main Chat --- */
  .main { flex: 1; display: flex; flex-direction: column; height: 100%; }
  /* --- ./Chat Header --- */
  .chat-header { background-color: #0F3C5F; color: white; padding: 16px 32px; }
  .chat-header h2 { font-size: 18px; font-weight: 600; }
  .chat-header p { font-size: 13px; color: #cbd5e1; }
  /* --- ./Chat Content --- */
  .chat-content { padding: 32px; flex: 1; overflow-y: auto; }
  /* --- Input Bar --- */
  .input-bar { display: flex; padding: 16px 32px; border-top: 1px solid #ddd; gap: 12px; align-items: center; background: white; }
  .input-bar input { flex: 1; border: 1px solid #ccc; padding: 10px 16px; border-radius: 999px; font-size: 14px; }
  .input-bar input:focus { outline: none; border-color: #0F3C5F; }
  .input-bar button { background-color: #0F3C5F; color: white; border: none; padding: 10px 16px; border-radius: 999px; font-size: 18px; cursor: pointer; }
  .input-bar button:hover { background-color: #0d304f; }
</style>

<section>
  <div class="screen-layout">
  <div style="position:absolute;top:0;left:0;width:320px;z-index:100;">
    <LogoBar />
  </div>
    <!-- (1) Panel, Sidebar -->
    <aside class="sidebar">
      <div class="sidebar-top">

        <h2>Document Analysis</h2>

        <div class="buttons" style="gap:4px;">
          <button class="primary" style="display:flex;align-items:center;gap:6px;padding:8px 10px; min-width:140px; justify-content:center;">
            <img src="public/docup-btn.png" alt="Upload" style="width:18px;height:18px;" />
            <span style="white-space:nowrap;">Upload (PDF)</span>
          </button>
          <button class="secondary" style="display:flex;align-items:center;gap:6px;padding:8px 10px; min-width:140px; justify-content:center;">
            <img src="public/sel-btn.png" alt="Select" style="width:18px;height:18px;" />
            <span style="white-space:nowrap;">Select</span>
          </button>
        </div>

        <div class="no-doc">
          <p>No Document</p>
          <a href="">Upload or select a document</a>
        </div>
      </div>

      <div class="recent">
        <div class="recent-header">
          <span>Recent Documents (Hardcoded)</span>
          <button class="clear">Clear</button>
        </div>
        <ul>
          {#each documents as doc}
            <li>{doc}</li>
          {/each}
        </ul>
      </div>
    </aside>

    <!-- (2) Panel, Main Chat -->
    <div class="main">
      <!-- Back Button (top right) -->
      <div style="position: absolute; top: 18px; right: 32px; z-index: 10;">
        <button
          style="background: #f3f4f6; color: #0F3C5F; border: 1px solid #0F3C5F; border-radius: 999px; padding: 8px 18px; font-size: 14px; cursor: pointer;"
          on:click={() => history.back()}
          aria-label="Go Back"
        >
          ← Back
        </button>
      </div>
      <!-- Header with Logo -->
      <div class="chat-header">
        <h2>EquiFlow AI Assistant</h2>
        <p>Intelligent Policy Equity Analysis</p>
      </div>
      <!-- Chat Box -->
      <div class="chat-content">
      </div>
      <!-- Input Bar -->
      <form class="input-bar" on:submit|preventDefault={() => {}}>
        <input
          bind:value={inputText}
          placeholder="Ask about equity impact , request comprehensive analysis or inquire about specific..."
        />
        <button type="submit">⮞</button>
      </form>
    </div>

  </div>
</section>
