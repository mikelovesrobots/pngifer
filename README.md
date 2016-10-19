# Pngifer

## What is it?

Pngifer is a utility for translating small pngs into ContextFreeArt code to use
in your own digital art. Unfortunately images are limited to a max of 99 pixels 
due to the vector size limit in ContextFreeArt, so this utility is only suitable
for small pixel art.

If that sounds okay to you, you can still make some amazing things.

![Sample render](https://raw.githubusercontent.com/mikelovesrobots/pngifer/master/sample-render.png)

## Installation

* Install ruby (this was built with v2.3.1)
* Clone the repo
* `gem install bundler`
* `bundle install`

## Synopsis

`$ ./pngifer sample-input.png > sample-output.cfdg`

## What does the output look like?

```
image_width   = 8
image_height  = 8
image_hues    = 0.00, 0.00, -8.00, -8.00, -8.00, -8.00, 0.00, 0.00, 0.00, -8.00, 0.00, 0.00, 0.00, 0.00, 0.00, 0.00, -8.00, 0.00, 0.00, -8.00, -8.00, -8.00, -8.00, 0.00, -8.00, 0.00, -8.00, 50.00, 50.00, 50.00, -9.00, -8.00, -8.00, 0.00, -8.00, 50.00, 50.00, -8.00, -9.00, -8.00, -8.00, 0.00, 0.00, -8.00, -8.00, 0.00, -8.00, -8.00, 0.00, -8.00, 0.00, 0.00, 0.00, -8.00, -8.00, 0.00, 0.00, 0.00, -8.00, -8.00, -8.00, -8.00, 0.00, 0.00
image_sats    = 0.00, 0.00, 0.99, 0.99, 0.99, 0.99, 0.00, 0.00, 0.00, 0.99, 0.00, 0.00, 0.00, 0.00, 0.00, 0.00, 0.99, 0.00, 0.00, 0.99, 0.99, 0.99, 0.99, 0.00, 0.99, 0.00, 0.99, 0.99, 0.99, 0.99, 0.97, 0.99, 0.99, 0.00, 0.99, 0.99, 0.99, 0.99, 0.97, 0.99, 0.99, 0.00, 0.00, 0.99, 0.99, 0.00, 0.99, 0.99, 0.00, 0.99, 0.00, 0.00, 0.00, 0.99, 0.99, 0.00, 0.00, 0.00, 0.99, 0.99, 0.99, 0.99, 0.00, 0.00
image_brights = 0.00, 0.00, 0.81, 0.81, 0.81, 0.81, 0.00, 0.00, 0.00, 0.81, 0.00, 0.00, 0.00, 0.00, 0.00, 0.00, 0.81, 0.00, 0.00, 0.81, 0.81, 0.81, 0.81, 0.00, 0.81, 0.00, 0.81, 1.00, 1.00, 1.00, 1.00, 0.81, 0.81, 0.00, 0.81, 1.00, 1.00, 0.81, 1.00, 0.81, 0.81, 0.00, 0.00, 0.81, 0.81, 0.00, 0.81, 0.81, 0.00, 0.81, 0.00, 0.00, 0.00, 0.81, 0.81, 0.00, 0.00, 0.00, 0.81, 0.81, 0.81, 0.81, 0.00, 0.00
image_alphas  = 0.00, 0.00, 1.00, 1.00, 1.00, 1.00, 0.00, 0.00, 0.00, 1.00, 0.00, 0.00, 0.00, 0.00, 0.00, 0.00, 1.00, 0.00, 0.00, 1.00, 1.00, 1.00, 1.00, 0.00, 1.00, 0.00, 1.00, 1.00, 1.00, 1.00, 1.00, 1.00, 1.00, 0.00, 1.00, 1.00, 1.00, 1.00, 1.00, 1.00, 1.00, 0.00, 0.00, 1.00, 1.00, 0.00, 1.00, 1.00, 0.00, 1.00, 0.00, 0.00, 0.00, 1.00, 1.00, 0.00, 0.00, 0.00, 1.00, 1.00, 1.00, 1.00, 0.00, 0.00

CF::Background = [b -0.95]
startshape image[a -1]
shape image {
	loop xx=image_width [] {
		loop yy=image_height [] {
			index = xx + (yy * image_height)
			cell[
				x xx
				y -yy
				h image_hues[index]
				sat image_sats[index]
				b image_brights[index]
				a image_alphas[index]
			]
		}
	}
}

shape cell {
	SQUARE[]
}
```

Replace cell with whatever interesting thing you want to do for the pixel treatment.  
For example, one of my favorites (used in the sample image above) is:

```
shape cell {
	SQUARE[s 0.85..0.9]
	loop 4[s 1.5 a -0.75]
		TRIANGLE[z -1 r 0..360]
}
```

## Licensing

Please see the file called MIT_LICENSE

