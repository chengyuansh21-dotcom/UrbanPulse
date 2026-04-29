---
name: image-to-editable-ppt
description: Generate one or more images with Codex image generation, then build an editable PowerPoint deck that uses the images as visual assets while keeping slide text, shapes, tables, charts, and layout editable. Use when the user asks to turn generated images, image prompts, storyboards, visual concepts, or AI image outputs into PPT/PPTX slides.
---

# Image To Editable PPT

Use this skill when a user wants to generate images and turn them into an editable PowerPoint deck, especially when they mention image generation, gpt-image-2, image-2, generated pictures, visual slides, storyboard slides, PPT, PPTX, or editable presentation.

## Required companion skills

- Use `imagegen` first for raster image generation or image editing.
- Use `Presentations` after the images are selected to create or edit the `.pptx`.

## Core principle

The deck must be editable PowerPoint content. Generated images may be embedded as raster assets, but titles, body text, labels, callouts, arrows, shapes, tables, charts, and layout elements should be authored as presentation-native objects whenever possible.

Do not export a flat screenshot of a full slide and place it into PowerPoint unless the user explicitly asks for a non-editable mockup.

## Workflow

1. Clarify or infer the deck goal: audience, topic, slide count, tone, aspect ratio, and whether the output is a full deck or one slide.
2. Convert the request into an image plan: one prompt per image asset, with each asset's role in the deck.
3. Generate images with the default `imagegen` built-in path unless the user explicitly asks for CLI/API/model controls.
4. Save final image assets into the current workspace before using them in the deck.
5. Build the PPTX with the `Presentations` skill and presentation-native primitives:
   - image assets for hero visuals, backgrounds, product shots, illustrations, scene panels, or storyboard frames
   - editable text for all slide copy
   - editable shapes for masks, callouts, labels, arrows, dividers, and layout structure
   - editable charts or tables when the slide contains data
6. Render the deck to PNG previews and inspect the slides for text clipping, overlap, missing images, and poor crops.
7. Return the `.pptx` path, preview path or paths, image asset paths, and a short note about editability.

## Image prompting rules

For each generated image, include:

```text
Use case: productivity-visual or ads-marketing or illustration-story
Asset type: PowerPoint slide visual asset
Primary request: <specific image description>
Composition: leave negative space where slide text or callouts will sit
Text in image: none, unless the user explicitly requires exact text
Output needs: high-resolution raster image suitable for a 16:9 presentation
Avoid: watermarks, UI text, unreadable pseudo-text, logos unless supplied or requested
```

Prefer generating images without embedded text. Add text later as editable PowerPoint text.

## PPT construction rules

- Keep generated images separate from editable overlay objects.
- Use masks, crops, and overlays in the presentation layer instead of baking layout into the image when practical.
- Put slide copy, titles, page numbers, labels, legends, and callouts in native text boxes.
- If a generated image includes accidental text or artifacts, regenerate or crop it; do not rely on it as important slide content.
- For multi-slide decks, keep a consistent visual system across images: palette, lighting, perspective, aspect ratio, and subject style.
- Keep final deliverables and generated images in the user's workspace. Do not leave project-referenced image assets only under `$CODEX_HOME/generated_images`.

## Output checklist

Before finishing, confirm:

- The generated image assets exist in the workspace.
- The `.pptx` opens as a presentation file and is not just a collection of screenshots.
- Core slide content is editable: text, shapes, labels, tables, and charts where applicable.
- Rendered previews show no missing images, clipped text, or incoherent overlap.
- The final response includes the PPTX path, preview path, test or inspection status, and any unresolved issues.
