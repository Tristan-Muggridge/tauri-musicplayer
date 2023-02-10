<script lang="ts">
    import { readDir, BaseDirectory, type FileEntry } from '@tauri-apps/api/fs';
    import { convertFileSrc } from '@tauri-apps/api/tauri';

    let directories: FileEntry[] = [];
    let playing = null;
    let audioElement: HTMLAudioElement;

    let currentlyPlaying:string = "";

    async function readFiles(){ 
        directories = await readDir('Music\\MuggPlayer\\', { dir: BaseDirectory.Home, recursive: true });
    }

    const handleTrackOnClick = (id: string) => {      
        if (audioElement as HTMLAudioElement) audioElement.pause();
        audioElement = document.getElementById(id) as HTMLAudioElement;
        audioElement.play();
        currentlyPlaying = id;
        playing = true;
    }

    const handlePlayPauseOnClick = () => { playing = audioElement.paused; audioElement.paused ? audioElement.play() : audioElement.pause(); }

    readFiles();
</script>

<div>
    <div style="display: flex; gap: 1rem; flex-wrap:wrap;" class="row">
        {#each directories as dir}
            <div style="display: flex; flex-direction: column;  padding: 1rem; background-color: white; border-radius: 1rem; align-items: center;">
                {dir.name}
                {#if dir.children}
                    {#each dir.children.filter(file => file.name.slice(-3) == "jpg") as file, i}
                        {#if dir.name+".jpg" == file.name}
                            <img src="{convertFileSrc(file.path)}" alt="" style="width: 20rem; height: 20rem; border-radius: 1rem;">
                        {/if}
                    {/each}
                    {#each dir.children.filter(file => file.name.slice(-3) == "mp3") as file, i}
                        <span style="width: 100%; color: #0f0f0f; list-style: none; cursor: pointer; display: flex; gap: 1rem; justify-content: left;">
                            <p>{++i}.</p>
                            <p on:click={() => handleTrackOnClick(file.name)} on:keypress={() => handleTrackOnClick(file.name)}>{file.name.split('.')[0]}</p>
                            <audio id="{file.name}" src="{convertFileSrc(file.path)}" />
                        </span>
                    {/each}
                {/if}
            </div>
        {/each}        
    </div>

    <footer style="margin: 2rem 0; display: flex; flex-direction: column; justify-content: center; gap: 2rem;">
        <div>
            <button>&lt;</button>
            <button on:click={handlePlayPauseOnClick}>{!playing ? '▶' : '||' }</button>
            <button>&gt;</button>
        </div>
        <span>{currentlyPlaying.split('.')[0]}</span>
    </footer>

    <button on:click={readFiles} style="margin: 2rem 0;"> Refresh </button>
</div>