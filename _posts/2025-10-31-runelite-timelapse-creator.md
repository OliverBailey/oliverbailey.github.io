---
layout: post
title: "RuneLite Timelapse Creator"
image: ''
date: 2025-10-31 12:00:00
tags:
- osrs
- runelite
- python
- open-source
description: 'Create awesome timelapse videos from your RuneLite screenshots'
categories:
- projects
---

# RuneLite Timelapse Creator

I've created an open-source tool that automatically creates timelapse videos from your RuneLite screenshots! 

## What It Does

If you play Old School RuneScape with RuneLite, you probably have hundreds (or thousands) of screenshots scattered across different folders. This tool:

- 📸 Automatically finds and sorts all your screenshots by timestamp
- 🎵 Adds background music (Sea Shanty 2 included!)
- 🔒 Blurs your chatbox to protect privacy
- ⚡ Uses GPU acceleration for fast encoding
- ⚙️ Fully customizable via `.env` configuration

## Features

- **Automatic screenshot discovery** - Recursively scans all RuneLite screenshot folders
- **Chronological sorting** - Sorts by the timestamp in the filename
- **Privacy protection** - Configurable chatbox blurring
- **Music support** - Add background music with two playback modes
- **GPU acceleration** - Auto-detects NVIDIA/AMD/Intel GPUs for 5-10x faster encoding
- **Smooth playback** - Separate controls for screenshot pacing vs. video smoothness
- **Quality control** - Adjustable video quality/bitrate settings

## Technical Details

Built with Python and FFmpeg, featuring:
- Environment-based configuration (`.env` files)
- Automatic GPU encoder detection with CPU fallback
- Configurable frame interpolation for smooth playback
- Support for variable screenshot rates while maintaining smooth video output

## Get Started

Check out the project on GitHub:

**[github.com/OliverBailey/runelite-timelapse](https://github.com/OliverBailey/runelite-timelapse)**

Perfect for creating montages of your OSRS journey, showing account progress, or just looking back on your adventures!

---

*MIT Licensed - Free to use and modify*
