This project was the result of trying to get something working in Tauri over the course of a couple of hours. Biggest time wasters included:
- [Getting permission to read the filesystem](https://tauri.app/v1/api/js/fs/#readdir)
- Figuring out how to see the console debug to find my errors (F12 on the app itself)
- [Figuring out why it couldn't find my resources](https://tauri.app/v1/api/js/tauri/#convertfilesrc)
- [Figuring out why I couldn't load assets](https://tauri.app/v1/api/config/#platform-specific-configuration)

Lesson Learned: Skimming the documentation is not the same as READING the documentation...

Upon opening the software for the first time it will attempt to scan the user's Music/MuggPlayer directory. Please add directories of mp3 and jpg files (album art) and either re-run the program, or utilise the "refresh" button depicted in below screenshot.

![Screenshot of application window](https://raw.githubusercontent.com/Tristan-Muggridge/tauri-musicplayer/main/readme/cover.png)

- Previous and Next buttons currently do not function, purely aesthetic
- Play/Pause button DOES work.
- Please click the track you wish to listen to

Below is a working file format as an example of how I've got it crudely parsing the directory. <br />
![Screenshot of recommended file structure example](https://raw.githubusercontent.com/Tristan-Muggridge/tauri-musicplayer/main/readme/FileExplorerExample.png)

# Tauri + Svelte + Typescript

This template should help get you started developing with Tauri, Svelte and TypeScript in Vite.

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Svelte](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode) + [Tauri](https://marketplace.visualstudio.com/items?itemName=tauri-apps.tauri-vscode) + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer).
