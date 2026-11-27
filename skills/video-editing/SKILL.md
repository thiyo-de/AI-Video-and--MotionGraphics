---
name: video-editing
description: Plan, edit, preview and verify videos in any format, including trims, interviews, tutorials, documentaries, motion pieces and social reels. Use for analysis, creative direction, transitions, voice, sound or final delivery.
---

# Video editing

## Start with the request

Scope edits, audits, examples and reports to the active project and the approved reference library. Keep every project self-contained under `projects/<project-name>/` (`assets/raw/`, `assets/clips/`, `assets/images/`, `audio/`, `manifests/`, `tools/`, and `export/`) — never store project media, scripts or exports in global workspace root folders. Include personal collection items only if the user explicitly selects them for the task. Inspect the relevant brief, media, existing timeline and approvals. For analysis or verification, report what you checked and stop there. For an exact technical change with an established delivery spec, perform the requested work and check the result. For creative work, follow the interview below before committing to a direction.

### Default visual style

For every creative edit, start with the bundled [Reference 2.0 style index and nine playable examples](references/reference-2-0-styles.md). The collection is the approved house style unless the user supplies a different direction. Use the index to pick a relevant example and open its existing contact sheet for composition and type. Play the matching passage when deciding motion, pacing or sound. Mention the reference ID and the specific pacing, type treatment or transition in the brief. If two directions would materially change the result, use the interview to resolve the choice. Build the footage, wording, graphics and soundtrack from the project's own material. Keep the single rough-cut review.

### Ask the editor's questions

Use Grill Me if available. Any agent can run the same interview directly in chat.

1. Read what the user has already supplied. Probe facts such as dimensions, runtime, available tracks and filenames locally. Carry forward previous answers.
2. Ask one to three unresolved questions that materially change the edit. Give a concrete recommendation and a short reason for each, then wait for the user's reply. An unanswered recommendation stays open. Ask dependent questions in the next round.
3. Start with the decision that changes the most work. For an interview that may be which answer to keep. For a tutorial it may be real-time versus condensed steps. For a creative brief it may be audience, destination or mood. Ask about language, original dialogue, VO, music, effects or intentional silence when the choice is open. Ask about the output spec only where it is unknown and consequential.
4. Summarize the chosen direction briefly in the existing brief or conversation. Carry approved choices and open questions into handoffs. Reopen a choice only when an instruction changes or evidence prevents the approved approach. When the user delegates a choice, stay within that delegation.

## Choose the work the edit needs

- Exact trim, crop, audio repair or re-export with complete instructions. Use the current source and validate the requested change. Create a preview if requested.
- Creative cut or revision. Establish what to keep, select shots or passages, mark cut points and make one playable rough cut. Keep a short edit map in the existing timeline or brief.
- Staged production. When the approved brief calls for generated footage, motion design or a separately produced mix, consult only the relevant sections of the [studio production guide](references/studio-production.md). Use the full planning skill for a commissioned multitrack production. Apply approvals to the stages the user chose.

## Preview with one playable cut

Use the current timeline and its built-in playback or supply one low-resolution MP4 that opens in a normal player. Show the actual layout at review scale, including framing, text placement, readable captions where planned, moving elements, entrances, exits and the intended transitions at their proposed speed. Include the planned dialogue or draft voiceover, action and transition SFX, and relevant ambience. Mute background music for the review. Use an existing take or inexpensive scratch track for unfinished sound and identify substitutions. For a missing essential track, flag the gap before asking the user to approve timing. Use real footage or stills where available and plain timed labels for missing shots. Spend preview effort on the editorial decision. Custom controls, vector recreations, decorative polish, alternative cuts, contact sheets and high-resolution renders require a specific review need or request.

For an existing assembly with the correct music-free review mix, this example writes a lightweight review copy. If music is baked into that file, export from the timeline with its music track muted or mux the music-free stems first. If the timeline lives in an editor, use its draft playback or proxy export directly. A proxy of an unedited source cannot demonstrate a proposed edit.

```sh
ffmpeg -n -i assembly.mp4 -map 0:v:0 -map 0:a:0? -vf "scale='min(iw,854)':'min(ih,854)':force_original_aspect_ratio=decrease:force_divisible_by=2" -c:v libx264 -preset ultrafast -crf 28 -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart review.mp4
```

On revision, play the changed interval with a little context on both sides. To share an excerpt from an updated assembly, use the same command with `-ss START` before the input, `-t DURATION` after it and a fresh output name. Review the full cut again when changes shift later timing. Play the encoded review cut once to verify the layout, moving elements, cuts and intended sounds. Share the preview with its open question and wait for sign-off before polish or a final render.

## Choose transitions from the shots

Start with a clean cut. When a transition serves the moment, describe the outgoing cue, incoming cue and where the eye or ear follows. For example, cut from a hand reaching to the next shot as it lands, switch angles as a foreground object covers the lens, or bring the next speaker's voice in before the picture changes. Match direction and speed for moving shots. Use a detail zoom only when the incoming shot resolves the same detail. A still hold can be the right choice for a speaker or a step the viewer must read.

For a modern look, show the user one proposed cut at the relevant timecode. Skip preset slide pushes, page turns and decorative wipes. Use the selected reference to study timing, movement and sound. Build the sequence from the project's own material. If asked for a current trend, verify a dated example relevant to that audience before describing it as trending.

Check suspect entries in continuous playback, after a seek and frame-by-frame across the cut. Look for a single black frame, double exposure, position jump, restarted source or an unready incoming frame. In browser compositions set the initial layer state before the first frame and prime the incoming media. Compare the same timecode in encoded output before attributing preview flicker to the export.

## Select sound effects and background music

Watch the rough cut once. For each meaningful transition or moving element, inspect the few frames around its entrance, contact or landing. Record the timecode, visible action and intended sound in the existing edit map. Keep a quiet beat when it serves the scene.

Search approved local recordings and licensed assets first (or retrieve real acoustic effects via `media-use` / Openverse CC0—never synthetic wave SFX; omit SFX when dialogue + music alone serves the story better). Search online for the remaining cues by action, material and character (for example, `short dry cloth swish, light, no impact`). When the choice is unclear, audition two or three candidates at comparable loudness against the same frames, with dialogue on and background music muted. Place the audible accent on the visual event. Check the opening for harsh noise, a heavy bass hit or a distracting tail. Reuse an approved cue where it fits.

After picture approval, select music by its role under the story, instruments, energy and vocal space. Test it beneath the busiest spoken line and through the final scene. If the brief calls for sound that the available recordings cannot supply, ask before generating custom SFX or music. A failed search or missing account leaves the choice open.

Choose a source that fits the delivery.

- **Realistic Foley and ambience.** Search the Openverse Audio API with an action and a license filter. Start with CC0. Use CC BY when the required credit can be delivered. Verify the item on its original page. Direct commercial use of Freesound's own API requires a separate arrangement. [Openverse audio search example](https://api.openverse.org/v1/audio/?q=cloth%20movement&license=cc0&page_size=2) · [Freesound API terms](https://freesound.org/docs/api/terms_of_use.html)
- **Short motion cues and online commercial music.** Browse individual Mixkit effects or instrumentals. Match the music license to the destination, especially for broadcast. [Mixkit SFX](https://mixkit.co/free-sound-effects/) · [Mixkit music](https://mixkit.co/free-stock-music/) · [Terms](https://mixkit.co/terms/)
- **Alternative instrumental beds.** Browse Pixabay Music and retain the download certificate when the track is registered with Content ID. For a cinematic score, consider Scott Buckley when the client can publish the required credit. [Pixabay music](https://pixabay.com/music/) · [Pixabay FAQ](https://pixabay.com/service/faq/) · [Scott Buckley licensing](https://www.scottbuckley.com.au/library/using-this-music/)

Use the provider's permitted download method. Keep the selected recording's title, creator, source URL, license and required credit or certificate with the project. Use a project-relative path for the local audio. The rough-cut preview keeps background music muted.

## Check sound and delivery

- List the tracks expected from the brief. For dialogue or VO, check first and last words, intelligibility, sync and music masking. For intended effects, audition the cue against the visible action. Check entrances, exits, clicks and quiet passages. Check that an intentionally silent delivery meets the agreed track layout.
- Use the delivery spec for integrated loudness, true peak and channel layout. For the studio social mix, the house target is −14 LUFS ±0.5 and at most −1 dBTP. Measure the encoded deliverable and audition speech and key cues, including a `350 Hz–7 kHz` mono mobile fold-down if relevant.
- Export using the approved size, aspect, frame rate, duration, codec and audio settings. Fully decode the delivered file, probe the actual streams, and play the opening, closing and changed cuts. Check crops, captions, sync and unintended flashes at delivery size. For a decoupled video-only copy without re-rendering, strip audio losslessly (`-map 0:v:0 -c:v copy -an -movflags +faststart`) into `projects/<project-name>/video only/`, and prune temporary render caches (`tools/cache/hfcache-*`, `.hyperframes/`, `audio/qa/`) after final verification.
- The bundled `scripts/video_workbench.py validate` checks the file against supplied expectations. Pass relevant targets and expected stream counts explicitly, including `--audio-streams 0` for a video-only export. See the [quality checklist](references/quality-gates.md) when a deeper audit is needed. Report what was measured, what was seen or heard, and any check still pending.
