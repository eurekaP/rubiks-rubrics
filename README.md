# Rubik's Rubrics

A stunning (if I do say so myself), self-contained 3D Rubik's Cube visualizer and solver. Scan your
real cube with your webcam and watch it come to life on screen, then sit back as it shows you exactly
how to solve it with smooth, eased layer-turn animations. Or let a random scramble appear and solve
itself. Either way, you control the show.

**▶ Live demo:** https://leereilly.net/rubiks-rubriks/

![](screenshot.webp)

## Features

- **Random scramble:** the cube shows up in a random state every time.
- **Scan a real cube with your webcam:** turn on your camera, hold up a physical cube
  face by face, and the browser reads the colors and shows the detected layout as an
  editable net. Color detection isn't perfect, so depending on your lighting, camera
  quality, and how the cube catches the light, a sticker or two might get read wrong.
  No big deal: just tap any sticker on the net to cycle it to the right color before
  solving. Once it looks right, it solves the cube so you can watch it unscramble.
- **Animated solve:** watch it unscramble with buttery, eased quarter-turn animations.
- **Speed slider:** go from a slow crawl to turbo.
- **Timeline scrubber + transport:** scrub anywhere between *Scrambled* and *Solved*,
  step a single move back/forth, jump to either end, or play/pause.
- **GitHub contributions mode:** repaint the stickers as GitHub contribution-graph
  squares (those familiar greens).
- **Auto-rotate**, orbit (drag), and zoom (scroll) for a showcase feel.
- **Stunning rendering:** physically based glossy stickers, image-based reflections,
  soft contact shadows, and subtle bloom.

## How it works

The cube starts solved, then a random sequence of quarter turns scrambles it. The
solution is simply that sequence **reversed and inverted**, so every solve is valid by
construction, no solver library required. State is tracked as a small logical model
(each cubie's grid position + orientation quaternion), which keeps scrubbing
frame-perfect and drift-free.

A cube you **scan** with your webcam can be in any state, so that path uses a real
solver: [cubejs](https://github.com/ldez/cubejs) (Herbert Kociemba's two-phase
algorithm) runs in a Web Worker, loaded straight from a CDN. All 54 stickers are matched
against the six scanned center colors in a hue/saturation space (brightness is ignored, so
glare and uneven lighting don't wash them out) and then balanced so each color appears
exactly nine times, which fixes systematic misreads like red-vs-orange and guarantees a
legal cube. If the automatic read still gets a sticker wrong, you can fix it by hand on
the net before solving. The solution it returns is fed through the same
reverse-and-invert machinery, and the visualizer plays it back.

## Kudos

Made with ♥ and [GitHub Copilot](https://github.com/features/copilot), Claude Opus 4.8, [three.js](https://threejs.org/) + [cube.js](https://github.com/ldez/cubejs) 

## License

[MIT](LICENSE)
