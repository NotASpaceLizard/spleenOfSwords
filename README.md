# Spleen of Swords

A lightweight character sheet tracker for our Daggerheart table. It is meant for **playing at the table**, not for building characters. Character creation and leveling still happen on heartofdaggers.com.

It is one HTML page plus one JSON file per character. There is no server, no account, and nothing to install.

## For players

1. Open the tracker link on your phone.
2. Tap your character.
3. Play. Everything you change saves automatically on your device.
4. At the end of the session, scroll to **End of session**, check the **Changes this session** list, and tap **Download**. Send the downloaded `.json` file to the organizer.
5. Re-enter the changes on heartofdaggers.com yourself, using the same list.

### What you can do on the sheet

- **Live tracks:** tap a box to mark up to it. Tap the last marked box to unmark it. HP, Stress, Hope, and Armor each have their own shape, so nothing depends on color.
- **Action buttons:** under any feature that says things like "mark a Stress", "spend 2 Hope", or "clear 2 Stress", there is a button that does it for you. A button is unavailable if you can't pay the cost: **"(not enough)"** for Hope, **"Stressed out"** when your Stress is full, and **"(nothing to clear)"** when there is no Stress to clear.
- **Once per rest:** a checkbox appears under any ability that says "once per rest". **Take a rest** resets them all.
- **Domain cards:** move a card between loadout and vault with the button on the card.
- **Gold, inventory, and notes:** edit them freely.

### Good to know

- **Your progress is stored in your browser on that one device.** Clearing browser data, or opening the sheet on a different phone, loses it. Download your file at the end of every session.
- Stats, features, and card text are read-only here. Fix mistakes on heartofdaggers and ask the organizer to refresh your file.
- **Discard session changes** resets your sheet back to the last frozen version.
- If a new version of the tracker doesn't seem to show up, wait a couple of minutes and reload. Adding `?v=2` (or any new number) to the end of the link also forces a fresh copy. The version number appears under your character's name.

## For the organizer

### What's in this repo

```
index.html             the tracker (all code and styling, heavily commented)
characters/index.json  the list of characters shown on the start screen
characters/*.json      one file per character
README.md              this file
```

### Session flow

1. Players make their edits and level-ups on heartofdaggers.
2. The GM calls a character freeze the night before.
3. Each player exports a fillable PDF of their sheet and sends it over.
4. The PDFs are converted into character JSON files in the layout below.
5. Upload the new files to `characters/` (**Add file → Upload files** on GitHub). A file with the same name replaces the old one.
6. After the game, players send back their downloaded JSON files. Upload them over the old ones so the repo reflects the end of the session.
7. Players update heartofdaggers by hand, since this tool is the source of truth as of the end of the session.

### Adding a character

1. Add the character's `.json` file to `characters/`.
2. Add its file name to `characters/index.json`, for example `["rondo.json", "someone-else.json"]`.

### Character file layout

Each file has two kinds of data:

- **Frozen data** comes from heartofdaggers and is shown read-only: identity, traits, defenses, maximums, weapons, domain cards, features, experiences, and advancements.
- **Live data** changes at the table: the `live` block (HP, Stress, Hope, and Armor marks, plus rest checkboxes), `gold`, `inventory`, `notes`, and each card's `inLoadout` flag.

`meta.frozenOn` records the freeze date. When it changes, any in-progress session saved on a player's device is ignored and the new frozen file takes over. Set it to the actual freeze date whenever a character file is refreshed.

### Tweaking the page

Open `index.html` and look at the comment block at the top. In short:

- **Colors:** the `:root` block in the `<style>` section.
- **Track shapes:** the `.hp`, `.stress`, `.hope`, and `.armor` rules.
- **Counters:** the `TRACKS` object in the script.
- **Action buttons:** the pattern in `btns()` controls which phrases get a button.
- **Wording and layout:** the `render()` function.

When you edit the file on GitHub, tell whoever is generating updates, or give them your current version, so a replacement does not undo your changes.

### Troubleshooting

- **The start screen shows no characters:** check that `characters/index.json` exists, that its file names match exactly, and that the `characters` folder sits next to `index.html`.
- **The page doesn't work when opened from a folder on your computer:** browsers block local file loading. Use the published link, or use the "open a file" option on the start screen.
- **A change doesn't appear:** hard refresh, wait for GitHub Pages to finish publishing, or use the `?v=` trick above.

## Notes

- This is an unofficial fan tool for personal use at our table. It is not affiliated with or endorsed by Darrington Press, Critical Role, or heartofdaggers.com.
- Daggerheart rules content comes from the publicly released SRD and from our own character sheets. If you keep this repo public, check Darrington Press's community content terms for any attribution they require.
- The data layout is designed so that other community Daggerheart sheet formats can be converted into it later.
