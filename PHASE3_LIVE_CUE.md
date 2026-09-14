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

No independent timer or playback clock is introduced. Both cue types are handled by the existing tracker frame/sequencer path:

- Phrase cue is consumed at the existing phrase boundary.
- Chain cue is consumed only when the current Chain has no further Chain rows.

The selected LIVE Chain now correctly advances through all phrases in the Chain before looping. This also fixes the Phase 2 behavior that would otherwise restart at Chain row 0 at every phrase boundary.

## Notes

The current implementation is intentionally limited to per-column Chain selection and per-column cues. Whole-row CUE and additional UI polish are left for a later phase.
