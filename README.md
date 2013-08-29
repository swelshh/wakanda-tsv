## Notes

This is a quick little script to import tab delimited data into your datastore classes using tab delimited text files.

The utl.js file is setup to be used as a CommonJS module.  So you'll need to create a folder named modules and put the utl.js file in there.

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
var utl = require('utl');

/**
 * @param {String} dsClassName Name of the datastore class we are importing data into.
 * @param {String} fileName File name stored in project/import.
 * @param {Boolean} hdrRow If the file to import has a header row.
 * @param {String[]} attributeNames Attribute names corresponding to import file columns.
 * @return {String} Summary of the import.
 */
importSummary = utl.importTabDelim(
    "Product",
    "products.txt",
    true,
    ["ID", "releaseDate", "partNo", "name"]
);

console.log(importSummary); //display the import summary in the console
```

Note that if you import an ID column, the import script is smart enough to skip importing existing records and will also update the sequence number for the ID after finishing the import.

## License

Copyright 2011 - 2013 CoreBits DataWorks LLC  
http//corebitsdw.com  
Released under the MIT license (included in distribution in MIT LICENSE.txt)  


