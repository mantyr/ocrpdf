# ocrpdf

*A tool to convert scanned documents into searchable PDFs*

`ocrpdf` recognises and extracts text from scanned documents then combines them into (generally) searchable PDFs that look like the original document. It uses the open source [Tesseract](https://tesseract-ocr.googlecode.com) library for OCR, [Leptonica](http://leptonica.com) for image manipiulation, [gofpdf](code.google.com/p/gofpdf) for document generation, and [kingpin](https://github.com/alecthomas/kingpin) for CLI support.

## I demand a GUI!

You're probably better off with [`gscan2pdf`](http://gscan2pdf.sourceforge.net/), which was the original inspiration for this tool (obligatory Sourceforge warning)

## Installation

Use `go install bitbucket.org/johnsto/ocrpdf` to install `ocrpdf`

Both the Leptonica and Tesseract libraries must be installed.

### Leptonica

Ensure that you have the Leptonica 1.71 library installed.

* Debian: `apt-get install liblept3` (Jessie or newer)
* Fedora: `yum install leptonica`
* Arch: `pacman -S leptonica`
* Windows: uh...

### Tesseract

Ensure that you have the Tesseract 3.03.03 library and data files installed.

* Debian: `apt-get install libtesseract3 tesseract-ocr` (Jessie or newer)
* Fedora: `yum install tesseract`
* Arch `pacman -S tesseract tesseract-data-eng`
* Windows: er...

## Usage

Converting a scanned image is as simple as:

`ocrpdf scan.jpg`

By default, `ocrpdf` will take the filename name of the first input scan as the output document name, in this case, `scan.pdf`.

You can also specify a document size, output filename, document title, enable compression and specify multiple pages:

    ocrpdf -s letter \
           -o taxes.pdf \
           -t "2015 Taxes" \
           --compress \
           taxes1.jpg taxes2.jpg taxes3.jpg

Automatic contrast enhancement to improve the legibility of the text is performed by default, you can disable this with the `--contrast=0` flag.

## Image support

Reading JPEGs, PNGs and TIFs is supported, plus any other formats that Leptonica supports. Images in outputted PDF will be either JPEG or PNG, based on the input format of the respective image. You can force a specific output format using the `--format` parameter.

## PDF Structure

Pages in the output PDF contain two layers, one with the recognised text, and one with the scanned image. The image is positioned and arranged on top of the text.

In PDF viewers like `evince`, this arrangement lets you search and select text as if it were an invisible layer on top of the image.
