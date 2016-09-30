NX Print
========

NX Print provides secure access to Windows' printing infrastructure from the browser.

Use cases:

- Need to print from the browser automatically?
- End users don't want to click around the print dialog, choose printer and printer setings.
- Print PDF just-like-you-see-it to the printer (no more browser-based differences)
- Raw printer-level access (control the printer in its own language)

If you need to print labels, we also have [LabelCloud](https://function61.com/products/labelcloud/)
offering, which is built on NX Print's technology.

Download
--------

Downloads and more info from [function61.com/products/nxprint](https://function61.com/products/nxprint/)

Licensing
---------

NX Print is not free software - only this documentation is covered under GPL. [Contact us for licensing](https://function61.com/products/nxprint/).

Demo website
------------

[View demo website](https://s3.amazonaws.com/xs.fi/nx/example/nx.nxprint_1_0-demo.html).

TODO: just link to LabelCloud go.

API
---

### Prerequisites

Include in your HTML:

```html
<script src="nx.js"></script>
<script src="nx-print.js"></script>
```

This .js files you find from the install paths of NX and NX Print on your computer.

TODO: improve this mechanism.

### List printers

```javascript
NX.nxprint_1_0.listWorkstationPrintQueues(function (err, printers) {
	if (err) { throw err; }

	console.log(printers)
});

// => ["Microsoft XPS Document Writer", "Microsoft Print to PDF", "Fax"]

```

### Print PDF

```javascript
NX.nxprint_1_0.print_pdf_http({
	printQueueName: 'HP LaserJet 1234',

	// URL which generates a PDF document
	documentUrl: 'https://example.com/api/generate_pdf?invoiceId=465923',

	papersource: 'Tray B' // not required
}, function (err, printers) {
	if (err) { throw err; }

	console.log('printing done');
});

```

### Print raw

```javascript
NX.nxprint_1_0.print_file_http(
	'HP LaserJet 1234',
	'https://example.com/api/generate_labels_rawcontrolcodes?id=12358',
	'print_job_1234',
	function (err) {
		if (err) { throw err; }

		console.log('printing done');
	}
);

```

### Get printer details

```javascript
NX.nxprint_1_0.get_printer_details('HP LaserJet 1234', function (err, details) {
	if (err) { throw err; }

	console.log(details.stdout_json);
});

// => {driver_name: "Microsoft Print To PDF", friendly_name: "Microsoft Print to PDF", paper_sources: []}

```

Security
--------

Head over to NX documentation which covers the security aspects also provided for NX Print.

Browser support
---------------

Supports all desktop browsers.
