textract
========

A text extraction node module.

[![NPM](https://nodei.co/npm/textract.png?compact=true)](https://nodei.co/npm/textract/)
[![NPM](https://nodei.co/npm-dl/textract.png)](https://nodei.co/npm/textract/)

## Currently Extracts...

* PDF
* DOC
* DOCX
* XLS
* XLSX
* PPTX
* DXF
* PNG
* JPG
* `application/javascript`
* All `text/*` mime-types.

Does textract not extract from files of the type you need?  Add an issue or submit a pull request.  It's super easy to add an extractor for a new mime type.

## Install

```
npm install textract
```

## Requirements

* `PDF` extraction requires `pdftotext` be installed, [link](http://www.foolabs.com/xpdf/download.html)
* `DOC` extraction requires `catdoc` be installed, [link](http://www.wagner.pp.ru/~vitus/software/catdoc/)
* `XLS` extraction requires `xls2csv` be installed (it comes with `catdoc`), [link](http://www.wagner.pp.ru/~vitus/software/catdoc/)
* `DOCX` extraction requires `unzip` be available
* `XLSX` extraction requires `unzip` be available
* `PPTX` extraction requires `unzip` be available
* `PNG` and `JPG` require `tesseract` to be available, [link](http://code.google.com/p/tesseract-ocr/).  Images need to be pretty clear, high DPI and made almost entirely of just text for `tesseract` to be able to accurately extract the text.
* `DXF` extraction requires `drawingtotext` be available, [link](https://github.com/davidworkman9/drawingtotext)

## Usage

### Commmand Line

If textract is installed gloablly, via `npm install -g textract`, then the following command will write the extracted text to the console.

```
$ textract pathToFile
```

### In your node app

#### Import

```javascript
var textract = require('textract');
```

#### Execution

If you do not know the mime type of the file

```javascript
textract(filePath, function( error, text ) {})
```

If you know the mime type of the file

```javascript
textract(type, filePath, function( error, text ) {})
```

If you wish to pass some config...and know the mime type...

```javascript
textract(type, filePath, config, function( error, text ) {})
```

If you wish to pass some config, but do not know the mime type

```javascript
textract(filePath, config, function( error, text ) {})
```

Error will contain informative text about why the extraction failed. If textract does not currently extract files of the type provided, a `typeNotFound` flag will be tossed on the error object.

## Configuration

Configuration can be passed into textract.  The following configuration options are available

* `preserveLineBreaks`: By default textract does NOT preserve line breaks. Pass this in as `true` and textract will not strip any line breaks.
* `exec`: Some extractors (xlsx, docx, dxf) use node's `exec` functionality. This setting allows for providing [config to `exec` execution](http://nodejs.org/api/child_process.html#child_process_child_process_exec_command_options_callback). One reason you might want to provide this config is if you are dealing with very large files. You might want to increase the `exec` `maxBuffer` setting.
* `[ext].exec`: Each extractor can take specific exec config.



