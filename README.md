# UrbanPulse Codex Skills

This repository currently contains a Codex skill for turning AI-generated images into editable PowerPoint decks.

## Skill: image-to-editable-ppt

`image-to-editable-ppt` guides Codex through a two-step workflow:

1. Generate one or more raster images with the built-in image generation workflow.
2. Build an editable `.pptx` deck where generated images are used as visual assets, while slide text, labels, shapes, tables, charts, and layout elements remain PowerPoint-native and editable.

The skill is useful for requests such as:

- Generate future-city images and create a Chinese PPT proposal.
- Turn visual concept prompts into an editable presentation.
- Build storyboard-style decks where images are backgrounds or scene panels, but copy remains editable.

## Repository Layout

```text
skills/
  image-to-editable-ppt/
    SKILL.md
    agents/
      openai.yaml
```

## Install

Use Codex skill installation from this repository path:

```text
chengyuansh21-dotcom/UrbanPulse:skills/image-to-editable-ppt
```

After installing, restart Codex so the new skill is picked up.

## Example Prompt

```text
Use $image-to-editable-ppt to generate 5 future-city style images and create a 6-page editable Chinese PPT titled AI Smart City Solution.
```

## Editability Notes

The intended output is not a flat screenshot deck. Generated images should be embedded as image assets, while important presentation content should remain editable:

- Titles and body copy: native text boxes
- Labels and callouts: native text and shapes
- Diagrams: native shapes where practical
- Data: native charts or editable tables when applicable
- Generated images: background, hero, scene, or concept assets

## Example Assets

A local example deck was created during development:

- `ai-smart-city-solution.pptx`
- five generated future-city PNG assets
- one preview montage PNG

Large binary examples are not currently committed here because the active GitHub connector path used by Codex in this session supports text uploads directly, while binary example upload requires a normal Git push or a binary-capable upload path.
