# BHARAT 360 — Indian Heritage Virtual Museum

A lightweight, browser-based heritage museum built on the original Neural Nexus A-Frame project. It retains the existing single-room gallery, WASD/mouse camera, three section navigation, seven paintings, exhibit information panels, and guided tour. The central rotunda now presents a locally stored, rotating Nataraja scan; the Art & Culture alcove includes a stationary Khmer Ganesha scan.

## Run locally

From this project directory:

```sh
python3 -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000). Use a local HTTP server rather than opening `index.html` as a `file://` URL so WebGL, GLB and image assets load correctly.

## Controls and features

- Select **Start Exploring** on the welcome screen.
- Move with **W A S D**, look with the mouse, and zoom with the mouse wheel.
- Use **Ancient India**, **Architecture & Monuments**, and **Art & Culture** to move to a section.
- Click any framed painting or either 3D sculpture to open its historical information. If a click is difficult, use **Browse Exhibits · Info** and choose the exhibit from the catalogue.
- Close an information panel with **Close** or **Escape**.
- Use **Start Guided Tour**, then **Next**, **Previous**, and **Exit Tour**. The nine stops include all seven paintings and both sculptures.

## Scene implementation

The room, interface, exhibit records, click handling and tour remain in `index.html`. Artwork planes are sized after A-Frame's local image assets load. They use the source image's natural dimensions and fit within a 2.884 × 2.156 metre maximum, with matching inner mats and frame borders; this reduces the former artwork scale by 30% without stretching or cropping the artwork.

The central sandstone and brass plinth supports the Nataraja at approximately 0.96 m above its top. Its scene graph separates a fixed pedestal anchor, a zero-offset rotating pivot, and a fitted GLB child. The fitted centering offset stays on the GLB child, so only the pivot turns (one revolution in about 63 seconds). The side pedestal in Art & Culture supports the stationary Ganesha. Both sculptures have separate exhibit records, clickable mesh entities, spot lighting and their own tour entries.

Section switching, catalogue selection and tour navigation share the same exhibit IDs and section keys. Camera pose is set on the existing rig and the camera's local look offsets are reset on section changes. No backend or additional runtime framework is used.

## 3D model credits and licences

- `assets/models/nataraja-scan.glb` — *Siva Nataraja at the Guimet Museum, Paris*, 3D scan by Scan the World, distributed through [Zenodo record 21161898](https://zenodo.org/records/21161898) under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). This licence requires attribution, sharing adaptations under the same licence, and non-commercial use. The model's original geometry and textures are retained; the application applies a restrained bronze material tint.
- `assets/models/ganesha-guimet-scan.glb` — Guimet Museum Ganesha scan by Scan the World, downloaded from the optimized `normalized_optimized-0.500` model record at [Zenodo](https://zenodo.org/records/21690572), under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). The model is the Khmer sandstone Ganesha from near Srah Ta Set, Angkor Thom (now Musée Guimet, Paris), dated to the late 12th–early 13th century. Its local filename is retained in `assets/models/`; the model is used with attribution and the source licence applies.

Both scans use Draco compression. The existing local decoder in `assets/vendor/draco/` avoids a remote decoder request (Google Draco, Apache License 2.0). Model and image assets load from this project; A-Frame 1.5.0 remains vendored at `assets/vendor/aframe.min.js` under its MIT licence.

## Artwork image credits

| File | Credit | Licence |
|---|---|---|
| `assets/ajanta-painting.jpg` | The Yorck Project (2002), via Wikimedia Commons | Public domain |
| `assets/sarnath-lion-capital.jpg` | Chrisi1964, via Wikimedia Commons | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| `assets/padmapani-ajanta.jpg` | SpeakingArch, via Wikimedia Commons | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| `assets/taj-mahal.jpg` | Steve Evans, via Wikimedia Commons | [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) |
| `assets/konark-sun-temple.jpg` | Raveesh Vyas, via Wikimedia Commons | [CC BY-SA 2.0](https://creativecommons.org/licenses/by-sa/2.0/) |
| `assets/virupaksha-hampi.jpg` | Jirijindra, via Wikimedia Commons | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) |
| `assets/madhubani-paintings.jpg` | Mohitkiran, [Madhubani painting](https://commons.wikimedia.org/wiki/File:Madhubani_painting.jpg), via Wikimedia Commons | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) |

The original Neural Nexus project licence terms and attribution are preserved; the source checkout contains no separate top-level `LICENSE` file. Individual media licences above continue to apply to their respective assets.
