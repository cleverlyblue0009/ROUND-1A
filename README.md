# Adobe PDF Outline Extraction

This module extracts document outlines and headings from PDF files, outputting structured JSON for each input PDF.

## Features

- Extracts text and metadata (font size, position) from PDFs.
- Detects document title and heading hierarchy (H1, H2, etc.).
- Outputs a JSON file per PDF with the detected title and outline.

## How to Run

### 1. (Optional) Create and activate a virtual environment

bash
python3 -m venv venv
source venv/bin/activate


### 2. Install dependencies

bash
pip install -r requirements.txt


### 3. Place your PDF files

Put your PDF files in the input/ directory inside adobe/.

### 4. Run the script

bash
python main.py


### 5. Output

- JSON files will be generated in the output/ directory, one per input PDF.

## Dependencies

- pymupdf (fitz)
- langdetect

Install with:
bash
pip install -r requirements.txt
