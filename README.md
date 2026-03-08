# Kolmogorov Complexity Visualizer

An interactive, browser-based tool that approximates and visualizes the [Kolmogorov complexity](https://en.wikipedia.org/wiki/Kolmogorov_complexity) of any string — no build step, no dependencies, just a single HTML file.

## What is Kolmogorov Complexity?

The Kolmogorov complexity **K(s)** of a string is the length of the shortest program that produces it. Intuitively:

- **Structured / repetitive strings** (e.g. `aaaaaaa`, `ababab`) have *low* complexity — they can be described briefly.
- **Random strings** have *high* complexity — the shortest description is the string itself.

Because true Kolmogorov complexity is [uncomputable](https://en.wikipedia.org/wiki/Kolmogorov_complexity#Uncomputability), this tool approximates it using **LZ77 compression**: the number of LZ77 tokens produced serves as the complexity estimate.

## Features

- **Live analysis** — type or paste any string (up to 600 characters) and see metrics update instantly.
- **Character visualization** — each character is rendered as a colored block; back-referenced (repeated) patterns share the same color, literals are shown in grey.
- **Token stream** — the full LZ77 token sequence is displayed, showing exactly how the string is "described" as literals and back-references.
- **Normalized complexity gauge** — displays `K(s)/|s|` as a percentage with a color-coded label from *Very Simple* to *Near-Random*.
- **Complexity comparison** — a built-in side-by-side comparison of classic examples (all-A's, AB repeat, Thue-Morse sequence, π digits, random string, etc.).
- **Example presets** — one-click buttons to load well-known strings for exploration.

## Usage

Open `index.html` in any modern browser — no server or installation required.

```
open index.html
```

## How It Works

1. The input string is tokenized with a sliding-window **LZ77** algorithm (window size 255, max match length 16).
2. Each token is either a **literal** (one new character) or a **back-reference** (offset + length into the previous window).
3. **Normalized complexity** = `token count / string length`. A ratio near 0 means highly compressible; near 1 means effectively random.
4. Characters belonging to the same back-reference group are colored identically, making repeated patterns immediately visible.

## Examples

| String | Description | Complexity |
|---|---|---|
| `aaaaaaaaaa…` | All identical characters | Very Simple |
| `ababababab…` | Two-character period | Simple |
| `aababcabcd…` | Growing prefix sequence | Moderate |
| Thue-Morse sequence | Structured but aperiodic | Moderate |
| π digits | Normal number, digit distribution | Complex |
| Random alphanumeric | No exploitable structure | Near-Random |
