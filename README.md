# Chord & Lyrics Practice Tool

A single-page web tool for practicing songs with **chords aligned above each lyric character**, integrated with **audio playback, AB loop** and a **loop playlist**.  
Runs entirely in the browser – no backend, no build step.

- GitHub repo: <https://github.com/ymhomer/Chord-Lyrics-Practice-Tool>
- Live demo (GitHub Pages): <https://ymhomer.github.io/Chord-Lyrics-Practice-Tool>

---

## Features

- 🎼 **Chord-over-lyrics layout**
  - Splits every lyric line into characters and gaps.
  - Each character (and each gap) gets a `+` chord slot above it.
  - Click a slot to open a small **Chord editor** panel.
  - Supports quick buttons (C / G / Am / F / D / Em / Bm) or any custom chord (e.g. `C/G`, `Am7`).

- 🧾 **Lyrics editor with sections & hints**
  - Paste or type lyrics directly into the editor.
  - Load from a `.txt` file.
  - Insert sample lyrics for a starting template.
  - Use **section tags** like `[Intro]`, `[Verse 1]`, `[Chorus]`:
    - These appear as pills in the **section bar** and inline tags in the lyrics.
  - Use **hint text** inside parentheses `( ... )`:
    - Hints do not show in the lyric line.
    - They appear in the top **Hint bar** as the corresponding line comes into view.

- 🎧 **Audio player with AB loop**
  - Load a local audio file (e.g. MP3) via the bottom bar.
  - Set **A** and **B** points on the timeline.
  - Toggle **AB Loop** ON/OFF – the player will loop between A and B.
  - Choose playback speed: `0.25x / 0.5x / 0.75x / 1x / 2x`.

- 🔂 **AB loop playlist (per-song presets)**
  - Save the **current A/B points + lyric scroll position** as a named loop.
  - Each loop item shows:
    - Nearest section label (e.g. `Verse 1`, `Chorus`),
    - Line hint (e.g. `Line 8`),
    - A–B time range.
  - Clicking a saved item:
    - Restores its A/B range and enables AB loop.
    - Scrolls lyrics back to the saved view.
  - Delete individual loops or clear all.

- 🔍 **View & scroll control panel**
  - Adjust **font size** (lyrics & chords scale together).
  - Enable **auto scroll** and control scroll speed.
  - Handy for hands-free playing while watching the screen.

- 📤📥 **Session export & import (JSON)**
  - Export a **JSON session** that includes:
    - Raw lyrics text,
    - All chords and their positions,
    - AB loop playlist (A/B + scrollTop),
    - Font size, auto scroll, scroll speed,
    - Current A/B state and loop flag.
  - Import a previously exported JSON to restore an entire practice setup.
  - Great for moving between devices or resuming another day.

- 🖥️ **Pure front-end**
  - No server; all data stays in your browser.
  - Works on modern desktop and mobile browsers.

---

## Getting Started

### 1. Open the tool

You have two options:

- **Use GitHub Pages (recommended):**  
  <https://ymhomer.github.io/Chord-Lyrics-Practice-Tool>

- **Run locally:**
  ```bash
  git clone https://github.com/ymhomer/Chord-Lyrics-Practice-Tool.git
  cd Chord-Lyrics-Practice-Tool
  # Just open index.html in your browser
  # (double-click or drag into a browser window)
  ```

### 2. Add lyrics & build layout

1. Click **📝 Edit lyrics** (top-right of the main panel).
2. In the editor:
   - Paste lyrics, *one line per row*, **or**
   - Click **📄 Load TXT file** to load a `.txt`, **or**
   - Click **Insert sample lyrics** to see the expected format.
3. Add section labels and hints as needed (see next section).
4. Click **Build chord layout**.
5. The main view now shows:
   - Line numbers,
   - Section tags,
   - Lyric characters with `+` chord slots above and between characters.

### 3. Place chords

1. Click any **`+`** above a character or gap.
2. A **Chord editor** panel appears at the bottom-right.
3. Type a chord (e.g. `C`, `Am7`, `C/G`) or click a quick chord button.
4. Click **Apply** to commit.
5. To remove a chord:
   - Click the slot again and choose **Clear**, or
   - Apply an empty value.

---

## Lyrics Format & Markup

### Sections

Use square brackets to mark sections:

```text
[Intro]
[Verse 1]
[Chorus]
[Bridge]
```

- These are removed from the lyric text itself.
- They appear:
  - As inline green tags at the start of the line,
  - In the **section navigation bar** on top.

Clicking a section pill scrolls the lyrics so that section is centered.

### Hints

Use parentheses `( ... )` for hints:

```text
Instrumental only (4 bars intro)
In the quiet of the night    I am holding this guitar (play softer)
Following the steady beat    till the song is done (mute strum)
```

- Hints are stripped from the line body.
- When that line is near the center of the viewport, the hint text appears in the **Hint bar** at the top.
- Multiple hints on one line are joined with ` / `.

---

## Audio & AB Loop

At the bottom of the page:

1. Click **🎧 Load audio file** and select a local file.
2. Use the built-in audio controls to play/pause.
3. While playing:
   - Click **Set A** to store the start point.
   - Click **Set B** to store the end point.
4. Toggle **AB Loop** ON:
   - Playback loops between A and B.
5. Adjust playback speed via `0.25x / 0.5x / 0.75x / 1x / 2x`.

---

## AB Loop Playlist

Use the floating **📂** button to open the **AB loop playlist** panel.

- **Save loop**
  - Make sure A/B are set and looping works.
  - Scroll lyrics to where you want to follow.
  - Click **＋ Save current AB + view**.
  - A loop entry is added with:
    - Name based on nearest section label,
    - Line index,
    - A–B time range.

- **Recall loop**
  - Click a loop item:
    - AB loop is enabled with the stored A/B points.
    - Lyrics scroll to the saved position.
    - Audio jumps to A and plays.

- **Manage loops**
  - Use the ✕ button on each item to delete it.
  - Use **🗑 Clear all** to remove all loops.

---

## Export / Import JSON Sessions

### Export

In the **🔍 View & scroll** panel:

1. Click **📤 Export session**.
2. A file like `chord-lyrics-session.json` is downloaded.

The exported JSON contains:

```jsonc
{
  "version": 2,
  "rawLyrics": "Your lyrics here
...",
  "fontSize": 24,
  "scrollSpeed": 4,
  "autoScrollEnabled": false,
  "loops": [
    {
      "id": 1234567890,
      "a": 10.5,
      "b": 20.2,
      "scrollTop": 123,
      "label": "Chorus",
      "lineIndex": 8
    }
  ],
  "chords": [
    { "lineIndex": 4, "charIndex": 0, "kind": "char", "chord": "C" },
    { "lineIndex": 4, "charIndex": 1, "kind": "between", "chord": "G" }
  ],
  "ab": {
    "a": 10.5,
    "b": 20.2,
    "looping": true
  }
}
```

> **Note:** This structure is for reference. You normally don’t need to edit it manually.

### Import

1. Open the page.
2. Click **📝 Edit lyrics**.
3. Click **📥 Import JSON session**.
4. Choose a previously exported JSON file.
5. The tool restores:
   - Lyrics,
   - Chords,
   - AB loop playlist,
   - Font size & scroll speed,
   - Auto scroll state,
   - A/B points and loop flag.

Then simply re-load your audio file and continue practicing.

---

## Keyboard & UI Tips

- **Enter** in the chord editor: apply chord.
- **Esc** in the chord editor: close panel.
- Use the **section navigation pills** to jump quickly to `[Intro]`, `[Verse]`, `[Chorus]`, etc.
- When you’re not sure where something is, click the floating **❔** button to open the in-app guide.

---

## Development Notes

This project is intentionally simple:

- ✅ Single `index.html` with inline CSS & JavaScript.
- ✅ No build tooling, no dependencies.
- ✅ Suitable for cloning and tweaking for your own practice workflow.

Feel free to:

- Fork the repo.
- Customize chord quick buttons.
- Adjust styling (colors, spacing, shadows).
- Add your own shortcuts or layout tweaks.

---

## License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

---

## 简体中文简介

**Chord & Lyrics Practice Tool** 是一个用来练习歌曲的网页小工具：

- 在歌词上方精确对齐和显示和弦；
- 支持加载本地音频、设置 AB Loop 循环和播放速度；
- 可以保存多个 AB Loop（循环 + 当前歌词位置）形成播放列表；
- 支持导出 / 导入 JSON 会话，把歌词、和弦、AB Loop、显示设置一起保存，方便换设备或之后继续练习。

使用方式概览：

1. 打开页面：<https://ymhomer.github.io/Chord-Lyrics-Practice-Tool>
2. 点击 **📝 Edit lyrics**，粘贴歌词或加载 TXT 文件，按 **Build chord layout**。
3. 点击歌词上方的 `+` 添加和弦。
4. 底部加载音频，设置 A/B 点，再打开 **AB Loop** 做循环练习。
5. 用 **📂 AB loop playlist** 保存多个循环片段。
6. 用 **📤 Export session / 📥 Import JSON session** 在设备之间迁移或下次继续。

欢迎 Fork 和自定义成你自己的练习页面 🎸
