# Desoldering Station Logo

This directory contains the project logo and related branding assets.

## Files

- **logo.svg** - Main project logo (200x200px SVG)
  - Used in the documentation site navbar
  - Used in README and documentation
  - Features realistic desoldering gun with pistol-grip design
  
- **logo_tft.svg** - TFT display optimized logo (64x64px SVG)
  - Simplified design with bolder lines for small displays
  - Optimized for ILI9341 and similar TFT screens
  
- **logo_tft_64x64.png**, **logo_tft_128x128.png**, **logo_tft_240x240.png**
  - Pre-rendered PNG versions for embedded displays
  - Ready to use in firmware for splash screens or status displays

- **favicon.ico** - Website favicon (multi-size: 16x16, 32x32, 48x48, 64x64)
  - Used as the browser tab icon
  
- **social-card.png** - Social media card (1200x630px)
  - Used when sharing links on social media platforms
  - Includes logo and project description

## Logo Design

The logo represents the core functionality of the desoldering station with a realistic desoldering gun design:

### Visual Elements

1. **Desoldering Gun** (center)
   - Pistol-grip handle with ergonomic design (based on real desoldering stations)
   - Trigger and trigger guard
   - Dark gray body with gradient shading
   - Horizontal nozzle orientation
   - Grip texture details

2. **Heated Nozzle**
   - Orange-to-red gradient representing heat intensity
   - Gold glow at the tip showing active heating
   - Heat waves emanating from the nozzle
   - Rotated at -20° for dynamic appearance

3. **Temperature Display**
   - Digital display showing "350°C" (typical desoldering temperature)
   - Dark display background with cyan text (LCD-style)
   - Represents the RP2040-based temperature monitoring

4. **Circuit/Electronic Elements**
   - Cyan/blue circuit rings (concentric circles)
   - Connection nodes at cardinal points
   - Temperature arc gauge (orange/red gradient)
   - Small IC chip symbol (RP2040 reference)

5. **Color Scheme**
   - **Orange/Red** (#FF9F1C → #E63946) - Heat, active desoldering, high temperature
   - **Cyan/Blue** (#2EC4B6, #20A4F3) - Electronics, digital control, cool precision
   - **Dark Gray** (#6B7280 → #374151) - Gun body, hardware
   - **Grip Dark** (#4B5563 → #1F2937) - Handle, ergonomics
   - **Gold** (#FFD700) - Hot tip, active state

### Symbolism

- **Pistol-Grip Gun** = Professional desoldering tool (matches actual hardware)
- **Heat Gradient** = Precise temperature control (PID)
- **Digital Display** = RP2040 firmware with real-time monitoring
- **Circuit Rings** = Embedded electronics and control system
- **Temperature Arc** = Control precision and temperature range

### Design Reference

Based on real desoldering stations:
- Handskit ZD-8915 style
- Weller style desoldering guns
- Professional desktop desoldering stations with digital control

## Usage

The logo works well on both light and dark backgrounds due to its self-contained color scheme. The SVG format ensures crisp rendering at any size.

### In Documentation (Docusaurus)

The logo is referenced in `docusaurus.config.ts`:

```typescript
navbar: {
  logo: {
    alt: 'Desoldering Station Logo',
    src: 'img/logo.svg',
  },
}
```

### Favicon

The favicon is automatically loaded by Docusaurus from `static/img/favicon.ico`.

## Regeneration

If you need to regenerate the favicon or social card after modifying `logo.svg`:

### Option 1: Using Online Tools
- **Favicon**: Use [favicon.io](https://favicon.io/favicon-converter/) or [RealFaviconGenerator](https://realfavicongenerator.net/)
- **Social Card**: Use any image editor (GIMP, Photoshop, Figma, etc.)

### Option 2: Using Python Scripts

Install required dependencies:
```bash
pip install Pillow cairosvg
```

Create a script to generate the favicon:
```python
import io
from PIL import Image
import cairosvg

# Read logo.svg and generate multi-size favicon
sizes = [16, 32, 48, 64]
images = []

with open('logo.svg', 'r') as f:
    svg_content = f.read()

for size in sizes:
    png_bytes = cairosvg.svg2png(
        bytestring=svg_content.encode('utf-8'),
        output_width=size,
        output_height=size
    )
    images.append(Image.open(io.BytesIO(png_bytes)))

images[0].save('favicon.ico', format='ICO', 
               sizes=[(s, s) for s in sizes],
               append_images=images[1:])
```
