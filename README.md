# 🧪 Periodic Table Cipher Studio

[![License: MIT](https://img.shields.io/badge/License-MIT-emerald.svg)](LICENSE)
[![Vanilla JS](https://img.shields.io/badge/Tech-Vanilla%20JS%20%7C%20HTML5-blue.svg)](index.html)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-0-green.svg)](index.html)

A deterministic, fixed-width substitution cipher engine that encodes arbitrary English text into chemical atomic numbers and decodes contiguous numeric streams back into clean, sentence-cased language.

---

## 📌 Repository Description (for GitHub About Section)

> **About:** A deterministic 3-digit periodic table substitution cipher and interactive decoder built with zero-dependency vanilla JavaScript and HTML5.  
> **Topics:** `periodic-table`, `cipher`, `encoder-decoder`, `vanilla-javascript`, `stem`, `cryptography-toy`, `zero-dependencies`

---

## 💡 The Concept

Words and personal names often overlap with chemical element symbols. For instance, **RUCHIR** decomposes cleanly into:
* **Ru** (Ruthenium, atomic number `44`)
* **C** (Carbon, atomic number `6`)
* **H** (Hydrogen, atomic number `1`)
* **Ir** (Iridium, atomic number `77`)

While turning this into a simple mapping is straightforward, building a **deterministic, bidirectional cipher** creates parsing challenges:

1. **The Lookahead Problem (Variable-Width Tokens):** Chemical symbols can be 1 or 2 characters long (e.g., `S` + `C` vs `Sc`).
2. **The Digit-Length Ceiling:** Atomic numbers span 1 to 3 digits (`1` to `118`), creating boundary collisions when reading a flat digit stream.
3. **The Alphabet Gap:** Exactly 12 English letters (**A, D, E, G, J, L, M, Q, R, T, X, Z**) do not exist as standalone single-letter elements.

---

## 📐 The 3-Digit Protocol Specification

To make tokenization and decoding strictly $O(N)$ with zero ambiguity, the engine enforces a uniform **3-digit fixed-width chunking standard**:

```
[ Plaintext Input ]
         │
         ▼
[ Backtracking Tokenizer ]
  ├── 1. Greedy 2-Letter Element Match   (001 – 118)
  ├── 2. Single-Letter Element Match     (001 – 092)
  ├── 3. Missing-Letter Fallback Bank    (201 – 212)
  └── 4. Word Boundary / Space Token     (000)
         │
         ▼
[ 3-Digit Contiguous Stream (Length % 3 == 0) ]
         │
         ▼
[ Fixed-Width Decoder (str.slice(i, i + 3)) ]
         │
         ▼
[ Sentence Case Output Formatter ]
```

### Protocol Table

| Numeric Range | Purpose | Slicing Invariant | Examples |
| :--- | :--- | :--- | :--- |
| `001` – `118` | **Official Periodic Elements** | Exactly 3 digits | `001` (H), `006` (C), `044` (Ru), `077` (Ir), `118` (Og) |
| `201` – `212` | **Fallback Single Letters** | Exactly 3 digits | `201` (A), `202` (D), `203` (E), `204` (G), `205` (J), `206` (L), `207` (M), `208` (Q), `209` (R), `210` (T), `211` (X), `212` (Z) |
| `000` | **Space Delimiter** | Exactly 3 digits | Represents a word boundary (` `) |

### Demonstration
* Input: `"Ruchir Gupta"`
* Tokenized Elements: `Ru` · `C` · `H` · `Ir` · ` ` · `G` · `U` · `P` · `Ta`
* Encoded Stream: `044006001077000204092015073`
* Decoded Output (Sentence Case): `"Ruchir gupta"`

---

## ✨ Features

- **Zero Runtime Dependencies:** Built purely with semantic HTML5 and vanilla JavaScript.
- **Sub-token Optimizer:** Uses a backtracking algorithm prioritizing genuine multi-character elements over fallbacks to maximize elemental coverage.
- **Live Stream Validation:** Real-time character count and chunk divisibility inspector (`len % 3 === 0`).
- **Dynamic Badge Visualizer:** Displays real-time elemental cards with atomic numbers, symbols, and element names.
- **Dual Output Display:** Formats the deciphered text into natural **Sentence case** alongside a tokenized chemical inspection stream.
- **One-Click Clipboard Actions:** Instant copy triggers with toast notifications.

---

## 🚀 Quick Start

### Running Locally
No build tools, package managers, or local servers are required.

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/periodic-cipher.git
   cd periodic-cipher
   ```
2. Open `index.html` directly in your browser:
   ```bash
   # On macOS
   open index.html

   # On Linux
   xdg-open index.html

   # On Windows
   start index.html
   ```

---

## 🌐 Free Deployment (GitHub Pages)

1. Push your repository to GitHub.
2. In your repo, go to **Settings** $\to$ **Pages**.
3. Under **Branch**, select `main` and root `/(root)`, then click **Save**.
4. Your site will be live at:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```

### Custom Domain Configuration (Optional)
To use a custom domain (e.g., `cipher.yourdomain.com`):
1. In your DNS provider (e.g., Cloudflare, Route53, Namecheap), create a `CNAME` record:
   - **Type:** `CNAME`
   - **Name:** `cipher`
   - **Value / Target:** `<your-username>.github.io`
2. Under **Settings $\to$ Pages $\to$ Custom domain** in your GitHub repository, enter `cipher.yourdomain.com` and hit **Save**.
3. Check the **Enforce HTTPS** box once DNS propagation completes.

---

## 🤝 Contributing

Contributions are welcome! If you would like to expand the cipher (e.g., adding punctuation handling dictionaries or phonetic multi-character lookups):

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NewFeature`)
3. Commit your Changes (`git commit -m 'feat: Add support for special symbols'`)
4. Push to the Branch (`git push origin feature/NewFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.