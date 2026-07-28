# 🎵 Scale Notes — Musical Scale Memorization Trainer

An interactive, high-performance web application designed to help musicians, producers, and music theory students learn, practice, and master note spelling across 14 scale types in all 12 musical keys.

Built with **Astro**, **Tailwind CSS v4**, and the native **Web Audio API**.

---

## ✨ Features

- **Guided 3-Step Setup**: Effortlessly select a root note, pick a scale formula, preview notes, and choose quiz settings (such as random order shuffling).
- **Interactive Learn Mode**:
  - Visual note cards displaying scale degrees (`1st`, `♭3rd`, `5th`, etc.).
  - 2-octave interactive **Piano Visualizer** showing scale positions on key layouts.
  - Interval pattern breakdown (Half steps `H`, Whole steps `W`, Whole+Half `W+H`).
  - Audio playback for individual notes and full scale ascending sequences.
- **Interactive Quiz Mode**:
  - Degree-by-degree testing with 12-key multiple choice responses.
  - Real-time visual and audio feedback on correct/wrong answers.
  - Active streak & best streak tracking persisted via `localStorage`.
  - Keyboard shortcuts (`C`, `D`, `E`, `F`, `G`, `A`, `B`) for fast responsive quizzing.
- **Comprehensive Results Screen**:
  - Animated SVG circular score percentage display.
  - Total duration time tracking and correct/wrong counts.
  - Missed notes breakdown highlighting target degrees, user answers, and correct answers.
- **14 Supported Scale Formulas**:
  - Major (Ionian), Natural Minor (Aeolian), Harmonic Minor, Melodic Minor (asc.)
  - Modes: Dorian, Phrygian, Lydian, Mixolydian, Locrian
  - Pentatonics & Special: Major Pentatonic, Minor Pentatonic, Blues, Whole Tone, Diminished (H-W)

---

## 🏗️ Architecture & Technical Stack

### Core Technologies

- **Framework**: [Astro v5](https://astro.build/) — Static Site Generation (SSG) for fast initial load times.
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/) — Native CSS theme configuration (`@theme`) with custom OKLCH color palettes, note degree highlights, glassmorphism UI tokens, and keyframe animations.
- **Audio Engine**: **Web Audio API** — Zero-dependency, client-side synthesized piano sound generator.
- **Typography**: Google Fonts (`Inter` for UI layout and `JetBrains Mono` for numerical degree data and metrics).

### Application Architecture

The app is architected as a lightweight Single-Page Application (SPA) embedded within an Astro static frame:

```
src/
├── layouts/
│   └── Layout.astro         # Base HTML shell, metadata, Google Fonts, theme setup
├── pages/
│   └── index.astro          # Main entry route rendering ScaleTrainer
├── components/
│   └── ScaleTrainer.astro   # Monolithic interactive component (UI + State + Audio)
└── styles/
    └── global.css           # Tailwind v4 import, OKLCH color design system & keyframe animations
```

#### Component & Screen Flow (`ScaleTrainer.astro`)

`ScaleTrainer.astro` houses both the responsive markup for all 4 application screens and the client-side vanilla TypeScript/JS driver:

1. **Setup Screen (`#screen-setup`)**:
   - **Step 1**: Root Note grid selection (12 chromatic pitch roots).
   - **Step 2**: Scale selection list (14 formulas with note counts).
   - **Step 3**: Confirmation panel, clickable note preview, and random order shuffle toggle.
2. **Learn Screen (`#screen-learn`)**:
   - Interactive note cards, 2-octave piano keyboard canvas, interval step sequence, and full scale audio auditioning.
3. **Quiz Screen (`#screen-quiz`)**:
   - Step progress bar, degree prompt, 12-note answer grid, keyboard event listeners, and animated visual feedback.
4. **Results Screen (`#screen-results`)**:
   - SVG circle stroke animation, summary metrics, missed note diagnostic list, and session retry handles.

#### Music Theory & Data Engine

- **Note Calculation**: Calculates pitch indices relative to standard 12-tone equal temperament (12-TET).
- **Enharmonic Spelling**: Automatically maps sharp/flat note naming based on key signature conventions (e.g., flat notation for `F`, `Bb`, `Eb`, `Ab`, `Db`, `Gb`).
- **Interval Mapping**: Formula arrays convert semitone jumps into scale note degrees and standard interval labels.

#### Web Audio API Sound Synthesizer

The sound generator creates warm, piano-like tones directly in the browser without loading external audio assets:
- **Triple-Oscillator Additive Synthesis**:
  - Oscillator 1: Triangle wave for the fundamental frequency.
  - Oscillator 2: Sine wave at 2x frequency (1st overtone) for brightness.
  - Oscillator 3: Sine wave at 3x frequency (2nd overtone) for subtle shimmer.
- **ADSR Envelope**: Real-time gain ramps shaping Attack (8ms), Decay (80ms), Sustain, and Exponential Release for natural acoustic decay.

---

## 📁 Directory Structure

```text
MemorizeScaleNotes/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions workflow for automatic GitHub Pages deployment
├── public/
│   └── favicon.svg             # App favicon asset
├── src/
│   ├── components/
│   │   └── ScaleTrainer.astro  # Interactive scale memorization trainer component
│   ├── layouts/
│   │   └── Layout.astro        # App root layout, SEO metadata, fonts
│   ├── pages/
│   │   └── index.astro         # Root page route
│   └── styles/
│       └── global.css          # Tailwind CSS v4 design system tokens & animations
├── astro.config.mjs            # Astro configuration (base path & Tailwind Vite plugin)
├── package.json                # Project dependencies and scripts
├── README.md                   # Project documentation
└── tsconfig.json               # TypeScript configuration
```

---

## 🚀 Development & Commands

All commands are run from the root of the project:

| Command | Action |
| :--- | :--- |
| `npm install` | Installs project dependencies |
| `npm run dev` | Starts local development server at `http://localhost:4321` |
| `npm run build` | Builds static production bundle into `./dist/` |
| `npm run preview` | Previews the built production site locally |
| `npm run astro ...` | Runs Astro CLI helper commands |

---

## 🌐 Deployment

The project is configured for automated CI/CD deployment to **GitHub Pages** via GitHub Actions (`.github/workflows/deploy.yml`). On every push to the `main` branch, the site is compiled with `astro build` and published automatically.
