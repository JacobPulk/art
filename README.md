# What it does

This command-line program generates procedural art images. See a gallery [here](https://imgur.com/a/Pz2uvam). An image will contain one to several similar-but-different, ideally complementary, "paintings".

The way the program works is abstract and general. The intention in writing it has been to produce the widest diversity of images possible using simple mathematical tools. Using the program, you are bushwacking through a jungle to find areas that are relatively dense with aesthetically pleasing images.

The primary outputs are `.bmp` files, which can be rendered and re-rendered at any resolution based on associated `.json` files.

An image is drawn according to, essentially, a single, more or less continuous function of the XY plane.

The image is drawn in only one pass based on that function. There is no "composition" beforehand. There is only one layer; there are no objects. The color for each pixel is calculated once. Apart from the borders, there is no decoration or adjustment of any kind after the one pass.

**This is a meta-program** in that these functions are generated by mini-programs called **schemes** and **themes**, which are themselves generated, saved, and/or executed by this program, according to the user's direction.

You can guide searches for new **schemes** and **themes** by adjusting settings, and you can curate outputs at multiple levels, choosing which images, **themes**, or **schemes** to save.

In other words, images are composed by procedure and randomness, and are curated by you. Those procedures are composed by procedure and randomness, and are curated by you.

All **schemes**, **themes**, and images generated can probably be assumed, statistically, to have never been generated before, and to never be generated again.

<br>
<br>

# How to use it

<br>

## 1. Download & execute

The program consists of a few Python scripts. I strongly recommend using PyPy to run them, as the other options I have tried appear to be much slower. You have 3 options:

### Use PyPy
If you have already been using PyPy 3.10, just use it as normal for this. Otherwise follow these steps:

1. Download [PyPy 3.10](https://www.pypy.org/download.html) and extract the folder wherever you want.  
2. Download the latest script version of this program (the `...scripts.rar` version under "Assets" [here](https://github.com/JacobPulk/art/releases/latest)) and extract the folder wherever you want.  
3. (Recommended but not necessary) [Add PyPy to your environment PATH.](https://www.activestate.com/resources/quick-reads/how-to-install-and-work-with-pypy/)  
4. Open your command prompt/PowerShell/Terminal in the art program folder ([Windows](https://www.howtogeek.com/662611/9-ways-to-open-powershell-in-windows-10/#from-the-right-click-context-menu), [Mac](https://apple.stackexchange.com/questions/11323/how-can-i-open-a-terminal-window-directly-from-my-current-finder-location)).  
5. If you have added PyPy to your PATH, execute the program with `pypy art.py`.  
Otherwise, execute the program with `& "X\Y\Z\pypy.exe" art.py` (Windows PowerShell) or `"X\Y\Z\pypy.exe" art.py` (otherwise), where `X\Y\Z\pypy.exe` is the full path ([Windows](https://www.howtogeek.com/670447/how-to-copy-the-full-path-of-a-file-on-windows-10/), [Mac](https://www.digitaltrends.com/computing/how-to-find-and-copy-a-file-path-on-mac/)) to `pypy.exe`. 

### OR use the .exe (perhaps 4x slower)

1. Download the latest executable version of this program (the `...executable.rar` version under "Assets" [here](https://github.com/JacobPulk/art/releases/latest)) and extract the folder wherever you want.  
2. Execute the program by double-clicking `art.exe`.

### OR use Python otherwise (perhaps 6x slower)

Run `art.py` however you want.

<br>

## 2. Basic information  

- A **scheme**, **theme**, and image are analogous to a make, model, and car. A **scheme** has its own **themes**—a **theme** is only associated with one particular **scheme**. Together, they specify a stochastic (random number-influenced) system for creating images. In other words, images are created by one **scheme**, one **theme**, and some randomness. They are saved as `.json` files.

- The program comes with many "core" **schemes** and **themes**. You can use these and/or find your own.
  
- A **ptych** (from "triptych" or "polyptych"), also saved as a `.json` file, is a blueprint for an image (containing one to several related paintings). An image can be re-rendered at any resolution from its **ptych**.
  
- In the `data` folder are the `images`, `ptychs`, `themes`, and `schemes` folders. Look at the former two to see the saved/re-renderable images, and the latter two to see the saved/usable **schemes** and **themes**. You can rename these files freely, as long as (1) you do so after quitting the program and deleting the files in the `cache` folder, and (2) you maintain the same obvious naming conventions (**ptychs** and images have corresponding filenames; **schemes** and their **themes** have corresponding filenames).
  
- Using the program simply consists of entering commands as long as you like. You will be alternating a command to generate something with one or two save commands.

<br>

## 3. Main (generating) commands

<br>

- ### re-render images

You can re-render an already-produced image at a specified resolution (representing the longer side of the paintings within the ptych). Use a double-quote mark:

`" 2000` will re-render the last shown image at 2000 pixels.

`" nice 2000` will re-render the saved image called "nice" (leave off the extension) at 2000 pixels.

<br>

- ### discover images

You can run and re-run a **scheme**+**theme** combination ad infinitum, producing a new image each time, saving the ones you like.

`butterfly alpha` will generate and show a new image with the **scheme** called "butterfly" and its **theme** called "alpha".

`!` will generate a new image from a random saved **scheme** and **theme**.

` ` (just leave the command blank) will generate a new image with whatever scheme and theme were last used.

<br> 

- ### discover themes

You can specify a **scheme** and (repeatedly) direct the program to find a new theme for it, saving the **themes** you like. Of course, to test each **theme**, you will probably want to explore its images (run the **scheme**+**theme** combination several times), and may want to save some of those images along the way as well.

`butterfly` will find a new **theme** for the **scheme** called "butterfly".

`?` will find a new **theme** for whatever **scheme** was last used.

<br>

- ### discover schemes

You can specify nothing, and (repeatedly) direct the program to find a new **scheme**, saving the **schemes** you like. Of course, to test each **scheme**, you will probably want to test at least the first-generated **theme** several times (explore images), and may want to test several more **themes** for it.

`??` will find a new **scheme** with a new, appropriate **theme**, and generate and show a new image created by them.

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

## 3.5. Interrupt scheme/theme search

Using default settings, searches for **schemes** and **themes** should produce a result in seconds. Regardless, if the search is taking too long, press ``ctrl+C`` to interrupt it and enter a new command.

<br>

## 4. Save commands

<br>

After generating anything, you will be prompted to save the new content—first the image...

`image` will save the image with a timestamp-based filename, with the render/resolution just shown.

`image 2000` will save the image with a timestamp-based filename, at 2000 pixels.

`image nice` will save the image with the filename "nice", with the render/resolution just shown.

`image nice 2000` will save the image with the filename "nice", at 2000 pixels.

<br>

..and then the **scheme**, **theme**, or both (depending on what has already been saved—you will be told which option(s) are available).

`scheme moth` will save the **scheme** with the filename "moth".

`theme alpha` will save the **theme** with the filename "x_alpha", where "x" is the already-named **scheme** that was used.

`both moth alpha` will save the **scheme** with the filename "moth" and the **theme** with the filename "moth_alpha".

<br>

On either prompt...

`` ` `` (a backtick, next to the `1` key on a normal keyboard) will skip saving entirely.

`-` (a dash) will skip saving just the currently prompted part (the image, or the **scheme**/**theme**).

<br>

## 5. Settings

Change settings in the `settings.txt` file. The setting name and value are separated by tabs; you can add or remove tabs freely.

`DEFAULT RESOLUTION` is self-explanatory.

`SEARCH SLOWING` (in seconds per megapixel) and `RENDER SLOWING` (in milliseconds per **theme**) slow the program to avoid CPU heating.

<br>

The other settings represent your requirements for new **themes** (and, indirectly, for new **schemes** - for which the program must be able to find an acceptable **theme**). As the program searches through new (randomly generated) **themes**, for each one these measures will be estimated. The search ends and a **theme** is presented when one is found that meets your requirements. The more restrictive the requirements are, the longer the search will take; a search may never end (but any requirements at all similar to the default settings should yield results quickly).

<br>

"Complexity" is a _very rough_ estimate of the visual complexity resulting images. Low complexity **themes** may be less interesting; high complexity **themes** may be less pretty. **Themes** with median complexity above about 13 are hard to find.

`LOW COMPLEXITY MIN` is the lowest complexity you will accept for an image at the 5th percentile (i.e., for the top of the simplest 5% of images produced by the theme).

`MEDIAN COMPLEXITY MIN` is the lowest complexity you will accept for a median image (i.e., half the images may be that simple or simpler).

`MEDIAN COMPLEXITY MAX` is the highest complexity you will accept for a median image (i.e., half the images may be that complex or more complex).

`HIGH COMPLEXITY MAX` is the highest complexity you will accept the an image at the 95th percentile (i.e., for the bottom of the most complex 5% of images produced by the theme).

<br>

"Speed" is an estimate of the speed of rendering the resulting images. A higher speed is better.

`LOW SPEED MIN` is the lowest speed you will accept for an image at the 5th percentile (i.e., for the top of the slowest 5% of images produced by the theme).

`MEDIAN SPEED MIN` is the lowest speed you will accept for a median image (i.e., half the images may be that slow or slower).

<br>

You can also experiment with the additional settings found in the `default_settings()` function of `art.py`. However, these are less likely to improve your experience and not worth explaining here.

<br>
<br>

# How it works (short version)

<br>

Basically, an image is defined by a palette and 7 mathematical functions. The palette is generated more or less independently from the functions.

The functions are single-valued, more or less continuous functions of the XY plane. The image is drawn in one pass, by applying the functions and palette to each pixel's coordinates to arrive at a color for it.

At each pixel, one function value determines the number of iterations the rest of the functions will undergo. Two function values tweak the palette. One function value determines a location on the palette. Applied to the tweaked palette, this results in a color. The other three function values directly tweak that color's hue, saturation and brightness.

These functions are generated by
1. applying a **scheme**, which is an algorithm for generating functions composed of dozens or hundreds of building block minifunctions (like `X`, `Y`, `POW`, and `SIN`), then
2. applying a **theme**, which specifies a distribution of parameters to be assigned to those minifunctions (like the exponent in `POW`), as well as a few miscellaneous parameters for the palette construction and color calculation.

Importantly, those 7 functions are not generated independently. They share steps in their calculations, so there will be some harmony in the way their values vary across the image.

<br>

# How it works (long version)

<br>

## Code

Written in Python, only importing from the standard library. [Nuitka](https://pypi.org/project/Nuitka/) is used to compile the .exe version.

<br>

## Palettes

A palette of several colors is chosen, and arranged in a sequence, both according to some encoded aesthetics about consistencies and inconsistencies of hue, saturation, and brightness. The palette is sorted, and each color is assigned a "thickness", both partially randomly and partially in accordance with the colors' relative attributes. The resulting palette should be visualized like a vertical diagram of skin or soil layers. The arrangement is stochastically performed 10 times, to produce 10 replicate palettes of the same colors but different sequences. Palettes are essentially independent from **schemes** and **themes**.

<br>

## Rendering

For each pixel, 7 almost-everywhere continuous functions (see below for how the functions are constructed) are calculated, according to two arguments: its X and Y coordinates. The domains and ranges are all [0,1]. The interpretation of these 7 functions is as follows.

### iteration

One value of the function determines the number of iterations the other 6 functions will undergo. This is made continuous by calculating all following values with the "floor" number of iterations and the "ceiling" number, and interpolating between.

### palette choice

One value of the function determines, loosely speaking, which one of the 10 palettes is to be used. This is made continuous—non-integer palettes are handled—by completing the calculations for both the "floor" palette and the "ceiling" palette, and interpolating between. So, this value really determines two palettes and a distance between them, which will be synthesized to choose a color.

### "toonity"

One value of the function determines the smoothness or abruptness of the transitions between colors on the palettes being used.

### main height

The "main" value of the function is interpreted as a "height" on the palette (again, imagined as a vertical sequence of layers). Given a palette and a "toonity", a height implies a certain color. In general, the pixel will be between two palettes (see palette choice), so the color will be calculated for both palettes and blended in between, according to how far along it is between one and the other.

### hue, saturation, brightness adjustment

The other 3 values of the function determine the extent to which the hue, saturation, and brightness are to be shifted upwards or downwards from the main color.

<br>

## Schemes, themes, and functions

<br>

### Functions

A function is an arbitrary composition of about a dozen possible types of component mini-functions (like types of Lego blocks), currently known as `X`, `Y`, `RAND`, `INV`, `POW`, `POWER`, `SIGMOID`, `ARCFAN`, `SIN`, `SPIN`, `MINX`, `AMEAN`, and `GMEAN`. You can guess at their meaning. Most take at least one argument (e.g., the base in `POW`) and have at least one parameter (e.g., the exponent in `POW`). The component functions and calculating method are constructed to maintain a range of [0,1] on the domain [0,1] at (basically) every step. The whole function is treated as a [directed acyclic graph (DAG)](https://en.wikipedia.org/wiki/Directed_acyclic_graph), where each node is an instance of one of those components, and represents an intermediate or final value in the calculation of the function. The node's children represent its arguments—values that need to be calculated first.

The "7 functions" that define an image are really just one function, with 7 nodes indicated as the final values.

In the code, to avoid confusion from long words with multiple meanings like "function" and "parametrize", a function is called a **rope** and the instances of component mini-functions making it up are called **cords**. The list indicating which cords represent each of the 6 final values is called the **fray**.

<br>

### Schemes

#### Kinds

A **scheme** represents an algorithm for constructing functions. It is a set of **kinds**, which are like a specified (metaphorically, colored or numbered) component function type (e.g. `POW`), specifying how it is to be treated in the function construction process: how many instances are allowed in the function, which **kinds** it can take as arguments, etc. A **scheme** may have no **kinds** of some function types, and may have several **kinds** with the same function type. Maybe a `3-POW` can only accept a `5-SIGMOID` as an argument, while a `4-POW` can accept a `1-X` or a `2-X`. (Of course, any worthwhile **scheme** will have at least one `X` **kind** and at least one `Y` **kind**; the functions it generates should depend on both `X` and `Y`.)

#### Constructing functions
When a **scheme** is used to construct a function, the order of construction is more or less backwards with respect to the order of calculation. The first node constructed is a root, representing a final calculated value of the function. According to the scheme, the algorithm repeatedly appends child nodes (arguments) to the function (again, a DAG), creating new nodes and grafting existing nodes, until all nodes have all their arguments saturated. 6 root nodes are used, one for each value of the function; the DAGs they root may or may not be connected to one another. To the extend they are connected, the effects of the 7 values will be more coherent in the final image, because their functions depend on shared arguments (nodes). Thus, a **scheme**, applied through this stochastic process, generates the 6-valued function that almost fully determines an image.

<br>

### Themes

A **scheme** says nothing about parameters for the functions it generates. It needs a **theme** to assign them. A **theme** has five parts. The first two determine the parameters inside the function.

#### Conceiver

A **conceiver** is a mapping from **kinds** to **concepts**. A **concept** specifies a distribution of parameters. Thus, a **conceiver** will, stochastically, assign parameters to the components of a function, according to which **kind** they represent. It may be pulling parameters from one distribution for `3-POW`s and from another for `4-POW`s.

#### Correlator

After a **conceiver** has assigned parameters to the entire function, the **correlator** may rearrange some of those parameters. The **correlator** specifies a positive or negative correlation between **kinds** of a given relationship within the function. For example, the **correlator** may collect a list of `3-POW`s that are first cousins of `4-POW`s, and rearrange their parameters so that the highest `3-POW` parameters tend to be matched with the lowest `4-POW` parameters.

#### Calmer

All 6 final values of the function potentially range from 0 to 1. Apart from the main value, it may not be desirable to allow the others to affect the image so strongly. The **calmer** specifies a distribution from which, for each image, constants are chosen that shrink (or shrink and shift) these 5 values. Images with rainbows tend to result from **calmers** that do not calm the hue much, and allow it to be shifted through a substantial part of the spectrum.

#### Colorcounter

This part of a theme simply specifies a distribution of numbers of colors to use for the palette. This is applied at the beginning of the process, essential to creating the palette in the first place, even before the **scheme** has been considered. 

#### Complicator

This specifies two distributions, which are sampled to choose the minimum and maximum number of iterations the image's functions will be put through.

<br>

### Theme search

Generating random **themes** is mostly straightforward. An important part of the code, part of generating a random **conceiver**, is the set of functions for generating random **concepts** for each of the types of component functions. These define a _distribution of distributions_ of parameters, that will hopefully result in a more or less even distribution of visually different results down the line. Some "special" options for parameters are given extra weight. For example, for the exponent in `POW`, 0, 1/2, and 2 might be "visually meaningful" values, 0 not affecting the result at all, and 1/2 and 2 being essential for a perfect circle.  

The search ends when a randomly generated **theme** meets the requirements indicated in the settings. At the beginning of a **theme** search, the relevant **scheme** is applied many times to generate a sample of many "ropes" (functions). The **theme** is applied to all of them, the complexity and speed are estimated for all of them, and the results are checked against the set requirements.

<br>

### Scheme search

Generating random **schemes** is not as straightforward as one would hope, because a **scheme** should guarantee that the functions it produces depend on both `X` and `Y` components. It does not simply have to include `X` and `Y` kinds; it also has to guarantee that at least one of each will be reached every time. So, X **kinds**, Y **kinds**, guaranteed X-dependent **kinds**, guaranteed Y-dependent **kinds**, X- & Y-combining **kinds**, guaranteed X- & Y-depedent **kinds**, and unrestricted **kinds** are all generated separately to maintain their separate requirements; the **kinds** that can be used for the final 6 values must all be guaranteed X- & Y-dependent.

A **scheme** search is really just a series of **theme** searches. A random **scheme** is generated; some number of random **themes** are tried for it; if one meets the **theme** requirements, that **scheme** and **theme** are returned, otherwise the next random **scheme** is tried, and so on.

<br>

## Ptych coordination

Paintings in a **ptych** are similar but different. This is _not_ accomplished by generating one painting and tweaking it several times. Even if such a method was implemented carefully enough that modified paintings were indistinguishable from "properly" generated ones, it would still violate the spirit of the program by depending on post-processing. Instead, all paintings in a **ptych** are generated by the exact same process, with the random number generator (Python `random` module) seeded differently for (randomly) selected, brief intervals within the generating methods. At initialization, all paintings are assigned the same (random) sequence of seeds for their reseed points, after which each painting has new seed values assigned to a small random subset of its reseed points. Reseed points are carefully arranged in the code so they are each reached exactly once during the creation of a painting. This is necessary for the numbers generated at the *n*th point in one painting to be being used for the same purpose as the numbers generated at the *n*th point in another painting.

Borders are subject to this same reseeding, but their variation is sometimes overriden shortly afterwards—on select paintings, they are replaced with replicates of select earlier-generated borders, so that the "odd" half of alternating paintings, and paintings mirroring each other in the **ptych** sequence, are assigned identical borders.

<br>
<br>

# How it does not work

<br>

While randomness influences the palette and function, there is no randomness applied once rendering starts; the image is a deterministic given those "inputs". Even applying the `RAND` component function is deterministic in that the values are always generated by the same seed to the `random` module (arbitrarily, 0)—it is one unchanging function that looks random.  

A **theme's** complexity and speed are not estimated by test-drawing (they are estimated by analytic means on a sample of test functions).

There is no "composition" beforehand; there is only one layer—the color for each pixel is calculated once; there is no distortion or decoration afterwards (apart from the border/glow around the edges).

There is no drawing upon preset colors, palettes, images, compositions, or archetypes thereof, in the code. (Of course, whatever **scheme** and **theme** you're using will narrow the range of possibilities—that's the point.)

There is no directly encoded or guaranteed "symmetry" or "asymmetry"; they both occur naturally from combining random functions.

There is no neural network, training data, or training or learning of any kind. It is not AI.
