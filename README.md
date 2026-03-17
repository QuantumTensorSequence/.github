# Quantum Tensor Sequence

**A universal compression format that understands your data.**

---

## What is .qtsq?

Most compression tools — ZIP, GZIP, 7z — look at your data as a raw stream of bytes. They don't know or care whether you're compressing a photograph, a song, or a spreadsheet. They just look for repeating patterns and call it a day. That approach works, but it misses a lot.

A photograph is full of self-similar textures. An audio file is mostly a handful of frequencies repeating over time. A CSV file is structured columns of numbers. Each of these has a mathematical structure that a generic byte-level compressor can't take advantage of.

**.qtsq** (Quantum Tensor Sequence) is a file format designed around one idea: **look at the data first, then pick the right compression strategy for it.**

When you feed a file into the .qtsq compressor, an internal component called the **Spaghettification Engine** runs a three-stage analysis — checking file signatures, analyzing text characteristics, and measuring entropy — to classify the data into one of 16 types. Based on that classification, it routes the data to the mathematically appropriate compression strategy:

| Data Type | Compression Strategy | How It Works |
|---|---|---|
| 📷 Images | Iterated Function Systems (IFS) | Exploits self-similar patterns across the image at different scales |
| 🎵 Audio & Signals | Discrete Fourier Transform (DFT) | Keeps only the frequency components that carry meaningful energy |
| 📝 Text, CSV, JSON | Dictionary + Schema Encoding | Builds pattern tables and encodes values relative to statistical baselines |
| 💾 Generic Binary | Procedural Seed Compression | Searches for a PRNG seed that produces the most compressible XOR residual |
| 🎬 Video | Temporal Delta + Fractal | Inter-frame differences with fractal keyframes |

The name "Spaghettification" comes from the tidal stretching effect that occurs near a black hole — the idea that data gets pulled apart and analyzed before being compressed into its densest possible form.

## More than just compression

A single .qtsq file handles a lot more than just making data smaller. The format packs 11 features into an 80-byte header:

### 🔐 Security
- **AES-256-GCM encryption** — Industry-standard authenticated encryption with PBKDF2 key derivation (100,000 iterations). The file metadata stays readable so you can inspect file type and dimensions without the key, but the actual data is fully protected.
- **Schnorr zero-knowledge proofs** — You can cryptographically prove that you own a file or know the password without ever revealing the password or the data to the verifier. This is useful for things like proving file ownership in disputes or authorizing access across wormhole links.

### 🛡️ Reliability
- **Reed-Solomon error correction** — Parity data is embedded directly in the file, so if part of the file gets corrupted (bad sectors, transfer errors, bit rot), it can correct itself automatically. The overhead is configurable — by default it's 10% of the compressed data size.
- **Per-chunk CRC-32 checksums** — Every section of the file can be independently verified for integrity.

### 🔗 Smart Storage
- **Wormhole links** — If two .qtsq files share common data (like photos from the same location sharing similar sky gradients), one file can reference the other instead of storing the data twice. Works locally, over LAN, or via remote URLs.
- **Gravitational wave updates** — When a file changes, instead of rewriting the whole thing, the system generates a small .qtsw patch file containing just the differences in the compressed domain. Other copies can apply the patch to sync up.

### 🎚️ Flexibility
- **Multi-resolution output (Redshift/Blueshift)** — Decompress at any quality level from thumbnail to full resolution, all from a single file. Useful for progressive loading and bandwidth-adaptive streaming.
- **Lazy partial decompression** — An internal index lets you decompress specific sections of the file without reading the whole thing.
- **Chandrasekhar Limit** — Files below 4KB are stored uncompressed, because at that size the compression overhead would be larger than the savings.

## Architecture

The format is structured around a five-layer model drawn from black hole physics. This isn't just a naming theme — the layers give a natural order to how data flows through the pipeline:

```
┌─────────────────────────────────────────────┐
│  Layer 1: EVENT HORIZON                     │
│  Header + Schema · 80 bytes · Type info     │
│  ┌─────────────────────────────────────┐    │
│  │  Layer 2: ACCRETION DISK            │    │
│  │  Transform Pipeline · Compression   │    │
│  │  ┌─────────────────────────────┐    │    │
│  │  │  Layer 5: PHOTON SPHERE     │    │    │
│  │  │  Error Correction · CRC     │    │    │
│  │  │  ┌─────────────────────┐    │    │    │
│  │  │  │  Layer 3: SINGULARITY│   │    │    │
│  │  │  │  Compressed Core     │   │    │    │
│  │  │  └─────────────────────┘    │    │    │
│  │  └─────────────────────────────┘    │    │
│  └─────────────────────────────────────┘    │
│  Layer 4: HAWKING RADIATION                 │
│  Lazy decompression index                   │
└─────────────────────────────────────────────┘
```

Data enters through the Event Horizon (where it's classified), spirals through the Accretion Disk (where it's transformed and compressed), and collapses into the Singularity (the compressed core). Decompression runs the process in reverse.

## QTSQ Studio

We've built a macOS application — **QTSQ Studio** — that lets you compress files into .qtsq format and view them directly:

- **Image files** render in full color with the Gravitational Field Compression engine
- **Audio files** play back through a built-in waveform visualizer
- Drag-and-drop interface for quick compression
- Side-by-side comparison of original vs compressed file sizes

## Research

The format specification is described in detail in our preprint paper:

> **"Quantum Tensor Sequence: A Universal Data Compression Format with Physics-Inspired Architecture, Zero-Knowledge Verification, and Self-Healing Recovery"**
>
> Haruhito · Independent Researcher · March 2026

A second paper covering **Gravitational Field Compression** — a new strategy based on Wendland C² radial basis functions adapted from computational physics — is currently in preparation.

## Current Status

- ✅ Reference implementation in C (portable, no external dependencies)
- ✅ macOS app (QTSQ Studio) for compression and viewing
- ✅ Image compression with Gravitational Field Compression
- ✅ Audio compression with 1D Gravitational Field Compression
- ✅ Full encryption and zero-knowledge proof support
- 🔧 Benchmarking suite (in progress)
- 📋 Python, Rust, and WebAssembly bindings (planned)

## License

**Quantum Tensor Sequence Proprietary License (QTSPL) v1.0**

Free for personal, educational, and academic research use. Commercial use, distribution, modification, and creation of compatible or competing implementations require written authorization from the author.

See [LICENSE](LICENSE) for the complete terms.

---

*Built by Haruhito · Copyright © 2026 Haruhito. All Rights Reserved.*
