urlparser - 0.1.5 - BETA
-------------
[![Build Status](https://travis-ci.org/codenamegary/url-parser.png?branch=0.1.5-beta)](https://travis-ci.org/codenamegary/url-parser)

The best little URL tool for PHP!

#####Features

- Fully tested
- Chainable methods
- PSR-0 autoload and PSR-1 compliant
- Friendly syntax for Segment, Query String and other URL part manipulation

#####Coming Soon

- Batch wrapper for processing multiple URLs
- Composer / Packagist publishing

###Installation

#####Manually
Download the Master ( [.zip](https://bitbucket.org/codenamegary/urlparser/get/master.zip) [.gz](https://bitbucket.org/codenamegary/urlparser/get/master.tar.gz) [.bz2](https://bitbucket.org/codenamegary/urlparser/get/master.tar.bz2) )

- Extract to the location of your choosing
- Include url.php
 - @include('path/to/extracted/files/src/codenamegary/urlparser/URL.php');
- **OR** use a PSR-0 compatible Autoloader of your choice
 - Map namespace "codenamegary" => 'path/to/extracted/files/src/codenamegary'

#####Composer via Packagist

- In composer.json add "codenamegary/url-parser": "0.1.5-beta" to require

###Docs

- PHPDocs are included in the repo under 'path/to/extracted/files/docs/index.html'
- Plenty of documentation and examples throughout the source in [url.php](https://bitbucket.org/codenamegary/url-parser/src/b35343be3583178d870e2e7ebc0d9b6120d7ca2a/src/codenamegary/urlparser/URL.php?at=master)

#Usage Examples

###Load a complex URL and merge in some query parameters.

```php
$url = new codenamegary\urlparser\URL('https://maps.google.ca/maps?saddr=Tokyo,+Japan&daddr=Toronto,+ON&hl=en&sll=43.653226,-79.383184&sspn=0.444641,1.056747&geocode=FRCUIAIduoZTCCnnVy7whxtdYDGJG1cii2EBLg%3BFWoYmgIdcLVE-ymlO8bXkMvUiTF3xLQqUFU1Mg&oq=tokyo&mra=ls&t=m&z=3');
$url->addQuery(array(
	'foo'	=> 'bar',
));
echo $url->make();
```

####Returns

https://maps.google.ca/maps?saddr=Tokyo,+Japan&daddr=Toronto,+ON&hl=en&sll=43.653226,-79.383184&sspn=0.444641,1.056747&geocode=FRCUIAIduoZTCCnnVy7whxtdYDGJG1cii2EBLg%3BFWoYmgIdcLVE-ymlO8bXkMvUiTF3xLQqUFU1Mg&oq=tokyo&mra=ls&t=m&z=3&foo=bar

###Load a complex URL and get rid of some query parameters.

```php
$url = new codenamegary\urlparser\URL('https://maps.google.ca/maps?saddr=Tokyo,+Japan&daddr=Toronto,+ON&hl=en&sll=43.653226,-79.383184&sspn=0.444641,1.056747&geocode=FRCUIAIduoZTCCnnVy7whxtdYDGJG1cii2EBLg%3BFWoYmgIdcLVE-ymlO8bXkMvUiTF3xLQqUFU1Mg&oq=tokyo&mra=ls&t=m&z=3');
$url->stripQuery('geocode');
echo $url->make();
```
####Returns

https://maps.google.ca/maps?saddr=Tokyo,+Japan&daddr=Toronto,+ON&hl=en&sll=43.653226,-79.383184&sspn=0.444641,1.056747&oq=tokyo&mra=ls&t=m&z=3

###Get an instance of the URL parser for the page currently being visited

```php
// .. and strip all the segments and query string from the URI
$url = new codenamegary\urlparser\URL;
$url->stripSegments()
    ->stripQueries()
    ->make();
echo $url;
```
####Returns

Full URL of the current page minus the URI segments and query string.

###Swap a URI string

```php
$url = new codenamegary\urlparser\URL('http://www.apple.com/bananas/coconut/date/elephant/giraffe');
$url->swapSegment('date','raisin');
echo $url->make();
```

####Returns

http://www.apple.com/bananas/coconut/raisin/elephant/giraffe

###Put something in front of coconut

```php
$url = new codenamegary\urlparser\URL('http://www.apple.com/bananas/coconut/date/elephant/giraffe')
    ->prependSegment('lime','coconut');
echo $url->make();
```

####Returns

http://www.apple.com/bananas/lime/coconut/date/elephant/giraffe

###Change the host and protocol using method chaining

```php
$url = codenamegary\urlparser\URL::to('http://www.apple.com/bananas/coconut/date/elephant/giraffe')->host('www.microsoft.com')->protocol('ftp');
echo $url->make();
```

####Returns

ftp://www.microsoft.com/bananas/coconut/date/elephant/giraffe
