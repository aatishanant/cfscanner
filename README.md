# CrownfallScanner — scanner foundation (no AI/API)

Target: Paper 26.3, Java 25.

## Command
`/cfscan <world> <centerX> <centerZ> <width>`

The width is the full X/Z width of the square; the scanner uses the world's full vertical height. It processes one chunk per tick, skips empty vertical sections, counts non-air materials, and groups occupied blocks into 16x16x16 summary cells. It saves a bounded JSON summary to `plugins/CrownfallScanner/scans/scan-<id>.json`.

## Safety bounds
- Width: 1–1000 blocks.
- Maximum 4096 intersecting chunks.
- Saves up to 80 material types and 5000 occupied cells; aggregate totals still cover all scanned non-air blocks.
- No AI/API calls and no API key.

## Important limitations
- This first foundation is not connected to the Skript empire variables. Coordinates and width must be supplied manually.
- Current blocks alone cannot reliably distinguish player-placed blocks from natural terrain. Before trusting AI build judgments, add a separate block-change journal or terrain-aware structure extraction.
- Scanning loads chunks and can cause server load. Test during a quiet period and make a backup first.

## Build
Use JDK 25 and Gradle (or open in IntelliJ IDEA with Gradle support), then run `gradle build`. The JAR will be in `build/libs/CrownfallScanner-0.1.0.jar`. Stop the server before uploading it to `plugins/`, then restart.
