# Publishing

This repo is designed to be compatible with the `skills` CLI and skills.sh-style skill folders.

## Prerequisites
- A GitHub repo under `zhyGuGu` (recommended name: `agent-skills-collection`).

## Publish Steps (GitHub)
1. Create the repository in the GitHub UI:
   - Owner: `zhyGuGu`
   - Name: `agent-skills-collection`
   - Visibility: Public
2. Add a git remote and push:
   - `git remote add origin https://github.com/zhyGuGu/agent-skills-collection.git`
   - `git push -u origin main`

## Verify Installability
From any machine with Node:
- List available skills:
  - `npx skills add zhyGuGu/agent-skills-collection --list --full-depth`
- Install one skill:
  - `npx skills add https://github.com/zhyGuGu/agent-skills-collection/tree/main/skills/accessibility-audit`

## Publish to skills.sh
Skills appear on skills.sh automatically via anonymous telemetry when users run `npx skills add <owner>/<repo>`.

Docs reference:
- https://skills.sh/docs/faq

To trigger initial visibility, have a few people install:
- `npx skills add zhyGuGu/agent-skills-collection`

Repository URL:
- https://github.com/zhyGuGu/agent-skills-collection
