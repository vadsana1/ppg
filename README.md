# Thesis Cover Page Generator (pdf-lib + Lao Font)

## 1. Project Overview
This repository demonstrates how to generate a custom PDF cover page in Lao and English using the `pdf-lib` library, including how to embed a Lao-compatible font and a Base64-encoded logo. The final PDF is previewed in an `<iframe>`.

### Goal
Allow users to fill out thesis details (title, major, advisors, students, etc.) in Lao and English, then generate and preview a PDF cover page within the browser.

### Technology
- **`pdf-lib`**: For creating PDF documents in JavaScript.
- **Custom Lao TTF font**: Converted to Base64 to properly display Lao text.
- **Base64-encoded PNG logo**.

### Files
- **`index.html`**: Main web page containing the form and PDF preview.
- **`font_base64.js`**: Contains the Base64-encoded Lao font (raw base64, no `data:` prefix).
- **`logo_base64.js`**: Contains the Base64-encoded PNG logo (with `data:image/png;base64,` prefix).

## 2. Prerequisites
- A modern browser (Chrome, Firefox, Edge, Safari, etc.).


## 3. Installation & Setup
1. Clone or download this repository.
2. Place your custom Lao font (TTF) data in `font_base64.js`:
   - Use an online Base64 converter to convert the `.ttf` file to raw base64.
   - Assign that string to `window.LAO_FONT_BASE64`.
3. Place your PNG logo data in `logo_base64.js`:
   - Convert the `.png` file to Base64 (with prefix `data:image/png;base64,`).
   - Assign that string to `window.LOGO_BASE64`.
4. Ensure the correct script order in `index.html`:

```html
<!-- pdf-lib must load first -->
<script src="https://cdn.jsdelivr.net/npm/pdf-lib/dist/pdf-lib.min.js"></script>
<!-- Then fontkit if embedding custom fonts -->
<script src="https://cdn.jsdelivr.net/npm/@pdf-lib/fontkit/dist/fontkit.umd.js"></script>
<!-- Then font_base64.js, logo_base64.js, etc. -->
```

## 4. Running the Project
1. Open a terminal in the repository folder.

2. Open `index.html`.
3. Fill out the form (thesis title, major, students, etc.).
4. Click “Generate PDF”. The right side `<iframe>` should show the generated PDF.

## 5. Common Issues & Troubleshooting
### Blank Boxes for Lao Text
- Ensure `window.LAO_FONT_BASE64` is set to a valid base64 string of a font that supports Lao glyphs (e.g., NotoSansLao).
- Check for typos in your base64 data or script references.

### Error: Input to `PDFDocument.embedFont` was a custom font, but no fontkit instance was found
- Load the `@pdf-lib/fontkit` UMD script and call `pdfDoc.registerFontkit(...)` before embedding a custom font.

### “No enabled plugin supports this MIME type”
- Ensure your browser has an internal PDF viewer enabled. Try Chrome or Firefox.
- Alternatively, provide a download link instead of inline preview.

### “Tainted canvas” or CORS errors
- Avoid opening `index.html` directly via `file://` path. Serve via HTTP on localhost.

### Font or Logo Not Loading
- Verify the paths and script load order.
- Check the browser console for 404 or syntax errors in your `.js` files.

## 6. Customizing
- **Form Fields**: Add or remove form fields in `index.html`.
- **Layout/Styling**: Edit CSS or positions in the PDF generation code to match your desired cover style.
- **Additional Pages**: For multiple pages, use `pdfDoc.addPage()` and repeat the drawing process.

## 7. License
Feel free to modify or distribute this code. Original libraries used (`pdf-lib`, `fontkit`) have their own licenses—be sure to check them if you plan to use this in production.


## This project was initiated by Dr. Savath Saypadith