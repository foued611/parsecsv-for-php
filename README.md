# parseCSV
<a href='https://travis-ci.org/foued611/parsecsv' ><img  src='https://travis-ci.org/foued611/parsecsv.svg?branch=master'></a>


Note: parseCSV is now being revised to PHP 5 standards. If you have an issue or a feature request we encourage you to open an issue.

parseCSV is an easy to use PHP class that reads and writes CSV data properly. It
fully conforms to the specifications outlined on the on the
[Wikipedia article][CSV]. It has many advanced features which help make your
life easier when dealing with CSV data.

This library was originaly created in early 2007 by [jimeh](https://github.com/foued611) due to the lack of built-in
and third-party support for handling CSV data in PHP.

[csv]: http://en.wikipedia.org/wiki/Comma-separated_values

## Installation

**Installation using Composer.**

_Include the following in your composer.json_

```
 "foued611/parsecsv": "dev-master"
```

**psr-0 namespace autoloading.**

```php
use Parse\Csv\ParseCSV;
```

_You may also manually include the ParseCSV.php file_

```php
require_once ('parsecsv/src/Parse/Csv/ParseInterface.php');
require_once ('parsecsv/src/Parse/csv/ParseCSV.php');
```

## Features

* ParseCSV is the only complete and fully featured CSV solution for PHP (as
  far as I know).
* Supports enclosed values, enclosed commas, double quotes and new lines.
* Automatic delimiter character detection.
* Sort data by specific fields/columns.
* Easy data manipulation.
* Basic SQL-like _conditions_, _offset_ and _limit_ options for filtering
  data.
* Error detection for incorrectly formatted input. It attempts to be
  intelligent, but can not be trusted 100% due to the structure of CSV, and
  how different programs like Excel for example outputs CSV data.
* Support for character encoding conversion using PHP's _iconv_ function
  (requires PHP 5.4).
* Supports both PHP 5.4


## Example Usage

**General**

```php
$csv = new ParseCSV('data.csv');
print_r($csv->data);
```

**Tab delimited, and encoding conversion**

```php
$csv = new \Parse\Csv\ParseCSV();
$csv->encoding('UTF-16', 'UTF-8');
$csv->delimiter = "\t";
$csv->parse('data.tsv');
print_r($csv->data);
```

**Auto-detect delimiter character**

```php
$csv = new ParseCSV();
$csv->auto('data.csv');
print_r($csv->data);
```

**Modify data in a CSV file**

```php
$csv = new \Parse\Csv\ParseCSV();
$csv->sort_by = 'id';
$csv->parse('data.csv');
# "4" is the value of the "id" column of the CSV row
$csv->data[4] = array('firstname' => 'John', 'lastname' => 'Doe', 'email' => 'john@doe.com');
$csv->save();
```

**Add row/entry to end of CSV file**

_Only recommended when you know the extact sctructure of the file._

```php
$csv = new ParseCSV();
$csv->save('data.csv', array('1986', 'Home', 'Nowhere', ''), true);
```

**Convert 2D array to csv data and send headers to browser to treat output as
a file and download it**

```php
$csv = new ParseCSV();
$csv->output('movies.csv', $array, array('field 1', 'field 2'), ',');
```


## License

(The MIT license)

Copyright (c) 2014 Jim Myhrberg.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
