---
slug: fonts-matter-2025-06-12
title: Fonts Matter
date: 2025-06-12
tags: [fedora, fonts, productivity, note, todo]
status: draft
---

# Fonts Matter: A Deep Dive into Typography and Display

After switching from a MacBook Pro with Retina display to a ThinkPad T590, I've gained a new
appreciation for how fonts work and why they matter. This note explores the technical aspects of
fonts, their rendering, and practical considerations for different displays.

<!-- truncate -->

## TODO

I've created a font master script `~/.scripts/fedora/fonts.sh` which allows to manage fonts
configuration. It supports profiles and i've created a default T590Code fonts profile:

```
# Font profile: T590Code
# Created: Fri Jun 13 03:55:33 AM +07 2025
MONOSPACE_FONT="Terminus 10"
INTERFACE_FONT="Source Code Pro Medium Italic 10"
DOCUMENT_FONT="Source Code Pro Medium Italic 10"
TITLEBAR_FONT="Source Code Pro Medium Italic 10"
SCALING_FACTOR=1.0
HINTING=full
ANTIALIASING=rgba
RGBA=rgb
```

I've downloaded some proprietary fonts in `~/.fonts` for later tests.

- https://github.com/sunaku/tamzen-font
- http://www.fial.com/~scott/tamsyn-font/
- https://github.com/be5invis/Iosevka
- https://github.com/ryanoasis/nerd-fonts
- https://github.com/cancng/fonts

- [] Experiment with creating different profiles
- [] Test modern, paid and experimental fonts

## Why Fonts Matter

Fonts are crucial for readability, productivity, and eye comfort, especially when working with code.
The difference becomes particularly noticeable when switching between high-DPI displays (like
Retina) and traditional displays. While modern displays make almost any font look good, older
displays require careful font selection to maintain readability and reduce eye strain.

## Types of Fonts

### Monospace vs Proportional Fonts

Before diving into font technologies, it's important to understand the fundamental difference
between monospace and proportional fonts:

**Monospace Fonts:**

- Every character has the same width
- 'i' takes up the same space as 'w'
- Essential for code and terminals
- Makes text align in columns
- Examples: Terminus, Fira Code, JetBrains Mono

**Proportional Fonts:**

- Characters have different widths
- 'i' is narrower than 'w'
- Better for reading text
- More natural looking
- Examples: Cantarell, Noto Sans, Arial

Monospace fonts are particularly important for:

- Code editing (aligns code blocks)
- Terminal use (creates grid-like layouts)
- ASCII art
- Tables and data display
- Any situation where character alignment matters

### 1. Bitmap Fonts (Pixel Fonts)

Bitmap fonts are the most basic type, where each character is literally a grid of pixels. Think of
them as tiny pixel art for each letter.

#### How They Work

- Each character is a fixed grid of pixels
- Designed pixel by pixel for specific sizes
- No scaling or anti-aliasing
- Direct pixel-to-screen mapping

#### Characteristics

**Pros:**

- Razor-sharp at intended sizes
- Minimal CPU usage
- Excellent for low-resolution displays
- Perfect for terminal use

**Cons:**

- Limited to specific sizes (e.g., Terminus 9, 10, 12)
- No smooth curves
- Poor scaling
- Limited support for italics, bold, and Unicode
- Can be hard on the eyes for long reading sessions

**Common Examples:**

- Terminus
- Proggy
- Dina
- Fixedsys
- Misc Fixed

### 2. Modern Vector Fonts

Modern fonts use mathematical curves (vectors) to define character shapes, allowing for smooth
scaling and advanced typographic features.

#### How They Work

- Characters defined by mathematical curves
- Rendered at any size
- Uses anti-aliasing and subpixel rendering
- Supports advanced typographic features

#### Characteristics

**Pros:**

- Infinitely scalable
- Smooth curves and diagonals
- Full support for bold, italics, Unicode, ligatures
- Better for long reading sessions
- Modern features like variable width and stylistic sets

**Cons:**

- Can appear slightly blurry on low-DPI displays
- More CPU intensive
- May not be as sharp as bitmap fonts at small sizes

**Common Examples:**

- Fira Code
- JetBrains Mono
- MesloLGS NF
- Source Code Pro
- Hack
- DejaVu Sans Mono
- Consolas

### 3. Hybrid Approaches

Some fonts combine the best of both worlds:

- Vector fonts with bitmap fallbacks for specific sizes
- Hinted fonts that align to pixel grids
- Fonts with special rendering for small sizes

### 4. Specialized Programming Fonts

#### Nerd Fonts

Nerd Fonts are a collection of patched fonts that add a large number of glyphs (icons) to popular
programming fonts. They're particularly popular among developers who use terminal-based tools and
want to display icons and symbols.

**Key Features:**

- Adds thousands of icons to existing fonts
- Maintains original font characteristics
- Supports popular icon sets (Devicons, Font Awesome, etc.)
- Works across different platforms and terminals
- Preserves programming ligatures

**Popular Nerd Font Variants:**

- JetBrainsMono Nerd Font
- FiraCode Nerd Font
- Hack Nerd Font
- Source Code Pro Nerd Font
- MesloLGS NF (already includes Nerd Font patches)

**Use Cases:**

- Terminal prompts (Oh My Zsh, Starship)
- File managers (ranger, nnn)
- Code editors (Vim, Neovim)
- Status bars and widgets
- Documentation with icons

#### Iosevka

Iosevka is a unique programming font that stands out for its narrow design and extensive
customization options. It's particularly popular among developers who want to maximize screen real
estate while maintaining readability.

**Key Features:**

- Narrow design (saves horizontal space)
- High legibility at small sizes
- Extensive customization options
- Multiple variants (Term, Slab, Aile, etc.)
- Support for programming ligatures
- Customizable character shapes

**Variants:**

- Iosevka (default)
- Iosevka Term (terminal-optimized)
- Iosevka Slab (with serifs)
- Iosevka Aile (more rounded)
- Iosevka Sparkle (with ligatures)

**Why Developers Love It:**

- Fits more code on screen
- Maintains readability at small sizes
- Consistent character width
- Clean, modern appearance
- Highly customizable
- Excellent for long coding sessions

### Deep Dive: Iosevka Typeface Family

Iosevka [ˌjɔˈseβ.kʰa] is an open-source, sans-serif + slab-serif, monospace + quasi‑proportional
typeface family, designed for writing code, using in terminals, and preparing technical documents.
It represents a unique approach to programming typography that challenges traditional monospace
constraints.

#### Design Philosophy

Iosevka was created with the philosophy that programming fonts don't need to be strictly monospace.
Instead, it uses a "quasi-proportional" approach where:

- **Monospace Core**: Most characters maintain consistent width for code alignment
- **Smart Widths**: Certain character pairs (like "ll", "ii", "rn") can be narrower
- **Contextual Spacing**: Characters adjust based on their neighbors for better readability

This hybrid approach gives you the benefits of monospace fonts (code alignment) while improving
readability and saving horizontal space.

#### Family Variants

Iosevka offers an extensive range of variants that can be mixed and matched:

**Base Styles:**

- **Iosevka**: Standard sans-serif variant
- **Iosevka Slab**: Serif variant with slab serifs
- **Iosevka Aile**: More rounded, friendly appearance
- **Iosevka Sparkle**: Includes programming ligatures

**Terminal Optimizations:**

- **Iosevka Term**: Optimized for terminal use with consistent character widths
- **Iosevka Fixed**: Strict monospace variant for maximum compatibility

**Width Options:**

- **Iosevka Extended**: Wider characters for better readability
- **Iosevka Narrow**: Compact design for maximum screen real estate
- **Iosevka Default**: Balanced width for general use

#### Advanced Customization

One of Iosevka's most powerful features is its build-time customization system. You can create
custom variants by specifying:

```bash
# Example build configuration
./build.sh \
  --family-name "Iosevka Custom" \
  --weights "thin,light,regular,medium,bold" \
  --widths "normal,extended" \
  --styles "normal,italic" \
  --variants "ss01,ss02,ss03" \
  --output-dir "./custom-iosevka"
```

**Stylistic Sets (ss01-ss20):**

- **ss01**: Alternative 'a' and 'g' forms
- **ss02**: Alternative 'i', 'j', 'l' forms
- **ss03**: Alternative '0' (slashed zero)
- **ss04**: Alternative '1' (serifed one)
- **ss05**: Alternative '6' and '9' forms
- **ss06**: Alternative '7' (crossed seven)
- **ss07**: Alternative '8' (closed eight)
- **ss08**: Alternative '9' (closed nine)
- **ss09**: Alternative 'k' form
- **ss10**: Alternative 'u' form
- **ss11**: Alternative 'G' form
- **ss12**: Alternative 'Q' form
- **ss13**: Alternative 'R' form
- **ss14**: Alternative 'W' form
- **ss15**: Alternative '3' form
- **ss16**: Alternative '6' form
- **ss17**: Alternative '9' form
- **ss18**: Alternative 'C' form
- **ss19**: Alternative 'G' form
- **ss20**: Alternative 'L' form

#### Technical Features

**Programming Ligatures:**

- Full support for Fira Code-style ligatures
- Customizable ligature behavior
- Maintains ligatures across all weights and styles

**Unicode Support:**

- Extensive coverage of programming symbols
- Powerline symbols for terminal prompts
- Mathematical and scientific notation
- International character support

**Rendering Optimizations:**

- Optimized for screen display
- Excellent hinting for low-DPI displays
- Smooth rendering at all sizes
- Consistent stroke weights across variants

#### Use Cases and Recommendations

**Best For:**

- **Code Editors**: Excellent ligature support and readability
- **Terminals**: Multiple variants optimized for different terminal types
- **Documentation**: Professional appearance for technical writing
- **Web Development**: Good support for HTML/CSS symbols

**Consider Alternatives When:**

- **Strict Monospace Required**: Some tools expect exact character widths
- **Legacy System Support**: Older systems may not support all variants
- **Team Consistency**: Custom builds may not match team standards

**Recommended Variants:**

- **General Development**: Iosevka Regular with ss01-ss03
- **Terminal Use**: Iosevka Term with your preferred weight
- **Documentation**: Iosevka Slab for a more formal appearance
- **Maximum Space**: Iosevka Narrow with ss01-ss03

#### Building Custom Variants

Iosevka's build system allows you to create perfectly tailored fonts:

```bash
# Clone the repository
git clone https://github.com/be5invis/Iosevka.git
cd Iosevka

# Install dependencies
npm install

# Build custom variant
./build.sh \
  --family-name "Iosevka Dev" \
  --weights "light,regular,medium,bold" \
  --widths "normal" \
  --styles "normal,italic" \
  --variants "ss01,ss02,ss03,ss04,ss05" \
  --output-dir "./iosevka-dev"
```

This customization capability makes Iosevka one of the most flexible programming fonts available,
allowing developers to create the perfect font for their specific needs and preferences.

## What is a Typeface Family?

A typeface family is a collection of related fonts that share the same design characteristics but
vary in weight, style, and other attributes. Think of it as a "family" where all members have the
same genetic traits but different personalities.

### Understanding the Structure

**Typeface vs Font:**

- **Typeface**: The overall design concept (e.g., "Helvetica")
- **Font**: A specific instance of that typeface (e.g., "Helvetica Bold 12pt")

**Family Members:** A complete typeface family typically includes:

1. **Weight Variations:**

   - Thin (100)
   - Extra Light (200)
   - Light (300)
   - Regular/Normal (400)
   - Medium (500)
   - Semi Bold (600)
   - Bold (700)
   - Extra Bold (800)
   - Black/Heavy (900)

2. **Style Variations:**

   - Regular
   - Italic
   - Oblique
   - Condensed
   - Extended

3. **Width Variations:**
   - Ultra Condensed
   - Condensed
   - Normal
   - Extended
   - Ultra Extended

### Examples of Typeface Families

#### Source Code Pro Family

```
Source Code Pro Thin
Source Code Pro Extra Light
Source Code Pro Light
Source Code Pro Regular
Source Code Pro Medium
Source Code Pro Semi Bold
Source Code Pro Bold
Source Code Pro Extra Bold
Source Code Pro Black
```

Each weight maintains the same character design but with different stroke thickness, allowing
designers to create visual hierarchy and emphasis.

#### Fira Code Family

```
Fira Code Light
Fira Code Regular
Fira Code Medium
Fira Code Semi Bold
Fira Code Bold
```

Fira Code is particularly popular among developers because it maintains programming ligatures across
all weights while providing flexibility for different use cases.

### Why Typeface Families Matter

1. **Consistency**: Using fonts from the same family ensures visual harmony across your interface
2. **Hierarchy**: Different weights help establish information hierarchy (headings, body text,
   captions)
3. **Flexibility**: Multiple weights give you options for different contexts and screen sizes
4. **Professional Appearance**: Consistent typography looks more polished and trustworthy

### Choosing the Right Family

When selecting a typeface family for development work, consider:

- **Complete Coverage**: Does it have all the weights you need?
- **Programming Features**: Does it support ligatures, powerline symbols, etc.?
- **Screen Rendering**: How does it look at different sizes on your display?
- **Cross-Platform**: Is it available on all your target systems?

### Variable Fonts: The Future

Modern typeface families are increasingly adopting the OpenType Variable Font format, which allows
for:

- Infinite weight variations (not just 9 discrete weights)
- Smooth transitions between styles
- Smaller file sizes
- More flexible design possibilities

## Font Rendering Explained

### Bitmap Rendering

```
"Draw this exact grid of pixels on the screen, don't touch it."
```

- Direct pixel mapping
- No anti-aliasing
- Sharp but blocky
- Perfect for terminals

### Vector Rendering

```
"Draw this shape at size X, smooth the edges, align to pixel grid if possible."
```

- Mathematical curve rendering
- Anti-aliasing for smooth edges
- Subpixel rendering for better clarity
- Better for general use

## Understanding Font Rendering Techniques

### Antialiasing

Antialiasing is a technique that smooths the jagged edges (aliasing) of fonts by adding intermediate
pixels. Think of it as "filling in the gaps" between pixels to create the illusion of smooth curves.

#### Types of Antialiasing:

1. **None**

   - No smoothing applied
   - Sharp but jagged edges
   - Best for bitmap fonts
   - Example: Terminal fonts at their native size

2. **Grayscale**

   - Uses shades of gray to smooth edges
   - Works on any display
   - Good balance of sharpness and smoothness
   - Example: Standard font rendering on most displays

3. **RGBA (Subpixel)**
   - Uses individual red, green, and blue subpixels
   - Creates smoother edges than grayscale
   - Only works on LCD displays
   - Can cause color fringing on some displays
   - Example: Modern font rendering on LCD screens

### Font Hinting

Hinting is like a set of instructions that tells the font renderer how to align characters to the
pixel grid. It's crucial for making text readable at small sizes.

#### How Hinting Works:

1. **None**

   - No alignment to pixel grid
   - Can look blurry at small sizes
   - Good for high-DPI displays
   - Example: Fonts on Retina displays

2. **Slight**

   - Minimal alignment to pixel grid
   - Good balance of sharpness and smoothness
   - Works well for most vector fonts
   - Example: Default setting for most modern fonts

3. **Medium**

   - Moderate alignment to pixel grid
   - Sharper than slight, but still smooth
   - Good for medium-sized text
   - Example: Body text in documents

4. **Full**
   - Strong alignment to pixel grid
   - Very sharp but can look blocky
   - Best for bitmap fonts and small text
   - Example: Terminal fonts at small sizes

#### Why Hinting Matters:

- Makes text readable at small sizes
- Ensures consistent character widths
- Maintains vertical alignment
- Preserves important features (like the dot in 'i')
- Crucial for low-DPI displays

## Fedora 42 GNOME Font Settings

Here's a practical guide for customizing fonts in Fedora 42 GNOME:

### System Font Settings

1. **UI (Interface) Font**

```bash
gsettings set org.gnome.desktop.interface font-name 'Cantarell 11'
```

2. **Monospace (Terminal) Font**

```bash
gsettings set org.gnome.desktop.interface monospace-font-name 'Terminus 9'
```

3. **Document Font**

```bash
gsettings set org.gnome.desktop.interface document-font-name 'Noto Sans 11'
```

4. **Title Bar Font**

```bash
gsettings set org.gnome.desktop.wm.preferences titlebar-font 'Cantarell Bold 11'
```

### Font Rendering Settings

5. **Antialiasing**

```bash
gsettings set org.gnome.settings-daemon.plugins.xsettings antialiasing 'rgba'
```

Options: 'none', 'grayscale', 'rgba' (default)

6. **Hinting**

```bash
gsettings set org.gnome.settings-daemon.plugins.xsettings hinting 'slight'
```

Options: 'none', 'slight', 'medium', 'full'

- Use 'full' for bitmap fonts
- 'slight' works well for most vector fonts

7. **Text Scaling**

```bash
gsettings set org.gnome.desktop.interface text-scaling-factor 1.0
```

Adjust this value (e.g., 1.1, 1.2) to scale all fonts without changing DPI.

### View Current Settings

```bash
gsettings list-recursively | grep font
```

## Practical Tips

1. For terminal use on older displays:

   - Try bitmap fonts like Terminus
   - Set hinting to 'full'
   - Consider size 9 or 10 for optimal sharpness

2. For general UI:

   - Use modern vector fonts (Cantarell, Noto Sans)
   - Keep antialiasing on 'rgba'
   - Use 'slight' hinting for best results

3. For code editing:
   - Consider programming fonts with ligatures (Fira Code, JetBrains Mono)
   - Ensure good contrast for comments
   - Test different sizes for your specific display

## Conclusion

Font choice significantly impacts productivity and comfort, especially when working with code. While
modern displays make font selection less critical, older displays require careful consideration of
font type, size, and rendering settings. The key is finding the right balance between sharpness and
readability for your specific use case and display.

Remember: What works on a Retina display might not work well on a traditional display, and vice
versa. Take the time to experiment and find what works best for your eyes and your workflow.
