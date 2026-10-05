# MediaPipe für die KI-Freistellung (Reel-Studio)

Diese Dateien braucht `reel_segment.js`, damit die Person ohne grünes Tuch freigestellt wird.
Alles läuft im Browser; es wird kein Bild hochgeladen. Nichts davon ist eine Zugangsdatei.

| Datei | Zweck | Größe |
|---|---|---|
| `vision_bundle.mjs` | MediaPipe Tasks Vision, JavaScript-Bündel | 155.439 Bytes |
| `wasm/vision_wasm_internal.js` | Lader für die Rechenbibliothek (mit SIMD) | 323.377 Bytes |
| `wasm/vision_wasm_internal.wasm` | Rechenbibliothek (WebAssembly, mit SIMD) | 11.756.954 Bytes |
| `wasm/vision_wasm_nosimd_internal.js` | Lader für ältere Browser ohne SIMD | 323.180 Bytes |
| `wasm/vision_wasm_nosimd_internal.wasm` | Rechenbibliothek für ältere Browser ohne SIMD | 10.960.242 Bytes |
| `selfie_segmenter.tflite` | KI-Modell „Selfie Segmenter“ (Person/Hintergrund, 256×256, float16) | 249.537 Bytes |

Gesamt: 23.768.729 Bytes (rund 22,7 MiB). Der Browser lädt je Besuch nur eine WASM-Variante
(etwa 12 MB), danach greift der Browser-Cache.

## Quelle und Version
- Paket `@mediapipe/tasks-vision`, Version **1.0.1** (npm, geladen am 05.10.2026 über
  `https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@1.0.1/`).
- Modell `selfie_segmenter.tflite` von
  `https://storage.googleapis.com/mediapipe-models/image_segmenter/selfie_segmenter/float16/latest/selfie_segmenter.tflite`
  (Google, Modellkarte: https://developers.google.com/mediapipe/solutions/vision/image_segmenter).
- Nicht mitgenommen: die `_module_`-Varianten der WASM-Dateien (werden nur mit `useModule = true` gebraucht).

## Lizenz
Bündel, WASM und Modell: **Apache License 2.0**, Copyright Google LLC.
Text der Lizenz: https://www.apache.org/licenses/LICENSE-2.0

## Aktualisieren
Neue Version holen: die sechs Dateien mit `curl` von den Adressen oben laden (Version im Pfad ändern),
dann `VERSION` in `reel_segment.js` anpassen. Bündel und WASM müssen immer dieselbe Version haben.
Fällt der Ordner weg, lädt `reel_segment.js` dieselbe Version vom CDN (nur mit Internet).
