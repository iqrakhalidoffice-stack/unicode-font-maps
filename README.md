# unicode-font-maps

Open JSON character maps for converting plain A–Z, a–z and 0–9 into Unicode "font" styles: bold, italic, script (cursive), Fraktur (gothic), double-struck, monospace, fullwidth (vaporwave) and circled.

These aren't fonts. Each style is a separate set of Unicode code points, mostly from the **Mathematical Alphanumeric Symbols** block (U+1D400–U+1D7FF). That's why the text survives copy and paste into Instagram, Discord, TikTok and X, where real fonts can't be used.

Live tool built on these maps: **[LingoFonts.com](https://lingofonts.com/)**

```
LingoFonts  →  𝓛𝓲𝓷𝓰𝓸𝓕𝓸𝓷𝓽𝓼   (bold_script)
LingoFonts  →  𝕷𝖎𝖓𝖌𝖔𝕱𝖔𝖓𝖙𝖘   (bold_fraktur)
LingoFonts  →  ＬｉｎｇｏＦｏｎｔｓ   (fullwidth)
```

## Styles included

| Key | Example | Source block | Digits |
|---|---|---|---|
| `bold` | 𝐋𝐢𝐧𝐠𝐨 | Math Alphanumeric | ✓ |
| `italic` | 𝐿𝑖𝑛𝑔𝑜 | Math Alphanumeric | – |
| `bold_italic` | 𝑳𝒊𝒏𝒈𝒐 | Math Alphanumeric | – |
| `script` | ℒ𝒾𝓃ℊℴ | Math Alphanumeric + Letterlike Symbols | – |
| `bold_script` | 𝓛𝓲𝓷𝓰𝓸 | Math Alphanumeric | – |
| `fraktur` | 𝔏𝔦𝔫𝔤𝔬 | Math Alphanumeric + Letterlike Symbols | – |
| `bold_fraktur` | 𝕷𝖎𝖓𝖌𝖔 | Math Alphanumeric | – |
| `double_struck` | 𝕃𝕚𝕟𝕘𝕠 | Math Alphanumeric + Letterlike Symbols | ✓ |
| `sans_bold` | 𝗟𝗶𝗻𝗴𝗼 | Math Alphanumeric | ✓ |
| `monospace` | 𝙻𝚒𝚗𝚐𝚘 | Math Alphanumeric | ✓ |
| `fullwidth` | Ｌｉｎｇｏ | Halfwidth and Fullwidth Forms | ✓ |
| `circled` | Ⓛⓘⓝⓖⓞ | Enclosed Alphanumerics | ✓ |

## The "holes" (why naive offset math breaks)

Some letters were encoded in the older **Letterlike Symbols** block (U+2100–U+214F) before the math block existed. Their slots in the math block are reserved and left empty, so adding a fixed offset produces blank boxes for them. This repo maps them to the correct characters:

- **Script:** ℬ ℰ ℱ ℋ ℐ ℒ ℳ ℛ ℯ ℊ ℴ
- **Fraktur:** ℭ ℌ ℑ ℜ ℨ
- **Double-struck:** ℂ ℍ ℕ ℙ ℚ ℝ ℤ
- **Italic:** ℎ (Planck constant)

Reference: [Unicode Standard, Mathematical Alphanumeric Symbols chart (PDF)](https://www.unicode.org/charts/PDF/U1D400.pdf)

## Usage

```js
import maps from "./maps.json" assert { type: "json" };

const convert = (text, style) =>
  [...text].map(ch => maps[style][ch] ?? ch).join("");

convert("Hello 2026", "bold_script"); // 𝓗𝓮𝓵𝓵𝓸 2026
```

Characters with no mapping (punctuation, accented letters, and digits in styles that have none) pass through unchanged.

## Accessibility note

Screen readers may announce these characters one at a time by their Unicode names (for example "mathematical bold script capital H"), or skip them entirely. Don't use styled text for usernames, links or important information. See [WebAIM on screen readers](https://webaim.org/techniques/screenreader/).

## License

MIT. Use the maps in any project. A link back to [LingoFonts](https://lingofonts.com/) is appreciated but not required.
