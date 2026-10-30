# Adding and changing media on Hesa's phone

How to put your own **photos, videos and audio** (mp3, m4a, voice memos…) into the phone.

Everything happens on GitHub, on the branch **`claude/gifted-wozniak-sjb7me`**.

---

## 1. The two steps

Every media change is the same two steps:

1. **Upload the file** to the right folder.
2. **Point to it** in `index.html`, in the `CONFIG` block near the bottom.

### Step 1: upload a file

1. Open the upload page for the folder you want (links in the table below).
2. Tap **Choose your files** and pick the photo, video or audio.
3. Scroll down, choose **"Commit directly to the `claude/gifted-wozniak-sjb7me` branch"**, then tap **Commit changes**.

| Folder | What goes in it | Upload link |
|---|---|---|
| `media/` | profile photos (Isaac, Niel, Hesa…) | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media) |
| `media/photos/` | the Photos app (photos and videos) | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media/photos) |
| `media/whatsapp/` | photos, voice notes and documents sent in WhatsApp chats | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media/whatsapp) |
| `media/voice-memos/` | Voice Memos recordings | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media/voice-memos) |
| `media/spotify/` | artist pictures, album and song covers, the song's audio | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media/spotify) |
| `media/x/` | X avatars and post pictures | [upload](https://github.com/twoholies/heavenonearth/upload/claude/gifted-wozniak-sjb7me/media/x) |

> **Shortcut:** if you upload a file with **exactly the same name** as an existing one (for example a new `media/isaac.jpg`), it replaces the old one everywhere, and you can skip step 2.

### Step 2: point to it in `index.html`

1. Open the editor: <https://github.com/twoholies/heavenonearth/edit/claude/gifted-wozniak-sjb7me/index.html>
2. Search (Ctrl+F / Cmd+F) for the word from the tables below, for example `voiceMemos:`.
3. Write the file's path **inside the quotes**, including the folder: `"media/voice-memos/om-isa.m4a"`.
4. Commit to the `claude/gifted-wozniak-sjb7me` branch.

---

## 2. File rules (read once)

| ✅ Do | ❌ Avoid |
|---|---|
| Simple names: `niel.jpg`, `om-isa-nyanyi.m4a` | `#`, `?`, `%` in names, which break on the web |
| Lowercase, `-` instead of spaces | Spaces (they work, but are easy to mistype) |
| **Photos:** `.jpg`, `.png`, `.webp` | **`.HEIC`** (iPhone's default), which browsers can't show |
| **Videos:** `.mp4` | `.mov` (doesn't play in every browser) |
| **Audio:** `.mp3`, `.m4a` | `.wav` (works, but the files are huge) |
| Photos under ~1 MB, videos under ~10 MB | Very big files, which make the page slow to load |

- **Names must match exactly**, including capitals and the ending: `Niel.JPG` ≠ `niel.jpg`.
- **iPhone photo is HEIC?** Either set *Settings → Camera → Formats → Most Compatible* before taking it, or in Photos tap *Share → Save to Files* (iOS usually converts it to JPG), or use any "HEIC to JPG" converter.
- **iPhone Voice Memos:** open the memo, tap *⋯ → Share → Save to Files*. You get an `.m4a` file you can upload as-is.
- **iPhone screen recording:** it's already `.mp4`/`.mov`. If a `.mov` won't play, convert it to `.mp4` (or send it to Claude to convert).

---

## 3. App by app

Search `index.html` for the word in **bold** to find the spot.

### Lock screen and wallpaper (search **`wallpaper:`**)
```js
wallpaper: "media/my-wallpaper.jpg",
```
The same wallpaper is used behind the WhatsApp chats. To give chats a different background, set `chatWallpaper:` (search **`chatWallpaper`**).

### Profile photos for Isaac and Niel (search **`notifications: [`**)
```js
{ name: "Isaac", avatar: "media/isaac.jpg", message: "...", when: "now" },
{ name: "Niel",  avatar: "media/niel.jpg",  message: "...", when: "now" },
```
These photos are reused automatically in **WhatsApp, FaceTime, Phone** and group chats.
*(In the group chat members list, search `members: [`, and update `avatar:` there too.)*

### Hesa's own photo in WhatsApp voice notes (search **`myAvatar`**)
```js
myAvatar: "media/hesa.jpg",
```

### WhatsApp: photo, voice note, document (search **`whatsapp: {`**)
Inside a chat's `history:` or `script:`:
```js
{ from: "them", type: "photo", src: "media/whatsapp/selfie.jpg", text: "caption (optional)", time: "23.52" },
{ from: "them", type: "voice", duration: "0:14", audio: "media/whatsapp/isaac-goodnight.m4a", time: "23.55" },
{ from: "me",   type: "doc", name: "Tiket.pdf", pages: 2, size: "51 KB", preview: "media/whatsapp/tiket.jpg", time: "19.24" },
```
- `duration` is what the bubble shows before playing. Set it to the recording's real length.
- Without `audio:`, the voice note plays silently.

### Photos app (search **`photos: {`**)
```js
items: [
  { src: "media/photos/beach.jpg", date: "Today" },
  { src: "media/photos/concert.mp4", type: "video", date: "Yesterday" },
  { src: "media/photos/concert.mp4", type: "video", poster: "media/photos/concert.jpg", date: "Yesterday" },
],
```
- Newest first. The "Items" count updates by itself.
- For videos, `poster` (the grid picture) is **optional**. Without it, the video's first frame is shown.
- **Hidden album:** search **`hidden: {`** and use the same format in its `items:`. Its `passcode:` is there too.
- To remove a placeholder, delete its whole line (including the `{ … },`).

### Voice Memos (search **`voiceMemos:`**)
```js
{ title: "om isa nyanyiiii", date: "2 Mar 2026", duration: "13.22", audio: "media/voice-memos/om-isa-nyanyi.m4a" },
```
`duration` is minutes.seconds as the phone shows it (`13.22` = 13 min 22 s). With a real file, the player follows the file's actual length.

### Spotify (search **`spotify: {`**)
```js
avatar: "media/spotify/me.jpg",
{ type: "artist", title: "HAECHAN", image: "media/spotify/haechan.jpg" },
{ type: "album", title: "The Firstfruit - The 1st Album", sub: "Album • Mark Lee", image: "media/spotify/firstfruit.jpg" },
nowPlaying: { title: "Collide (feat. Tyga)", artist: "Justine Skye, Tyga", cover: "media/spotify/collide.jpg",
              duration: "3:24", position: "1:10", audio: "media/spotify/collide.mp3" },
```

### X (search **`x: {`**)
```js
me: { name: "hesa", avatar: "media/x/hesa.jpg" },
{ name: "Arung", handle: "@tulisanarung", avatar: "media/x/arung.jpg", image: "media/x/post1.jpg", ... },
```
`avatar:` works on posts, quote posts, DMs (`chats`) and suggested accounts. `image:` adds a picture to a post.

### FaceTime (search **`facetime:`**)
```js
{ name: "Mama", photo: "media/mama.jpg", label: "Suggested" },
```

---

## 4. Seeing your changes

- **The Claude link** (`claude.ai/artifact/…`) is a copy. It only changes when Claude republishes it, so tell Claude **"update the link"** after you commit.
- **GitHub Pages** (if you set it up later) updates by itself a minute or two after each commit.
- **Edits made on the page itself** (renaming a contact on the lock screen, etc.) are saved in that browser and override `CONFIG`. If your changes don't appear, open the page in a **private window**.

## 5. If something breaks

| Problem | Usually means |
|---|---|
| Photo shows empty / grey | File name or folder in `CONFIG` doesn't match the upload exactly, or it's HEIC |
| Video won't play | It's `.mov`, so convert it to `.mp4` |
| Voice note runs silently | `audio:` is missing or the file name doesn't match |
| Whole page is blank after an edit | A missing `"` quote or `,` comma near what you just changed |

Every commit is saved, so a mistake can always be undone from the file's **History** on GitHub. Or send Claude the part you edited.
