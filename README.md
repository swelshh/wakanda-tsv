## Notes

This is a quick little script to import tab separated/delimited data into your datastore classes using tab separated/delimited text files.

The wakanda-tsv.js file is setup to be used as a CommonJS module.  So you'll need to create a folder named modules and put the wakanda-tsv.js file in there.

The importTabDelim function makes a few assumptions:

1. That you are storing the tab delim import files in a directory at project/import
2. That you are naming your primary key fields 'ID' and they are of type long

## Example

If you had a datastore class named Product with the following attributes:

* Product.ID
* Product.partNo
* Product.name
* Product.releaseDate

And you had a tab delimited text file with these columns stored at project/import/products.txt:

ProductID, ReleaseDate, Part#, Name

You could import those records in a server side javascript file like this:

```javascript
var utl = require('wakanda-tsv');

/**
 * @param {String} dsClassName Name of the datastore class we are importing data into.
 * @param {String} fileName File name stored in project/import.
 * @param {Bool} hdrRow If the file to import has a header row.
 * @param {String[]} attributeNames Attribute names corresponding to import file columns.
 * @return {String} Summary of the import.
 */
importSummary = utl.importTabDelim("Product", "products.txt", true, ["ID", "releaseDate", "partNo", "name"]);

importSummary; //display the import summary in the console
```

Note that if you import an ID column, the import script is smart enough to skip importing existing records and will also update the sequence number for the ID after finishing the import.

## References

* http://en.wikipedia.org/wiki/Tab-separated_values
* http://www.cs.tut.fi/~jkorpela/TSV.html

## License

Copyright 2011 - 2013 CoreBits DataWorks LLC

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

