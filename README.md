<div align="center">

<img src="https://getslatewave.com/brand/icon.png" alt="" height="64" align="middle">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://getslatewave.com/brand/wordmark-light.png">
  <img alt="Slatewave" src="https://getslatewave.com/brand/wordmark.png" height="64" align="middle">
</picture>

# Slatewave (delta)

A Slatewave palette for [`delta`](https://github.com/dandavison/delta) — the syntax-highlighting pager for git diffs. Part of the [Slatewave family](#slatewave-family) — one palette across editors, terminals, prompts, notes, and more.

> _Slate below, teal above._

![Slatewave preview](docs/preview.png)

</div>

---

## What it styles

`delta` exposes a flat, generous set of style keys — minus / plus, emph / non-emph, hunk / file / commit headers, line numbers, blame, merge conflicts, grep output. Slatewave maps each onto the family palette so the diff reads spatially, not just chromatically:

- **Minus / plus** — desaturated rose and teal tints behind a `syntax` foreground, so syntax highlighting stays legible against the role color
- **Emph styles** — saturated rose / teal for the *bytes that actually changed* inside a line, so delta's word-level diff signal is unmistakable
- **Hunk header** — teal-300 label inside a slate-600 box; `@@ -12,7 +12,9 @@` math rendered in amber so the line-number jump pops
- **File header** — slate-200 bold with a teal underline rule
- **Line numbers** — slate gutter, rose for minus, teal for plus, slate-500 for zero
- **Blame palette** — a four-step slate gradient so authorship reads as depth
- **Merge conflicts** — rose for "ours", teal for "theirs"
- **Grep output** — teal for filenames, amber for line numbers, rose-reverse on the matched word

Pairs with [bat-slatewave](https://github.com/kevinlangleyjr/bat-slatewave), which registers the `Slatewave` syntax theme that delta reads via `syntax-theme`.

---

## Requirements

- **delta** ≥ 0.16 — [install guide](https://dandavison.github.io/delta/installation.html)
- **bat-slatewave** *(recommended)* — registers the `Slatewave` syntax theme via `bat cache --build`. Without it, swap `syntax-theme = Slatewave` for a bat default like `base16-256`, or remove the line entirely.

---

## Installation

`delta` is configured entirely through `~/.gitconfig`. There are two clean paths.

### Clone + include

```sh
git clone https://github.com/kevinlangleyjr/delta-slatewave.git \
  ~/.config/delta-slatewave
git config --global include.path \
  ~/.config/delta-slatewave/slatewave.gitconfig
```

`include.path` layers the file into your global git config, so updates land with `git -C ~/.config/delta-slatewave pull`.

### Or: paste the block straight in

Copy the contents of [`slatewave.gitconfig`](slatewave.gitconfig) into your `~/.gitconfig` and you're done. This is the path to take if you want to tweak individual keys in place.

### Verify

```sh
git -C any-repo log -p | head -60
```

You should see slate-tinted minus/plus blocks, a teal hunk header sat in a slate box, and amber line-number math.

---

## Palette

Slatewave shares its palette with the companion themes. Every color resolves to a semantic role.

### Foundation — slate

| | Hex | Tailwind | Where |
|---|---|---|---|
| ![#1e293b](https://placehold.co/20x20/1e293b/1e293b.png) | `#1e293b` | slate-800 | blame stop 0 |
| ![#282c34](https://placehold.co/20x20/282c34/282c34.png) | `#282c34` | slate-editor | blame stop 1 |
| ![#334155](https://placehold.co/20x20/334155/334155.png) | `#334155` | slate-700 | blame stop 2 |
| ![#475569](https://placehold.co/20x20/475569/475569.png) | `#475569` | slate-600 | blame stop 3, header rule, line gutter |
| ![#64748b](https://placehold.co/20x20/64748b/64748b.png) | `#64748b` | slate-500 | zero-line numbers |
| ![#94a3b8](https://placehold.co/20x20/94a3b8/94a3b8.png) | `#94a3b8` | slate-400 | hunk-header file path |
| ![#cbd5e1](https://placehold.co/20x20/cbd5e1/cbd5e1.png) | `#cbd5e1` | slate-300 | commit body |
| ![#e2e8f0](https://placehold.co/20x20/e2e8f0/e2e8f0.png) | `#e2e8f0` | slate-200 | file header |

### Diff roles

| | Hex | Tailwind | Where |
|---|---|---|---|
| ![#5eead4](https://placehold.co/20x20/5eead4/5eead4.png) | `#5eead4` | teal-300 | hunk header, plus line numbers, file underline |
| ![#0e3a35](https://placehold.co/20x20/0e3a35/0e3a35.png) | `#0e3a35` | teal-deep | plus background |
| ![#1d6457](https://placehold.co/20x20/1d6457/1d6457.png) | `#1d6457` | teal-emph | plus-emph background (changed bytes) |
| ![#fb7185](https://placehold.co/20x20/fb7185/fb7185.png) | `#fb7185` | rose-400 | minus line numbers, ours-conflict, whitespace error |
| ![#3b0e1a](https://placehold.co/20x20/3b0e1a/3b0e1a.png) | `#3b0e1a` | rose-deep | minus background |
| ![#7a1a2a](https://placehold.co/20x20/7a1a2a/7a1a2a.png) | `#7a1a2a` | rose-emph | minus-emph background (changed bytes) |
| ![#fbbf24](https://placehold.co/20x20/fbbf24/fbbf24.png) | `#fbbf24` | amber-400 | hunk-header line numbers, grep line numbers |

---

## Style key map

| Key | Color | Notes |
|---|---|---|
| `minus-style` | `syntax` on `#3b0e1a` | full minus line |
| `minus-emph-style` | `syntax bold` on `#7a1a2a` | bytes that changed |
| `minus-non-emph-style` | `syntax` on `#2a0a13` | bytes that did not change |
| `plus-style` | `syntax` on `#0e3a35` | full plus line |
| `plus-emph-style` | `syntax bold` on `#1d6457` | bytes that changed |
| `plus-non-emph-style` | `syntax` on `#0a2a26` | bytes that did not change |
| `zero-style` | `syntax` | unchanged context |
| `hunk-header-style` | `#5eead4 bold` | the `@@ ... @@` label |
| `hunk-header-decoration-style` | `#475569 box` | slate box around it |
| `hunk-header-file-style` | `#94a3b8` | filename next to the label |
| `hunk-header-line-number-style` | `#fbbf24 bold` | the `-12,7 +12,9` numbers |
| `file-style` | `#e2e8f0 bold` | file path |
| `file-decoration-style` | `#5eead4 ul` | teal underline rule |
| `commit-style` | `#cbd5e1 bold` | commit hash + author body |
| `commit-decoration-style` | `#475569 box` | slate box |
| `line-numbers-left-style` | `#475569` | gutter, minus column |
| `line-numbers-right-style` | `#475569` | gutter, plus column |
| `line-numbers-minus-style` | `#fb7185` | line numbers on a minus line |
| `line-numbers-plus-style` | `#5eead4` | line numbers on a plus line |
| `line-numbers-zero-style` | `#64748b` | line numbers on context |
| `whitespace-error-style` | `#fb7185 reverse` | trailing whitespace, mixed indent |
| `blame-palette` | slate gradient | `#1e293b` → `#475569` |
| `merge-conflict-ours-diff-header-style` | `#fb7185 bold` | "ours" header |
| `merge-conflict-theirs-diff-header-style` | `#5eead4 bold` | "theirs" header |
| `grep-file-style` | `#5eead4` | filename in `git grep` |
| `grep-line-number-style` | `#fbbf24` | line number in `git grep` |
| `grep-match-word-style` | `#fb7185 reverse` | the matched substring |

---

## Customize

Override in place. Every `delta.*` key is independent — drop a single line in your own `~/.gitconfig` after the `include` and it wins.

```ini
# Bump the plus tint to a brighter teal
[delta]
    plus-style      = syntax "#114a44"
    plus-emph-style = syntax bold "#1f7867"

# Or go side-by-side
[delta]
    side-by-side = true
```

### Pair with bat-slatewave

`syntax-theme = Slatewave` resolves through `bat`'s theme cache. Install [bat-slatewave](https://github.com/kevinlangleyjr/bat-slatewave) and run `bat cache --build` to register it; without that step, set `syntax-theme` to a built-in like `base16-256` or `Coldark-Dark`.

### Pair with line numbers off

If you prefer a tighter view, drop `line-numbers = true`. The hunk header alone still gives you the `-12,7 +12,9` math, so you don't lose orientation.

---

## Slatewave family

One palette. Every tool.

- **Editors** — [VSCode](https://github.com/kevinlangleyjr/vscode-slatewave) · [Neovim](https://github.com/kevinlangleyjr/neovim-slatewave) · [Helix](https://github.com/kevinlangleyjr/helix-slatewave) · [Zed](https://github.com/kevinlangleyjr/zed-slatewave) · [Sublime Text](https://github.com/kevinlangleyjr/sublime-text-slatewave) · [JetBrains](https://github.com/kevinlangleyjr/jetbrains-slatewave)
- **Terminals** — [Alacritty](https://github.com/kevinlangleyjr/alacritty-slatewave) · [Ghostty](https://github.com/kevinlangleyjr/ghostty-slatewave) · [iTerm2](https://github.com/kevinlangleyjr/iterm2-slatewave) · [WezTerm](https://github.com/kevinlangleyjr/wezterm-slatewave) · [Windows Terminal](https://github.com/kevinlangleyjr/windows-terminal-slatewave) · [Kitty](https://github.com/kevinlangleyjr/kitty-slatewave)
- **Prompts** — [Oh My Posh](https://github.com/kevinlangleyjr/slatewave-omp) · [Starship](https://github.com/kevinlangleyjr/starship-slatewave)
- **Multiplexer** — [tmux](https://github.com/kevinlangleyjr/tmux-slatewave)
- **CLI** — [bat](https://github.com/kevinlangleyjr/bat-slatewave) · [LSD](https://github.com/kevinlangleyjr/lsd-slatewave)
- **Notes** — [Obsidian](https://github.com/kevinlangleyjr/obsidian-slatewave) · [Logseq](https://github.com/kevinlangleyjr/logseq-slatewave) · [MarkEdit](https://github.com/kevinlangleyjr/markedit-slatewave) · [Anytype](https://github.com/kevinlangleyjr/anytype-slatewave)
- **Launchers** — [Alfred](https://github.com/kevinlangleyjr/alfred-slatewave) · [Raycast](https://github.com/kevinlangleyjr/raycast-slatewave)
- **Chat** — [Slack](https://github.com/kevinlangleyjr/slack-slatewave)

See [getslatewave.com](https://getslatewave.com) for the full family.

---

## Contributing

Issues and PRs welcome. For palette tweaks, please include a before/after `git log -p` screenshot against a representative diff (a refactor with mixed adds/removes/renames works well) so the visual tradeoff is obvious.

---

## License

WTFPL — Do What The Fuck You Want To Public License. See [LICENSE](LICENSE).
