<script>
  import { onMount, tick } from 'svelte';
  import { registerDOM } from '../services/Tool-logic.js';

  let uploadButton, fileInput, uploadStatus, chatbox, queryInput, sendButton, thinkingIndicator, endChatButton, cleanupStatus;

  onMount(async () => {
    console.log('Tool component mounted. Waiting for DOM...');
    await tick();

    // Wait another microtask cycle
    setTimeout(() => {
      console.log('uploadButton:', uploadButton);
      console.log('uploadStatus:', uploadStatus);

      if (!uploadButton || !uploadStatus) {
        console.warn('DOM elements still not bound! ⛔️');
      } else {
        console.log('✅ All DOM refs present. Initializing...');
        registerDOM({
          uploadButton,
          fileInput,
          uploadStatus,
          chatbox,
          queryInput,
          sendButton,
          thinkingIndicator,
          endChatButton,
          cleanupStatus
        });
      }
    }, 0);
});
</script>

<style global>
  @import '../styles/Tool-styles.css';
</style>

<section>
    <h1 style="text-align: center;">COEQWAL Equity Analysis Bot</h1>

    <!-- (1) Doc. Upload Area -->
    <div id="upload-area">
        <p><strong>👋 Welcome to the COEQWAL Equity Analysis Tool!</strong></p><br>
        <input bind:this={fileInput} type="file" id="document-upload" name="document" accept=".pdf,.docx,.txt,.html,.md", on:change={() => uploadButton?.click()}>
        <button bind:this={uploadButton} id="upload-button">Upload</button>
        <div bind:this={uploadStatus} id="upload-status"></div>
    </div>

    <!-- (2) Chatbox, Messages, User Input -->
    <div bind:this={chatbox} id="chatbox">
         <div class="status-message">Please upload a document to begin analysis.</div>
    </div>

    <div id="input-area">
      <input id="query-input" bind:this={queryInput} type="text" placeholder="Ask about the document"/>

      <button class="icon-button" on:click={() => document.getElementById('document-upload').click()}>📎</button>

      <button class="icon-button" bind:this={sendButton}><img src="../../public/send-button.png" id="send-button1" alt="Send Button"></button>
    </div>

    <!-- (3) Spinner Animation -->
    <div bind:this={thinkingIndicator} id="thinking-indicator" style="text-align: center; margin-top: 10px; display: none;">
         Thinking... <div class="spinner"></div>
    </div>

    <!-- (4) Add End Chat Section, Removed -->
    <div id="end-chat-area">
        <button bind:this={endChatButton} id="end-chat-button" disabled>End Chat & Clean Up Resources</button>
        <div id="end-chat-instructions">
            <strong>Important:</strong> Please click this button before closing the window to delete your uploaded document and associated resources from the server.
        </div>
        <div bind:this={cleanupStatus} id="cleanup-status" style="margin-top: 5px; font-weight: bold;"></div>
    </div>
</section>