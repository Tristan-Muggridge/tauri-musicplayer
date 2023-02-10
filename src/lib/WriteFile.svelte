<script lang="ts">
import { writeText, readText } from '@tauri-apps/api/clipboard';
import { createDir, BaseDirectory } from '@tauri-apps/api/fs';

  let input = "";
  let path = ""
  let output;

  async function writeToClipboard(){ 
    console.debug("help")
    output = "help"

    await createDir('Music\\MuggPlayer', { dir: BaseDirectory.Home, recursive: true });
  }
</script>

<div>
  <div class="row">
    <input id="path-input" placeholder="Enter a file path" type="file" bind:value={path} />
    <button on:click={writeToClipboard}>
      Compose
    </button>
  </div>
  <p>{output}</p>
</div>