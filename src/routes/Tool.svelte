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

<style>
  @import '../styles/Tool-styles.css';
</style>

<section>
    <h1 style="text-align: center;">COEQWAL Equity Analysis Bot</h1>

    <!-- Doc. Upload Area -->
    <div id="upload-area">
        <label for="document-upload">1. Upload Document for Analysis:</label><br>
        <input bind:this={fileInput} type="file" id="document-upload" name="document" accept=".pdf,.docx,.txt,.html,.md">
        <button bind:this={uploadButton}>Upload</button>
        <div bind:this={uploadStatus}></div>
    </div>

    <!-- Chatbox, Messages, User Input -->
    <label for="input-area">2. Ask Questions about your document:</label>
    <div bind:this={chatbox} id="chatbox">
         <div class="status-message">Please upload a document to begin analysis.</div>
    </div>

    <div id="input-area">
        <input bind:this={queryInput} type="text" id="query-input" placeholder="Ask a question about the document's equity aspects..." disabled>
        <button bind:this={sendButton} id="send-button" disabled>Send</button>
    </div>

    <!-- Spinner Animation -->
    <div bind:this={thinkingIndicator} id="thinking-indicator" style="text-align: center; margin-top: 10px; display: none;">
         Analyzing... <div class="spinner"></div>
    </div>

    <!-- Add End Chat Section -->
    <div id="end-chat-area">
        <button bind:this={endChatButton} id="end-chat-button" disabled>End Chat & Clean Up Resources</button>
        <div id="end-chat-instructions">
            <strong>Important:</strong> Please click this button before closing the window to delete your uploaded document and associated resources from the server.
        </div>
        <div bind:this={cleanupStatus} id="cleanup-status" style="margin-top: 5px; font-weight: bold;"></div>
    </div>
</section>