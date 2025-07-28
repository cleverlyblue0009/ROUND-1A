# *Project Title: PDF Heading and Title Extractor*

## *Objective*

This project aims to automatically extract structured outlines—specifically the document title and headings (H1 to H4)—from PDF files using layout-based analysis. The system converts unstructured PDF content into a clean, machine-readable format (JSON), which can be useful for applications like document indexing, content summarization, or knowledge graph generation.

## *What the Project Does*

The program processes all PDF files located in the input/ directory. It utilizes the PyMuPDF library to extract both text and its layout metadata (such as font size and position) from each page of the PDF. This information is then used to determine the document's structure, including the title and hierarchical headings.

The program identifies the document title by analyzing the first page and selecting the most visually dominant text, typically the largest and most centrally placed. It classifies other headings (like H1, H2, H3, and H4) based on font size differences, text formatting (such as uppercase), and numbering patterns (e.g., 1., 1.1., etc.).

To improve accuracy, irrelevant content—like page numbers, headers, or short decorative elements—is filtered out. Each PDF is then analyzed, and the extracted information is saved as a structured JSON file in the output/ folder.

## *Key Components and Their Roles*

* extract_text_with_metadata(pdf_path): Reads a PDF and returns blocks of text with their font sizes, positions, and other metadata using PyMuPDF.

* get_heading_hierarchy(text_blocks): Analyzes font sizes in the document to build a hierarchy and distinguish between different heading levels and body text.

* get_pdf_title(text_blocks): Identifies the most likely title on the first page based on the largest font size and top-central placement.

* detect_headings(text_blocks, title): Detects heading levels using font size thresholds, case styles (like UPPERCASE), and section numbering formats.

* analyze_pdf(pdf_path): Coordinates the full processing pipeline—detecting language, extracting the title and headings, and returning the structured result.

* main(): Iterates through all PDFs in the input/ directory, processes them one by one using analyze_pdf(), and stores the results in output/ as .json files.

## **How It Works **

The code starts by reading each PDF file using PyMuPDF, which allows access to both textual content and layout information. It processes the PDF page by page, collecting data such as font size, text position, and text content. This metadata is crucial for determining the structural importance of each line of text.

The system then identifies the title of the document, usually found at the top of the first page, by selecting the line with the largest font size that is also centrally placed.

Next, the heading detection function compares font sizes and text patterns to identify different levels of headings. For example, section headers that use numbering (like "2.3.1") or are in all-caps are flagged as potential headings. The font hierarchy is dynamically determined per document, which makes the extractor generalizable across different formatting styles.

Short lines or repeated patterns often found in headers, footers, or decorative separators are ignored to maintain a clean structure.

Once all relevant information is gathered, the program creates a dictionary containing the title, headings, and their hierarchical relationships. This dictionary is saved as a JSON file, which can then be used for downstream applications such as indexing, navigation menus, or even generating a table of contents.

The code is modular, efficient, and designed to handle a wide range of PDFs without relying on OCR or external templates.

---

## *Sample Input*

A sample input could be a PDF file named sample.pdf placed inside the input/ directory. This file might include the following:


Title: Introduction to Machine Learning

1. Basics of ML
1.1 Supervised Learning
1.2 Unsupervised Learning
2. Applications
2.1 Image Classification
2.2 Natural Language Processing


---

## *Sample Output (JSON)*

json
{
  "title": "Introduction to Machine Learning",
  "headings": [
    {
      "level": "H1",
      "text": "1. Basics of ML"
    },
    {
      "level": "H2",
      "text": "1.1 Supervised Learning"
    },
    {
      "level": "H2",
      "text": "1.2 Unsupervised Learning"
    },
    {
      "level": "H1",
      "text": "2. Applications"
    },
    {
      "level": "H2",
      "text": "2.1 Image Classification"
    },
    {
      "level": "H2",
      "text": "2.2 Natural Language Processing"
    }
  ]
}
