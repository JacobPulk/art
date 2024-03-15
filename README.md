# What it does

This program generates procedural art images. Ideally, the images will be as diverse as possible without sacrificing aesthetics.

An image will contain one to several similar-but-different, ideally complementary, **paintings**, arranged in a **ptych** (from "triptych" or "polyptych").

Outputs are .bmp files, which can be rendered and re-rendered at any resolution based on associated .json files.

An image is drawn based on, essentially, a single, continuous mathematical function of the XY plane. Ideally, the space of pleasing functions will be covered as widely and evenly as possible.

The image is drawn in only one pass based on that function. There is no "composition" beforehand; the color for each pixel is calculated once; there is no distortion or decoration afterwards (apart from the border/glow around the edges).

This is a meta-program in that these functions are generated by mini-programs called **schemes** and **themes**, which are themselves executed and generated by this program, according to the user's direction.

Hence, you can curate outputs at multiple levels: choose which images to save, which themes to save, and which schemes to save.

<br>
<br>

# How to use it

<br>

## 1. Understand...
- the relationship between **schemes** and **themes**. Images are created by one **scheme** and one **theme** together. Together, they specify a stochastic (random number-influenced) system for creating images. A **scheme** owns its **theme**—a theme is only associated with one particular **scheme**.
- what a **ptych** is: a whole, final product of one to several related paintings, either _rendered_ as an image (a `.bmp` file in the `images` folder), or _unrendered_ as a "blueprint" for an image at any resolution (a `.json` file in the `ptychs` folder). If you delete the `.json` file, you will not be able to re-render the image.
- the file system. In the `data` folder are the `images`, `ptychs`, `themes`, and `schemes` folders. Look at the former two to see the saved/re-renderable images, and the latter two to see the saved/usable **schemes** and **themes**. Feel free to rename these files, as long as you (1) do so after quitting the program and deleting the files in the `cache` folder, and (2) maintain the same obvious naming conventions (**ptychs** and images have corresponding filenames; **schemes** and their **themes** have corresponding filenames).

<br>

## 2. Main commands

<br>

- ### re-render

You can re-render an already-produced image at a specified resolution (representing the longer side of the paintings within the ptych). Use a double-quote mark:

`" 2000` will re-render the last shown image at 2000 pixels.

`" nice 2000` will re-render the saved image called "nice" (leave off the extension) at 2000 pixels.

<br>

- ### explore images

You can run and re-run a scheme+theme combination ad infinitum, producing a new image each time, saving the ones you like.

`butterfly alpha` will generate and show a new image with the scheme called "butterfly" and its theme called "alpha".

` ` (just leave the command blank) will generate a new image with whatever scheme and theme were last used. This will be your most used command.

<br> 

- ### explore themes

You can specify a scheme and (repeatedly) direct the program to find a new theme for it, saving the themes you like. Of course, to test each theme, you will probably want to explore its images (run the scheme+theme combination several times), and may want to save some of those images along the way as well.

`butterfly` will find a new **theme** for the **scheme** called "butterfly".

`?` will find a new **theme** for whatever scheme was last used.

<br>

- ### explore schemes

You can specify nothing, and (repeatedly) direct the program to find a new scheme, saving the schemes you like. Of course, to test each scheme, you will probably want to test at least the first-generated theme several times (explore images), and may want to test several more themes for it(explore themes).

`??` will find a new **scheme** with a new, appropriate **theme**, and generate and show a new image created by them.

<br>

- ### interrupt scheme/theme search

Using default settings, searches for **schemes** and **themes** should produce a result in seconds. That said, if the search is taking too long, press ``ctrl+C`` to interrupt it and enter a new command.

<br>

- ### quit

`#` will quit the program.

<br>

- ### manually composed schemes/themes

There are functions in the `art_scheme.py` file where a user can manually compose a **scheme** and/or **theme**. However, this is difficult, and the program is not finalized enough for the effort to be worth it. Hence, the following types of commands will be of no use and should be avoided:

`++` will generate and show a new image with the manually composed **scheme** and **theme**.

`+?` will find a new theme for the manually composed **scheme**.

`butterfly +` will use the manually composed **theme** for the saved scheme called "butterfly".

<br>

## 3. Save commands

<br>

After generating anything (a re-rendered old image, or a new image/**scheme**/**theme**), you will be prompted to save the new content—first the image...

`image` will save the image with a timestamp-based filename, with the render/resolution just shown.

`image 2000` will save the image with a timestamp-based filename, at 2000 pixels.

`image nice` will save the image with the filename "nice", with the render/resolution just shown.

`image nice 2000` will save the image with the filename "nice", at 2000 pixels.

<br>

..and then the **scheme**, **theme**, or both (depending on what has already been saved).

`scheme moth` will save the scheme with the filename "moth".

`theme alpha` will save the theme with the filename "x_alpha", where "x" is the already-named scheme that was used.

`both moth alpha` will save the scheme with the filename "moth" and the the theme with the filename "moth_alpha".

<br>

On either prompt...

`` ` `` (a backtick, next to the `1` key on a normal keyboard) will skip saving entirely.

`-` (a dash) will skip saving just the currently prompted part (the image, or the **scheme**/**theme**).

<br>
<br>

# How it works

<br>

## Palettes

A palette of several colors is chosen, and arranged in a sequence, both according to some encoded aesthetics about consistencies and inconsistencies of hue, saturation, and value. Each color is assigned a "thickness". The palette should be visualized like a vertical diagram of skin or soil layers. The arrangement is stochastically performed 10 times, to produce 10 replicate palettes of the same colors but different sequences.

<br>

## Rendering

For each pixel, the values of a continuous 6-valued function (see below for how the function is constructed) are calculated based on its X and Y coordinates. The domains and ranges are all [0,1]. The interpretation of these 6 values is as follows.

### palette choice

One value of the function determines which of the 10 palettes is to be used. This is made continuous by calculating (see below) and blending both the colors implied by the "ceiling" palette and "floor" palette resulting from this value.

### toonity

One value of the function determines the smoothness or abruptness of the transitions between colors on the two palettes being used.

### main height

The "main" value of the function is interpreted as a "height" along an imagined vertical palette. Given a palette and a toonity, a height implies a certain color. In general, the pixel will be between two palettes (see palette choice), so the color will be calculated for both palettes and blended in between, according to how far along it is between one and the other.

### hue, saturation, value tweaking

The other 3 values of the function determine the extent to which the hue, saturation, and value are to be shifted upwards or downwards from the main color.

<br>

## Schemes, themes, and functions

<br>

### Functions

A function is an arbitrary composition of about a dozen possible types of component functions (like types of Lego blocks), currently known as `X`, `Y`, `RAND`, `INV`, `POW`, `POWER`, `SIGMOID`, `ARCFAN`, `SIN`, `SPIN`, `MINX`, `AMEAN`, and `GMEAN`. You can guess at their meaning. Most take at least one argument (e.g., the base in `POW`) and have at least one parameter (e.g., the exponent in `POW`). Specifically, a function is represented as a directed acyclic graph (DAG), where each node is an instance of one of those components, and represents an intermediate value in the calculation of the function, its children representing its arguments—values that need to be calculated first.

<br>

### Schemes

#### Kinds

A scheme represents an algorithm for constructing functions. It is a set of **kinds**, which are like a specified (metaphorically, colored or numbered) component function type (e.g. `POW`), specifying how it is to be treated in the function construction process: how many instances are allowed in the function, which **kinds** it can take as arguments, etc. A **scheme** may have no **kinds** of some function types, and may have several **kinds** with the same function type. Maybe a `3-POW` can only accept a `5-SIGMOID` as an argument, while a `4-POW` can accept a `1-X` or a `2-X`. (Of course, it will have at least one `X` **kind** and at least one `Y` **kind**; the functions it generates should depend on both `X` and `Y`.)

#### Constructing functions
When a scheme is used to construct a function, the first node constructed is a root, representing a final calculated value of the function. According to the scheme, the algorithm repeatedly appends child nodes (arguments) to the function (again, a DAG), creating new nodes and grafting existing nodes, until all nodes have all their arguments saturated. 6 root nodes are used, one for each value of the function; the DAGs they root may or may not be connected to one another. To the extend they are connected, the effects of the 6 values will be more coherent in the final image, because their functions depend on shared arguments. Thus, a scheme, applied through this stochastic process, generates the 6-valued function that almost fully determines an image.

<br>

### Themes

A scheme says nothing about parameters for the functions it generates. It needs a theme to assign them. A theme has four parts, two of which modulate the function's parameters.

#### Conceiver

A conceiver is a mapping from **kinds** to **concepts**. A **concept** specifies a distribution of parameters. Thus, a **conceiver** will, stochastically, assign parameters to the components of a function, according to which **kind** they represent. It may be pulling parameters from one distribution for `3-POW`s and from another for `4-POW`s.

#### Correlator

After a conceiver has assigned parameters to the entire function, the **correlator** may rearrange some of those parameters. A correlator specifies a positive or negative correlation between **kinds** of a given relationship within the function. For example, the conceiver may collect a list of `3-POW`s that are first cousins of `4-POW`s, and rearrange their parameters so that the highest `3-POW` parameters tend to be matched with the lowest `4-POW` parameters.

#### Calmer

All 6 final values of the function potentially range from 0 to 1. Apart from the main value, it may not be desirable to allow the others to affect the image so strongly. The **calmer** specifies a distribution from which, for each image, constants are chosen that shrink (or shrink and shift) these values. Images with rainbows tend to result from **calmers** that do not calm the hue much, and allow it to be shifted through a substantial part of the spectrum.

#### Colorcounter

This part of a theme simply specifies a distribution of numbers of colors to use for the palette. This is applied at the beginning of the process, even before the scheme has been invoked. 


