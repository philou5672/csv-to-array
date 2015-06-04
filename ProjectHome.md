# csv to array v2.1 #
A compact (645 bytes) but compliant function to convert a CSV string into a 2D array, conforming to the [RFC4180](#RFC4180_Summary.md) standard.

## csv to array v2.1 Summary ##

100% speed increase over previous versions, clearer option passing method, option for removal of leading, trailing white space from fields, options to override record separator with up to 2 characters, override for field separator and enclosing character.

## Planned for csv to array v2.2 ##

Custom escape character, ability to output as object, ability to fetch single row, or range of rows.

## csv to array Browser Tests ##
| **IE5.5 to IE10** | **Chrome 1+** | **Firefox 1+** | **Safari 3+** | **Opera 9+** |
|:------------------|:--------------|:---------------|:--------------|:-------------|
| OK                | OK            | OK             | OK            | OK           |

## csv to array Options ##

| | **Default** | |
|:|:------------|:|
|fSep|','          |'1 character'|
|rSep|'\r\n'       |'1-2 characters'|
|quot|'"'          |'1 character'|
|head|false        |true|
|trim|false        |true|

When overriding the enclosing character, the character will be used to escape its self for example, if the enclosing character is set to ' then a field containing a ' will need to be as follows 'I said, ''This is a quote''' but if the enclosing character is set to # it would be #I said, 'This is a quote'#

## csv to array jQuery ##
```javascript

$.ajax({
url: "test.csv",
dataType: 'text',
cache: false
}).done(function(csvAsString){
csvAsArray=csvAsString.csvToArray();
});
```
## csv to array Common usage: Javascript ##
```
csvAsArray = csvAsString.csvToArray();
```

#### Override field separator with # character ####
```
csvAsArray = csvAsString.csvToArray({ fSep:'#' });
```

#### Override record separator with || characters ####
```
csvAsArray = csvAsString.csvToArray({ rSep:'||' });
```

#### Override enclosing character with ' character ####
```
csvAsArray = csvAsString.csvToArray({ quot:"'" });
```

#### Omit Header ####
```
csvAsArray = csvAsString.csvToArray({ head:true });
```

#### Remove leading, trailing white space from fields ####
```
csvAsArray = csvAsString.csvToArray({ trim:true });
```

#### Override record separator with || and trim white space from fields ####
```
csvAsArray = csvAsString.csvToArray({ rSep:'||' , trim:true });
```

## csv to array javascript Test 1 ##
```
csvAsStringA = 'Header 1,Header 2,Header 3\r\n'
            + ',"","Test ""Quotes"""\r\n'
            + '"Test , Separator","Test \r\nCRLF",   Test    White   Space   \r\n'
            + ' '; //Some accidental white space on optional last row

csvAsArrayA = csvAsStringA.csvToArray({head:true});
```
#### Result ####
```
csvAsArrayA
(
[0] => Array
	(
	[0] => ||
	[1] => ||
	[2] => |Test "Quotes"|
	)
[1] => Array
	(
	[0] => |Test , Separator|
	[1] => |Test \r\nCRLF|
	[2] => |   Test    White   Space   |
	)
)

alert(csvAsArrayA[1][0]); //will alert "Test , Separator"
```
## csv to array javascript Test 2 ##
```
csvAsStringB = "Header 1#Header 2#Header 3||"
            + "#''#'Test ''Quotes'''||"
            + "'Test # Separator'#'Test ||CRLF'#   Test    White   Space   ||"
            + " "; //Some accidental white space on optional last row

csvAsArrayB = csvAsStringB.csvToArray({ rSep:'||' , fSep:'#' , quot:"'" , trim:true });
```
#### Result ####
```
csvAsArrayB
(
[0] => Array
        (
        [0] => |Header 1|
        [1] => |Header 2|
        [2] => |Header 3|
        )
[1] => Array
        (
        [0] => ||
        [1] => ||
        [2] => |Test 'Quotes'|
        )
[2] => Array
        (
        [0] => |Test # Separator|
        [1] => |Test ||CRLF|
        [2] => |Test    White   Space|
        )
)
```
## Change log ##
### v2.1 (Apr 21 2013) ###
Fixed IE8 bug

Changed the output formatting function used in the demo due to it not working properly in firefox and moved demo to my server due to jsFiddle not working on IE8
### v2.0 (Apr 21 2013) ###
Full rewrite, 100% speed increase

Added ability to override enclosing character

Added ability to remove leading, trailing white space

Added ability to override up to 2 characters for record separation

Changed to a clearer method of option passing
### v1.3 (Apr 17 2013) ###
Added ability to skip header line

Fixed issue where right hand side white space would be removed from the last field of the last record if it was not quote enclosed
### v1.2 (Apr 17 2013) ###
Changed from basic function to String extension for chainability

Discontinued jQuery specific version due to minimal difference

Changed the handling of new line characters
### v1.1 (Oct 22 2012) ###
Added optional record and field separator overrides
### v1.0 (Oct 21 2012) ###
Initial release
## RFC4180 Summary ##
Full Details: [RFC4180](http://tools.ietf.org/html/rfc4180)

  1. Each record is located on a separate line, delimited by a line break (CRLF or \r\n)
  1. The last record in the file may or may not have an ending line break
  1. There maybe an optional header line appearing as the first line of the file with the same format as normal record lines
  1. Spaces are considered part of a field and should not be ignored
  1. Each field may or may not be enclosed in double quotes
  1. Fields containing line breaks, double quotes, or commas should be enclosed in double-quotes
  1. Double-quotes inside a double-quote enclosed field must be escaped by preceding it with another double quote

## License ##
Copyright (c) 2012-2013 Daniel Tillin

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
## Feature Set/Alternative Comparison ##
| **Name** | **RFC4180** | **`JavaScript Type`** | **(separators)`[overrideable]`** | **Skip Header** |
|:---------|:------------|:----------------------|:---------------------------------|:----------------|
|[csvToArray v2.1](#csvToArray_v2.1.md)|Pass         |standard               |[,] [\n\r] ["]                    |Yes              |
|[splitCSV](http://www.greywyvern.com/?post=258)|Fail `[1]`   |standard               |[,] (\n\r) (")                    |No               |
|[CSVToArray()](http://stackoverflow.com/a/1293163/1703848)|Fail `[2]`   |standard               |[,] (\n\r) (")                    |No               |
|[js-tables](http://code.google.com/p/js-tables/source/browse/trunk/jquery.csv.js)|Fail `[3]`   |jQuery                 |[,] (\r or \n or \r\n) [" or ']   |No `[a]`         |
|[jquery-csv 0.7 (Beta)](http://code.google.com/p/jquery-csv/)|Pass         |jQuery                 |[,] (\r\n) ["]                    |Yes              |
|[csv.pegjs](http://gist.github.com/trevordixon/3362830)|Pass         |PEG                    |[,] (\n\r) (")                    |No               |
|[parseCSV](http://stackoverflow.com/a/14991797/1703848)|Fail `[4]`   |standard               |(,) (\n) (")                      |No               |
|[csv2array](http://www.speqmath.com/tutorials/csv2array/)|Fail `[5]`   |standard               |[,] (\n) (")                      |No               |

  1. Only creates 1D array and fails on \r\n
  1. Fails on empty fields, double quoted or not, js error cannot call method 'replace' of undefined
  1. \r\n inside double quoted fields breaks to new record
  1. Breaks record on \n leaving \r in data, easy fix
  1. Does not accept an spaces in non double quoted fields, throws error

`[a]` Can return an array of hashes, whose keys are from the header row