# 🕯️ The Forgotten Apartment

> A first-person psychological horror game built in Unity — explore a missing person's apartment, uncover the truth, and survive the night.

![Unity](https://img.shields.io/badge/Unity-2022.3+-black?logo=unity)
![Language](https://img.shields.io/badge/C%23-Scripts-239120?logo=csharp)
![Status](https://img.shields.io/badge/Status-In%20Development-orange)
![Platform](https://img.shields.io/badge/Platform-PC%20%7C%20WebGL-blue)

---

## 📖 About

**The Forgotten Apartment** is a solo-developed horror mystery game set in the abandoned apartment of Aryan Bose — a reclusive artist who vanished 6 months ago. You play as a private investigator with one night to find answers before the building is locked for demolition.

This project is built as a **portfolio piece** demonstrating Unity game development skills including custom physics-based door interaction, NavMesh AI, trigger-based scare scripting, and environmental storytelling.

**Estimated gameplay:** ~30 minutes  
**Genre:** First-person psychological horror / mystery  
**Engine:** Unity (URP)

---

## 🎮 Gameplay Overview

- Explore 6 interconnected rooms of a dark apartment
- Collect journal pages to piece together what happened to Aryan
- Find 3 hidden key fragments to unlock the bedroom
- Solve the **candle ritual puzzle** to confront the truth
- Two possible endings depending on your choices

---

## ✨ Features

### Custom Door System
- Bidirectional push detection — doors open from both sides
- Physics-based interaction using trigger zones and player velocity
- Supports scripted events: auto-open, slam shut, locked state
- Audio integration (open/close sound clips)

### Scripted Horror System (3 tiers)
| Tier | Type | Examples |
|------|------|----------|
| 1 | Ambient | Light flicker, whispers, objects shifting |
| 2 | Scripted scares | Door slams, shadow figure, mirror ghost |
| 3 | Active ghost | NavMesh AI patrol, ritual fail chase |

### Interaction & Puzzle
- Raycast-based first-person interaction (E key)
- Journal pickup and in-game reading UI
- 3-candle sequence puzzle with fail state and retry logic

### Atmosphere
- Diegetic clock (5:00 AM deadline)
- Post-processing: vignette, bloom on candlelight
- Dynamic audio: ambient loops, positional sound triggers

---

## 🗂️ Project Structure

```
Assets/
├── Audio/                  # Ambient, jump scare, music clips
├── BK_AlchemistHouse/      # Main apartment environment asset
├── EasyPeasyFirstPersonCor/# FPS controller
├── Free Wood Door Pack/    # Door mesh variants
├── Lighting/               # Light profiles and baked data
├── Materials/              # Door, floor, wall materials
├── Models/                 # Custom and imported 3D models
├── Prefabs/                # Door prefabs, ghost, interactables
├── PushDoor/               # Door push interaction system
├── Scenes/                 # Main game scene(s)
├── Scripts/                # All C# game logic (see below)
├── Settings/               # URP renderer, post-process profiles
└── Textures/               # UI textures, render textures (mirror)

Scripts/
├── DoorBump.cs
├── DoorInteraction.cs
├── DoorPushZone.cs         # Bidirectional door push detection
├── Door.cs                 # Core door open/close + audio
├── FirstPersonController.cs
├── PlayerInput.cs
├── RE_Door.cs
├── SC_FPSController.cs
├── SimpleDoor.cs
└── SimplePush.cs
```

---

## 🚪 Door System — How It Works

The door system uses two trigger zones per door pivot — one on each side — to detect the player's approach direction and open accordingly.

```
DoorPivotBedRoom1
├── PushZoneInside      ← multiplier: -1  (opens outward)
├── PushZoneOutside     ← multiplier: +1  (opens inward)
├── Door                ← Door.cs + BoxCollider + AudioSource
└── Frame
```

**`Door.cs`** — handles rotation animation and audio  
**`DoorPushZone.cs`** — detects player velocity + facing direction, calls `door.OpenDoor(float direction)`

The `direction` parameter (`+1` or `-1`) flips the open angle, allowing the same pivot to swing either way depending on which zone triggered it.

---

## 🛠️ Setup & Running Locally

### Requirements
- Unity **2022.3 LTS** or newer
- Universal Render Pipeline (URP) package
- Git LFS (for large asset files)

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/the-forgotten-apartment.git

# Open in Unity Hub
# File → Open Project → select the cloned folder
```

> **Note:** This project uses Unity's URP. If materials appear pink/magenta on first open, go to:  
> `Edit → Rendering → Render Pipeline → Upgrade Project Materials to URP`

### First Run
1. Open `Assets/Scenes/MainApartment` in Unity
2. Press **Play** in the Unity Editor
3. Use `WASD` to move, `Mouse` to look, `E` to interact

---

## 🎮 Controls

| Key | Action |
|-----|--------|
| `W A S D` | Move |
| `Mouse` | Look |
| `E` | Interact / pick up |
| `Esc` | Pause menu |
| `Left Shift` | Sprint |

---

## 📦 Assets Used

| Asset | Source | Usage |
|-------|--------|-------|
| BK Alchemist House | Unity Asset Store | Main apartment scene |
| Vintage Living Room 3D | Unity Asset Store | Act 1 props |
| Free Wood Door Pack | Unity Asset Store | All door meshes |
| Magic Effects FREE | Unity Asset Store | Candle VFX, ghost dissolve |
| EasyPeasy FPS Controller | Unity Asset Store | Player controller |
| Horror ambience clips | freesound.org (CC0) | Ambient audio |

---

## 🗺️ Development Roadmap

- [x] First-person controller setup
- [x] Basic door open/close system
- [x] Bidirectional door push (both sides)
- [x] Apartment scene layout (BK Alchemist House)
- [ ] Interact system (raycast E-key pickup)
- [ ] Journal pickup + reading UI
- [ ] Key fragment collection system
- [ ] Locked bedroom door logic
- [ ] Scripted scares (door slam, light flicker, mirror event)
- [ ] Ghost AI (NavMesh patrol)
- [ ] Candle ritual puzzle
- [ ] Diegetic clock (5 AM deadline)
- [ ] Both endings (escape / trapped)
- [ ] Post-processing polish pass
- [ ] Main menu + pause menu
- [ ] WebGL build for itch.io

---

## 🏗️ Architecture Notes

### GameManager (planned)
Singleton that tracks global state: key fragments collected, notes found, ritual attempts, current act, and ending trigger.

### Scare Trigger System (planned)
`ScriptedScare.cs` attached to invisible trigger volumes. Each scare has a type enum (`DoorSlam`, `ShadowFigure`, `LightFlicker`, `MirrorEvent`), a one-shot flag to prevent repeats, and optional delay.

### Ghost AI (planned)
NavMesh agent with three states: `Idle`, `Patrol`, `Chase`. Transitions to `Chase` on failed ritual attempt. Player detected via line-of-sight raycast.

---

## 📸 Screenshots

> *(Will be added as development progresses)*

---

## 👤 Developer

**Saqib Shakil**  
Full Stack Developer & Unity Game Dev  
📍 Kolkata, India

- Portfolio: [saqib-shakil-portfolio.vercel.app](https://saqib-shakil-portfolio.vercel.app)
- GitHub: [@SaqibShakil303](https://github.com/SaqibShakil303)
- LinkedIn: [linkedin.com/in/saqib-shakil303](https://linkedin.com/in/saqib-shakil303)

---

## 📄 License

This project is for **portfolio and educational purposes**.  
Third-party assets are subject to their respective Unity Asset Store or original licenses and are not redistributed in this repository.

---

*"Don't let it keep you too." — Aryan Bose, Journal Entry #7*
