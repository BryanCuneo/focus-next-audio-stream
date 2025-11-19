# focus-next-audio-stream
A bash script for Hyprland and PipeWire to cycle focus between widows that are actively playing audio.

## Installation Instructions
### 1. Clone this repository and `cd` into it
````
git clone https://github.com/BryanCuneo/focus-next-audio-stream.git
cd ./focus-next-audio-stream
````
### 2. Make the script executable
````
chmod +x ./focus-next-audio-stream.sh
````
### 3. Create a symlink to [focus-next-audio-stream.sh](./focus-next-audio-stream.sh) in your `$PATH` (e.g. `/usr/local/bin/`)
````
ln -s "$PWD/focus-next-audio-stream.sh" /usr/local/bin/focus-next-audio-stream
````
Alternatively, you can copy the file instead
````
cp ./focus-next-audio-stream.sh /usr/local/bin/focus-next-audio-stream
````
### 4. To test that it's working, open up a program and play some audio, such as a YouTube video and run
````
focus-next-audio-stream
````
Hyprland should move its focus to the window with audio playing

## Usage Instructions
Create a new keybinding in `~/.config/hypr/hyprland.conf`, for example:
````
bindd = SUPER SHIFT, A, Focus Next Audio Stream, exec, focus-next-audio-stream
````
For more details on creating Hyprland keybindings, see the [official documentation](https://wiki.hypr.land/Configuring/Binds/).

After saving your configuration, simply press your new shortcut!

## Limitations
Some windows may spin up multiple child process to play audio, most notable are browsers and their tabs. In cases like these, `hyprctl clients` does not have the ability to focus specific subprocess or specific browser tabs. It will find the top-level window for that process and focus that.

Notice in this example how the second browser window is skipped in the cycle despite being an active audio stream:
[focus_next_audio_stream](https://github.com/user-attachments/assets/833f88f3-55d9-4b51-b2a3-e6c3f1adca58)

This is a limitation of `hyprctl` and not something I can find any workaround for.
