---
title: "Fixing a tmux Hang on macOS"
date: 2025-03-01
draft: false
tags: ["macos", "tmux", "debugging"]
description: "Tracking down a startup hang caused by the tokyo-night tmux plugin."
---

A quick writeup on how `fabioluciano/tmux-tokyo-night` was causing tmux to hang on launch, and what I'm doing about it.

## The problem

After a macOS update, tmux started hanging on startup. No output, no error — just a frozen terminal.

## The culprit

Bisected my `.tmux.conf` and narrowed it down to the tokyo-night theme plugin. Disabling it restored normal behavior.

## What's next

Still deciding between finding a replacement theme or going with a manual plugin setup instead of TPM. Will update this post when I land somewhere.
