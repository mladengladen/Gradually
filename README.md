# Gradually - Gradient generator

A browser-based gradient generator. Pick two or more colors and Gradually renders dozens of modern gradient variations from them, then exports any one as a high-resolution image or a seamless Instagram carousel.

It's a single HTML file with no build step, no dependencies and no server. Open it in a browser and it runs.

## Features

- **Palette input.** Use 2 to 6 colors, set by color picker or hex code. Mark any color as **BG** to make it the background for the glow-based styles.
- **Extra colors.** Turn 2 colors into a family of 4 to 6. The modes are **Shades** (darker and lighter versions), **Neighbors** (nearby hues) and **Vivid** (bolder hues further around the color wheel). **Another mix** re-rolls the generated colors.
- **Palette ideas.** Suggestions built from your first color (analogous, complementary, triad, tonal, dusk and more), plus 10 curated palettes.
- **15 styles, 4 variations each.** Every style comes in Calm, Bold, Calm with grain and Bold with grain, alongside a row of plain CSS-style linear and radial gradients.
- **Editor.** Open any variation to adjust angle, warp, softness, scale, strength and grain, or to generate a new shape with the same settings.
- **Text contrast check.** Pick the color your text will use and see its WCAG contrast ratio against the gradient's weakest and typical areas.
- **Export formats.** 16:9, 9:16, 4:5 (Instagram) and 1:1.
- **Export resolutions.** 1080p, 2K and 4K, measured on the short side, so 1080p at 4:5 is Instagram's 1080 × 1350.
- **Carousel export.** Choose 2 to 10 slides. The gradient is rendered as one continuous image across all of them, so the slides line up when swiped, and they're saved as a single `.zip`.
- **PNG or JPG.** PNG is lossless. JPG is saved at 95% quality.

### Styles

| Style | What it looks like |
| --- | --- |
| Simple | Plain linear and radial gradients with no texture |
| Muted | A faint haze close to the background color, so text in your palette colors stays readable |
| Mesh | Soft, organic blending between scattered color points |
| Linear | A directional gradient with an optional organic warp |
| Radial | Circular falloff from a movable center |
| Conic | A color sweep around a center point |
| Aurora | Northern-lights curtains over a dark sky |
| Waves | Stacked wave layers with soft shadows |
| Liquid | Marbled, fluid swirls |
| Glow | Soft colored glows on a dark background |
| Fluted glass | A mesh gradient seen through ribbed glass |
| Lava | Rounded, flowing blobs |
| Spotlight | A cone of light shining down from above |
| Horizon | A glowing planet edge, like a sunrise from orbit |
| Corner glow | Light coming in from two opposite corners |
| Light beams | Soft diagonal beams of light |

## Getting started

Clone or download the repository, then open `gradually.html` in a recent version of Chrome, Safari, Edge or Firefox:

```bash
open gradually.html
```

Exports go to your browser's downloads folder. Your colors and settings are saved in the browser's `localStorage`, so the app opens where you left off.

The fonts (Bricolage Grotesque, Instrument Sans and JetBrains Mono) load from Google Fonts. Without an internet connection the app still works and falls back to system fonts.

### Hosting on GitHub Pages

1. Push the repository to GitHub.
2. Go to **Settings → Pages** and choose to deploy from your default branch.
3. The app is then served at `https://mladengladen.github.io/gradually/gradually.html`.

## How it works

- **Rendering.** Every style is a WebGL fragment shader, so previews and full-resolution exports come from the same code. Exports are rendered fresh at the target size, never scaled up from a preview.
- **Color blending.** Colors are mixed in the [Oklab](https://bottosson.github.io/posts/oklab/) color space, which keeps blends vivid instead of turning gray or muddy in the middle. Generated colors are built in OKLCH and adjusted to stay inside the sRGB color range.
- **No banding.** A small amount of random noise (dithering) is added to every pixel before export, so smooth gradients don't show visible steps in 8-bit PNG and JPG files.
- **Large and multi-slide images.** Rendering happens in tiles of up to 2048 px, which keeps 4K images and long carousels within GPU and canvas size limits. Each carousel slide is rendered as its own slice of one large virtual image.
- **Zip files.** Carousel zips are written by a small built-in zip encoder. Files are stored without compression, because PNG and JPG are already compressed.

## Project structure

```
gradually.html   The whole app: markup, styles, shader and script
README.md
```

## Browser support

Gradually needs WebGL, which is supported by every current desktop and mobile browser. If WebGL isn't available, the app shows a message instead of the grid.
# gradually
