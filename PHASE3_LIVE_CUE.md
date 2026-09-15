# Phase 3: LIVE Chain and Phrase Cue

Phase 3 builds on Phase 1/2 LIVE playback.

## LIVE behavior

In LIVE mode, each track/column can launch a Chain selected from any Song row. The selected Chain plays through all of its Chain rows (phrases) and loops at the end of the Chain until another Chain is launched/cued for that track.

## Controls

- `SHIFT+PLAY` (Select+Start on the RG40xxH): toggle LIVE mode. Turning LIVE off stops playback.
- `PLAY` on a Chain in LIVE mode:
  - If the track is stopped, launch the selected Chain.
  - If the track is already playing, queue the selected Chain for the end of the currently playing Chain.
- `OPT+PLAY` (B+Start on the RG40xxH) on a Chain in LIVE mode:
  - If the track is stopped, launch the selected Chain.
  - If the track is already playing, queue the selected Chain for the end of the currently playing Phrase.

A new cue replaces any existing cue for that track.

## Cue markers

- `+` = Chain-boundary cue.
- `*` = Phrase-boundary cue.

## Timing

LIVE mode uses the existing tracker frame/sequencer clock; no independent audio timer is introduced. LIVE columns share a 16-step musical downbeat:

- The first active LIVE column becomes the timing anchor.
- New LIVE columns wait for the next shared downbeat instead of starting at an arbitrary phrase row.
- Phrase cues switch at the shared 16-step downbeat.
- Normal Chain cues still wait for the end of the currently playing Chain, but the transition is quantized to the shared downbeat.
- If a column was started or cued while another column was already part-way through a phrase, it is aligned to phrase row `0` on the next shared downbeat.

The selected LIVE Chain correctly advances through all of its Chain rows before looping. This preserves the intended independent Chain selection per column while keeping the columns musically aligned.

## Notes

The current implementation is intentionally limited to per-column Chain selection and per-column cues. Whole-row CUE and additional UI polish are left for a later phase.
