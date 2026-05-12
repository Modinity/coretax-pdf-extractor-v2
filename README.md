# Coretax PDF Extractor

Browser-based tool for extracting selected fields from Coretax PDF withholding tax documents and exporting the result as an Excel recap file.

The app is contained in a single `index.html` file. It runs PDF text extraction in the browser with PDF.js, parses the extracted text with Python through PyScript, and generates an `.xlsx` report with pandas and xlsxwriter.

## Features

- Upload multiple PDF files at once.
- Process files in batches to reduce browser memory pressure.
- Extract Coretax Bupot fields from sections A, B, and C.
- Detect Bupot status such as `NORMAL`, `DIBATALKAN`, `PEMBETULAN`, and `PEMBETULAN KE - X`.
- Export the parsed data to an Excel file named like `Tax_Recap_YYYYMMDD_HHMM.xlsx`.
- Runs fully in the browser after dependencies load.

## Extracted Fields

The Excel output contains these columns:

- `NO`
- `NOMOR`
- `MASA PAJAK`
- `SIFAT PEMOTONGAN DAN/ATAU PEMUNGUTAN PPh`
- `STATUS BUKTI PEMOTONGAN / PEMUNGUTAN`
- `A.1 NPWP / NIK`
- `A.2 NAMA`
- `A.3 NITKU`
- `B.1 JENIS FASILITAS`
- `B.2 JENIS PPh`
- `B.3 KODE OBJEK PAJAK`
- `B.4 OBJEK PAJAK`
- `B.5 DPP`
- `B.6 TARIF`
- `B.7 PAJAK PENGHASILAN`
- `B.8 JENIS DOKUMEN`
- `B.8 TANGGAL DOKUMEN`
- `B.9 NOMOR DOKUMEN`
- `B.10 PEMBAYARAN PPH`
- `B.11 NOMOR SP2D`
- `C.1 NPWP / NIK`
- `C.2 NITKU`
- `C.3 NAMA PEMOTONG`
- `C.4 TANGGAL`
- `C.5 NAMA PENANDATANGAN`

## Requirements

- A modern browser such as Chrome, Edge, Firefox, or Safari.
- Internet access when opening the page, because the app loads:
  - Tailwind CSS from CDN
  - PyScript from CDN
  - PDF.js from CDN
  - Python packages declared in PyScript: `pandas` and `xlsxwriter`

No backend server, database, or build step is required.

## Usage

1. Open `index.html` in a browser.
2. Wait until the Python engine finishes loading.
3. Click the upload area and select one or more Coretax PDF files.
4. Wait for processing to finish.
5. The Excel report downloads automatically. You can also click `Download Excel Report` if needed.

## Local Development

Because this project is a static HTML file, you can open it directly:

```bash
open index.html
```

If your browser blocks any local-file behavior, serve the directory with a simple static server:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## Deployment

Deploy `index.html` to any static hosting provider, for example:

- GitHub Pages
- Cloudflare Pages
- Netlify
- Vercel static hosting
- An internal static web server

Make sure the deployment environment allows loading scripts and styles from the external CDNs listed in the requirements.

## Privacy Notes

PDF files are processed in the user's browser. The current implementation does not upload files to a backend service because there is no backend in this repository.

The page still loads third-party assets and runtime packages from public CDNs, so network access is required for those dependencies.

## Known Limitations

- Extraction depends on the text layout produced by PDF.js. Scanned image-only PDFs or PDFs with unusual text positioning may not extract correctly.
- The parser is tuned for Coretax PDF formats matching the current field labels and section structure.
- Only the first page of each PDF is parsed.
- Very large batches may still be limited by browser memory, although processing is grouped in batches of 50 files.

## Repository Structure

```text
.
|-- index.html   # Static browser app
`-- README.md    # Project documentation
```
