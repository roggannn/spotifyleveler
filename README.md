# Spotify Leveler

Keeps Spotify at a consistent loudness. If a song gets suddenly loud, or goes quiet and then loud again, the app turns Spotify's volume down for you so it never jumps out at you. You choose how loud "consistent" should be with a 0-100 slider.

## What you need

- Windows 10 or 11
- The Spotify **desktop app** (not the web player)

No Python or other installs needed.

## Getting started

1. Put `SpotifyLeveler.exe` anywhere you like (for example, a folder on your Desktop).
2. Double-click it.
3. **Windows may show "Windows protected your PC".** This happens because the app isn't code-signed, which costs money. Click **More info**, then **Run anyway**.
4. Start playing something in Spotify. The window will show Spotify's volume once it detects audio.

A green icon with equalizer bars appears in your system tray (you may need to click the small arrow near the clock to see it).

## Using it

- **Slider (0-100):** the loudness you want. Higher = louder overall, lower = quieter. 70 is a good place to start. Drag it while music is playing and listen for the level that suits you.
- **Enabled checkbox:** turns the leveling on or off. Turning it off sets Spotify's volume back to 100%.
- **Tray icon:** double-click to open the window. Right-click for **Show**, **Enabled**, and **Quit**.
- **Closing the window (X)** only hides it to the tray. The app keeps running. Use **Quit** from the tray menu to exit completely (this also resets Spotify to 100%).

The window shows the current output level, Spotify's mixer volume, and the song being learned (see below).

## Run at startup (optional)

1. Right-click `SpotifyLeveler.exe` and choose **Create shortcut**.
2. Right-click the shortcut, choose **Properties**, and add ` --minimized` to the end of the **Target** box (leave a space before it). This starts the app in the tray with no window.
3. Press **Win + R**, type `shell:startup`, and press Enter.
4. Move the shortcut into the folder that opens.

## How it works

The app listens to what your computer is playing, measures how loud it is, and moves Spotify's slider in the **Windows volume mixer** (not the slider inside Spotify) to stay near your target.

**It learns your songs.** The first time a song plays, the app remembers how loud it gets at each point. The next time that song plays, it already knows when a loud part is coming and turns Spotify down just before it arrives, instead of reacting afterwards. It gets a bit better each time you replay a song. The window shows "Learning this song" or "Predicting" for the current track.

## Good to know

- **It can only turn Spotify down, not up.** Spotify's mixer slider tops out at 100%. If quiet parts still sound too quiet, lower the 0-100 slider so loud parts are brought down closer to the quiet ones, then raise your Windows volume to compensate.
- **It listens to everything your PC plays**, not just Spotify. A video, call, or notification sound playing at the same time can confuse it for a moment.
- **If you switch speakers or headphones**, quit and restart the app.
- Spotify's own **Normalize volume** setting (Spotify Settings > Audio quality) works well alongside this app.

## Where things are saved

Settings and learned song data are saved in `%APPDATA%\SpotifyLeveler`
(paste that into the File Explorer address bar to open it).

- `leveler_config.json` holds your slider and on/off settings.
- The `profiles` folder holds the learned songs. Each file contains an artist and title. Delete the folder to make the app forget everything.
- `leveler_error.log` appears only if something goes wrong.

## Uninstalling

Quit the app from the tray, delete `SpotifyLeveler.exe` (and the startup shortcut if you made one), and delete the `%APPDATA%\SpotifyLeveler` folder.

## Troubleshooting

- **"Spotify: waiting for audio":** press play in the Spotify desktop app. Spotify only appears in Windows' mixer once it has made sound.
- **Volume doesn't seem to change:** check that **Enabled** is ticked and that the slider isn't at 100 (at 100 it almost never has anything to turn down).
- **Windows or antivirus blocks it:** see step 3 of Getting started. The file is safe, but unsigned apps trigger warnings.
- **Anything else:** check `leveler_error.log` in the folder above and send it to whoever gave you the app.
