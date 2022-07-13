| :warning: This repository was forked from @ErikvdVen's [php-gif](https://github.com/ErikvdVen/php-gif). It is minorly updated to work with PHP 8.
| ---
# PHP GIF Reborn
[![Latest Stable Version](https://poser.pugx.org/erikvdven/php-gif/v/stable)](https://packagist.org/packages/erikvdven/php-gif)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=erikvandeven100%40hotmail%2ecom&lc=NL&item_name=Erik%20van%20de%20Ven%20Github)

Below GIF image is an example image which can contain real-time data. A PHP script calculates the pending time till new year and generates the GIF image. An ideal solution for sending e-mails with real-time data to customers. E-mail clients give you the opportunity to load images by URL and so everytime the client re-opens the e-mail message, the GIF will be re-generated with real-time data.

For below image this doesn't work, unfortunately, because GitHub downloads the image once and stores it locally. Most e-mail clients, however, do load the images directly from source. Successfully tested with Gmail and Outlook 2011 (Mac OSX). 

*Important note: Outlook 2007, 2010 and 2013 for Windows will only show the first frame. TIP!: Keep the first frame universal, so it doesn't matter the GIF image animates or not.*

_There used to be a demo of the countdown below, but it is currently not working as of March 2022._
![Live countdown to new year](http://only-media.nl/gif/gif.php)

## Important Information
This package relies on the Lato font. You can download it from Google Fonts [here](https://fonts.google.com/specimen/Lato). Copy the TTF files into the fonts folder. Otherwise, the GIF will be blank.

## Installing PHP GIF Reborn
1. Download the repo
2. Open the src/Gif folder
3. Copy GIFEncoder.php and GIFGenerator.php into your file
4. Paste the following code at the top of your file:
```php
include 'GIFEncoder.php';
include 'GIFGenerator.php';
```
## Getting Started

Create a PHP file and add these headers at the beginning of the file:

```php
// Caching disable headers
header("Cache-Control: no-store, no-cache, must-revalidate, max-age=0");
header("Cache-Control: post-check=0, pre-check=0", false);
header("Pragma: no-cache");

// Output as a GIF image
header ('Content-type:image/gif');

// Import the GIFEncoder and GIFGenerator PHP files
include 'GIFEncoder.php';
include 'GIFGenerator.php';
```

On the next lines you can create a GIF image by first initializing the GIFGenerator object and creating an array with all the image frames:

```php
// Initialize a new GIFGenerator object
$gif = new GIFGenerator();

// Create a multidimensional array with all the image frames
$imageFrames = array(
	'repeat' => false,
	'frames' => array(
		array(
			'image' => './images/newyear.jpg',
			'text' => array(
				array(
					'text' => 'Hello GIF frame 1',
					'fonts-color' => '#000',
					'x-position' => 140,
					'y-position' => 138
				)
			),
			'delay' => 100
		),
	)
);
```
Finally you generate the image and `echo` the results on the screen: 

```php
echo $gif->generate($imageFrames);
```

## Example

A more complete example. You could copy/paste below code to a file and execute it in the browser to view a more complete result. As you can see it's not required to use text in your GIF image and you can add as much text per frame, and as much frames per GIF image as you like.

```php
<?php
// Caching disable headers
header("Cache-Control: no-store, no-cache, must-revalidate, max-age=0");
header("Cache-Control: post-check=0, pre-check=0", false);
header("Pragma: no-cache");

// Output as a GIF image
header ('Content-type:image/gif');

// Include the GIFEncoder and GIFGenerator PHP files
include 'GIFEncoder.php';
include 'GIFGenerator.php';

// Initialize a new GIFGenerator object
$gif = new GIFGenerator();

// Create a multidimensional array with all the image frames
$imageFrames = array(
	'repeat' => 5,
	'frames' => array(
		array(
			'image' => './images/newyear.jpg',
			'text' => array(
				array(
					'text' => 'Hello GIF frame 1',
					'fonts' => './fonts/Lato-Light.ttf',
					'fonts-size' => 30,
					'angle' => 0,
					'fonts-color' => '#000',
					'x-position' => 140,
					'y-position' => 138
				)
			),
			'delay' => 100
		),
		array(
			'image' => './images/newyear.jpg',
			'text' => array(
				array(
					'text' => 'Hello GIF frame 2',
					'fonts' => './fonts/Lato-Light.ttf',
					'fonts-size' => 15,
					'angle' => 0,
					'fonts-color' => '#000',
					'x-position' => 140,
					'y-position' => 138
				),
				array(
					'text' => 'Hello GIF frame 2',
					'fonts' => './fonts/Lato-Light.ttf',
					'fonts-size' => 15,
					'angle' => 0,
					'fonts-color' => '#000',
					'x-position' => 140,
					'y-position' => 108
				)
			),
			'delay' => 100
		),
		array(
			'image' => './images/newyear.jpg',
			'delay' => 50
		)
	)
);

echo $gif->generate($imageFrames);
?>
```

## License & Credits

This software is published under the [MIT License](https://en.wikipedia.org/wiki/MIT_License).

###### GIFEncoder

GIFEncoder.class.php contains minor adaptations from the GIFEncoder PHP class by [László Zsidi](http://gifs.hu).
