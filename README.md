# PSVE - PractiScore Video Export

PSVE is a desktop video editor for practical shooting match videos. It helps turn long stage recordings into clean clips by finding the timer beep, detecting shots, showing split times, and combining exported clips with PractiScore score cards into a final match video.

The app is designed around a project folder. Scores, imported video state, detected trim points, exported clips, score cards, and final videos are kept together so different matches do not overwrite each other.

## Contact
Feel free to send any feedback at michallasek92@gmail.com
Also feel free to report issues directly in github

## Usage Example
This is a sample video i made in this app, expect your final result to be something like that:
https://youtu.be/9dYnIif2NeM?si=O9AEz9FW1-sXhXrZ


## What It Does

- Extracts shooter score data from a saved PractiScore HTML page.
- Imports multiple stage videos into one project.
- Detects the start point from the timer beep, or falls back to the first shot if no beep is found.
- Detects the last shot and suggests clip start/end times.
- Uses score data, when available, to estimate the minimum number of expected shots per stage.
- Shows split times in the preview and can burn them into exported clips.
- Lets you manually adjust stage number, start/end trim points, sensitivity, and overlay position.
- Builds a final video with overall score card, stage score cards, and exported stage clips.

## Installing

Download and run the installer:

`PSVE Setup 0.1.0.exe`

Windows may warn that the app is from an unknown publisher because early GitHub builds are not code-signed. Choose `More info` and `Run anyway` if you trust the build.

PSVE bundles FFmpeg and FFprobe, so users do not need to install them separately.

## Basic Workflow

1. Create or open a project.
2. Save the shooter's PractiScore page as HTML from your browser.
3. Select that saved HTML file in PSVE and click `Extract Scores`.
4. Select the stage videos for the project.
5. Assign stage numbers to clips if you want score-guided shot detection.
6. Click `Detect Selected` or `Detect All`.
7. Review each clip in the preview.
8. Adjust start/end times if needed.
9. Enable or disable the splits overlay per clip.
10. Drag the splits overlay in the preview to choose where it appears in all clips and exports.
11. Export selected clips, or export all clips.
12. Build the final video.

## Score-Guided Detection

When a clip has an assigned stage number and scores have been extracted, PSVE calculates a minimum expected shot count:

`A + C + D + NS`

The real number of shots can be higher, but should not be lower. PSVE uses this minimum to improve sensitivity suggestions and can automatically use a better sensitivity when the current setting detects too few shots.

You can still run detection without scores or a stage number. PSVE will warn you first because split detection and sensitivity suggestions are less reliable without score guidance.

## Manual Adjustments

- `Set Start From Preview` changes the clip start and recalculates splits from that new start point.
- `Set End From Preview` changes where the exported clip ends.
- `Jump To Start` and `Jump To End` help review trim points quickly.
- The preview pauses once when it reaches the detected end. Press play again to continue past it.
- The clip sensitivity override only affects the selected clip.

## Final Video

The final builder creates:

- an overall score card,
- a score card before each stage,
- exported stage clips from the project `clips` folder,
- a final video named after the project.

PSVE detects the final video resolution and framerate from the first exported stage clip. Score-card slides are generated with that same profile. If no clips have been exported yet, PSVE falls back to 4K 50fps slides.

All exported clips used in the final video must match the same resolution and framerate. If they do not, PSVE stops with a clear error instead of producing a broken concat.

The final output is stored in the project folder.

## Notes

- The app preserves clip resolution and framerate
- Clips without burned-in overlays use stream copy for fast export.
- Clips with burned-in overlays are re-encoded because FFmpeg has to draw the overlay into the video.
- Internet access is currently required for app access verification. Minimal anonymous use data is also sent.
- The app is free in this version, that model might change in the future
