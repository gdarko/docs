---
title: File
category: field-types
group: Content
status: draft
---

## Description
The file field allows a file to be uploaded and selected by making use of the native WP media popup.

## Screenshots
<div class="gallery">
	<figure>
		<a href="https://raw.githubusercontent.com/AdvancedCustomFields/docs/master/assets/acf-file-field-interface.jpg">
			<img src="https://raw.githubusercontent.com/AdvancedCustomFields/docs/master/assets/acf-file-field-interface.jpg" alt="A file field that allows you to upload and select a file" />
		</a>
		<figcaption>The File field interface</figcaption>
	</figure>
	<figure>
		<a href="https://raw.githubusercontent.com/AdvancedCustomFields/docs/master/assets/acf-file-field-settings.jpg">
			<img src="https://raw.githubusercontent.com/AdvancedCustomFields/docs/master/assets/acf-file-field-settings.jpg" alt="The list of File field settings shown when setting up a File field" />
		</a>
		<figcaption>The File field settings</figcaption>
	</figure>
</div>

## Changelog
- Added `minimum` setting in version 5.1.9.
- Added `maximum` setting in version 5.1.9.
- Added `allowed file types` setting in version 5.1.9.

## Settings
- **Return value**
  Customize the returned data. Choose from File Array (array of data), File URL (string), or File ID (integer).

- **Library**
  Limit the file selection to only those that have been uploaded to this post, or the entire library.

- **Minimum**
  Add upload validation for minimum filesize in MB (integer). The filesize may also be entered as a string containing the unit. eg. ’400 KB’.

- **Maximum**
  Add upload validation for maximum filesize.

- **Allowed file types**
  Add upload validation for specific file types. Enter a comma separated list to specify which file types are allowed or leave blank for all types.

## Template usage

The file field will return either an array, a string or an integer value depending on the `return value` set. Below are some examples of how you can use this data.

### Basic display (Object)
This example demonstrates how to display the selected file when using the `array` return type. This return type allows us to easily access data such as `url` and `filename`.

```
<?php

$file = get_field( 'file' );

// Show link to file.
if( $file ): ?>

	<a href="<?php echo $file['url']; ?>"><?php echo $file['filename']; ?></a>

<?php endif; ?>
```

### Customized display (Object)
This example demonstrates how to display a custom link when using the `object` return type. This return type allows us to easily access data such as `url`, `title`, `type` and more. To see the full data available, please debug the [$file variable](https://www.advancedcustomfields.com/resources/how-to/debug/).

```
<?php

$file = get_field( 'file' );

// Create markup for custom link using the available variables.
if( $file ):

	$url = $file['url'];
	$title = $file['title'];
	$caption = $file['caption'];

	$icon = $file['icon'];

	// Set the thumbnail as $icon if the file type is 'image'.
	if( $file['type'] == 'image' ) {
		$icon =  $file['sizes']['thumbnail'];
	}

	if( $caption ): ?>

		<div class="wp-caption">

	<?php endif; ?>

	<a href="<?php echo $url; ?>" title="<?php echo $title; ?>">
		<img src="<?php echo $icon; ?>" />
		<span><?php echo $title; ?></span>
	</a>

	<?php if( $caption ): ?>

			<p class="wp-caption-text"><?php echo $caption; ?></p>

		</div>

	<?php endif; ?>
<?php endif; ?>
```

### Basic display (ID)
This example demonstrates how to display the selected file when using the `ID` return type. This return type allows us to efficiently load only the necessary data.

```
<?php

$file = get_field( 'file' );

if( $file ) {

	$url = wp_get_attachment_url( $file );

	?><a href="<?php echo $url; ?>" >Download File</a>

<?php } ?>
```

### Basic display (URL)
This example demonstrates how to display the selected file when using the `URL` return type. This return type allows us to efficiently display a basic link but prevents us from loading any extra data about the file.

```
<?php if( get_field( 'file' ) ): ?>

	<a href="<?php the_field( 'file' ); ?>" >Download File</a>

<?php endif; ?>
```