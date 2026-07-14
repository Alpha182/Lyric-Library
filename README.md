# 🎤 Lyric-Library

A small, hand-curated collection of **word-by-word synced lyrics** — the kind that light up one syllable at a time as a song plays.

Every file here is an alignment that earned a **★★★★★** rating in our lyric-aligner tool before being published, so this isn't a dump of everything we've ever made — it's the stuff that actually looks right.

---

## What's in here

```
lyrics/
  <spotifyTrackId>.ttml     one file per track, e.g. lyrics/0VjIjW4GlUZAMYd2vXMi3b.ttml
```

Files are **[AMLL](https://github.com/Steve-xmh/applemusic-like-lyrics)-style TTML** (Timed Text Markup Language). Each line carries per-word — often per-*syllable* — start/end times, plus optional background vocals:

```xml
<p begin="12.480" end="16.900" ttm:agent="v1">
  <span begin="12.480" end="12.720">So </span>
  <span begin="12.720" end="12.980">tell </span>
  <span begin="12.980" end="13.240">me </span>
  <span begin="13.240" end="13.900">that </span>
  <span ttm:role="x-bg">
    <span begin="13.500" end="13.780">(tell </span>
    <span begin="13.780" end="14.050">me)</span>
  </span>
</p>
```

- **`<span begin=".." end="..">`** — each sung word/syllable and exactly when it lands.
- **`ttm:role="x-bg"`** — background vocals ("echoes"), timed separately so they don't corrupt the lead line.
- **`ttm:agent`** — which voice sings the line (used to lay out duets as call-and-response).

Times are in seconds. That's it — no audio, no proprietary payloads, just timings you can drop into any TTML-aware lyrics player.

## How it's made

Each alignment is produced **from the audio itself**, not scraped from anyone's player:

1. **Separate** the vocals from the mix (Demucs).
2. **Force-align** the words to the isolated vocal with a phoneme model (MMS), anchored to synced LRC stamps where they exist.
3. **Clean up** — snap held notes to their sustain, cancel the aligner's small late bias, keep background vocals on their own track.
4. **Curate** — only alignments rated 5★ by a human get published here.

Plain lyric **text** comes from open sources ([LRCLIB](https://lrclib.net), NetEase); the **timing** is ours.

## Using a file

Look it up by Spotify track id:

```
https://raw.githubusercontent.com/Alpha182/Lyric-Library/main/lyrics/<spotifyTrackId>.ttml
```

Any AMLL-compatible viewer will render the word-by-word highlighting; a plain TTML parser will happily read the line- and word-level timings too.

## Notes

- **Coverage is intentionally small and slowly growing.** A track shows up here only after it's been checked and rated, so quality beats quantity.
- **No scraped content.** Alignments captured from third-party lyric backends are never published to this repo.
- Spotify ids are used purely as stable filenames — nothing here is affiliated with or endorsed by Spotify.

## License

Released under the **GNU General Public License v2.0** — see [`LICENSE`](LICENSE).
