
> **FORK:** This is a fork of [xpm](https://github.com/talwrii/xpm) that brings transparency to the table (literally and figuratively)

# XPM
A native python library for producing XPM files from raster images.
For parsing XPM files I recommend PIL.

## Usage

### Command line

    python -m xpm image.bpm > image.xpm

Though for this use case you might prefer imagemagick.

### Python code

Creates a 3x3 image of black and white pixels with varying transparency

	import xpm
	import sys

	# RGBA IN
	# Also supports RGB, RG and RED (grayscale)
	# Make sure your parser supports those options!
	black = (0, 0, 0, 127)
	white = (255, 255, 255, 192)
	image = [
			[black, white, black],
			[white, black, white],
			[black, white, black]]
	pixels = dict( ((i, j), colour)
		for j, row in enumerate(image)
			for i, colour in enumerate(row))
	xpm_im = xpm.XpmImage((3, 3), pixels).make_image()
	# XPM ARGB out
	if sys.version_info.major >= 3:
		sys.stdout.buffer.write(xpm_im)
	else:
		sys.stdout.write(xpm_im)
