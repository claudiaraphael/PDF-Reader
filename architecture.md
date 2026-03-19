# Personal PDF Study Tool: Project Architecture

## Objective: 
A native Desktop application for a personalized study workflow. The tool operates fully offline and allows for direct mouse interaction (click, drag, and highlight).

Leveraging a Python-based backend and a robust GUI, this architecture ensures high-performance document rendering and seamless local persistence.

# 🏗️ Offline Desktop Architecture

## 1. PDF Engine (Local Backend)

For a desktop app that requires permanent annotations, PyMuPDF (fitz) is the industry standard.

Why: It is extremely fast (C-based) and allows for programmatic "Highlight" annotations that remain compatible with external readers (Adobe, Edge, etc.).

Function: It opens the file, renders pages as images for the UI, and maps mouse-on-screen coordinates to the PDF's internal coordinate system to apply highlights.

# 2. Graphical User Interface (GUI)

For advanced mouse event handling and document visualization, PySide6 (the official Qt for Python) is recommended.

Advantage: Unlike web-based frameworks or basic libraries like Tkinter, Qt offers granular control over mouse/keyboard events and includes specialized widgets for document viewing.

Interaction: A QGraphicsView is used to display the PDF page and capture "drag" events for text selection.

# 3. Storage and Synchronization

Local: The application saves modifications directly to the .pdf file.

Optional Cloud: To maintain a "free and offline" approach, the strategy uses local directory monitoring (via Google Drive Desktop or Dropbox). The Python app saves locally, and the cloud service handles synchronization whenever internet access is available.

# 🛠️ Technical Stack

- Language: Python 3.10+

- GUI Framework: PySide6

- PDF Engine: PyMuPDF (pip install pymupdf)

- Packaging: PyInstaller or Nuitka (for .exe distribution).

# 📝 Project Roadmap

1. Module 1: The Viewer: Create a window to open PDF files and navigate pages. PyMuPDF generates a "pixmap" (image) for each page, which Qt displays natively.

2. Module 2: The Selector: Implement "Rectangle Capture" logic. The app tracks mouse drag events, draws a semi-transparent selection area, and maps those pixels to the PDF's real-world coordinates upon release.

3. Module 3: The Highlighter: Utilize the page.add_highlight_annot(quads) function to write yellow (or custom color) highlights directly into the file metadata.