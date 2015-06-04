# csvToArray v1.3 #

A compact (506 bytes) but compliant function to convert a CSV string into a 2D array, conforming to the [RFC4180](#RFC4180_Summary.md) standard.

## Options ##

| | **Default** | |
|:|:------------|:|
|Field Separator|","          |"single character"|
|Record Separator|"\r\n"       |"single character"|
|Skip CSV Header|0            |1|
0=No 1=Yes

## Common Usage: jQuery ##
```javascript

$.ajax({
url: "test.csv",
dataType: 'text',
cache: false
}).done(function(csvAsString){
csvAsArray=csvAsString.csvToArray();
});
```
## Common usage: Javascript ##
```
csvAsArray = csvAsString.csvToArray();
```

#### Override field separator ####
```
csvAsArray = csvAsString.csvToArray("|");
```

#### Override record separator ####
```
csvAsArray = csvAsString.csvToArray("", "#");
```

#### Override Skip Header ####
```
csvAsArray = csvAsString.csvToArray("", "", 1);
```

#### Override all ####
```
csvAsArray = csvAsString.csvToArray("|", "#", 1);
```
## Test ##
```javascript

csvAsString = 'Header 1,Header 2,Header 3\r\n'
+ ',"","Test ""Quotes"""\r\n'
+ '"Test , Separator","Test \r\nCRLF",   Test    White   Space   \r\n'
+ ' '; //Some accidental white space on optional last row

csvAsArray = csvAsString.csvToArray('','',1);```
#### Result ####
```
csvAsArray
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

alert(csvAsArray[1][0]); //will alert "Test , Separator"
```