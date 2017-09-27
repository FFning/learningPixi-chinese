# 学习Pixi
---

> 原文链接：[https://github.com/kittykatattack/learningPixi](https://github.com/kittykatattack/learningPixi)

一步一步的介绍使用[Pixi渲染引擎](https://github.com/pixijs/pixi.js)制作游戏及交互式多媒体。 **[更新至Pixi v4.0.0](https://github.com/pixijs/pixi.js/releases/tag/v4.0.0)**。如果你喜欢这份教程，[你也会喜欢这本书，它比本教程多了80%的内容！](http://www.springer.com/us/book/9781484210956)

### **目录**:
1. [介绍](#introduction)
2. [安装](#settingup)
    1. [安装Pixi的简单方法](#installingpixithesimpleway)
    2. [使用Git安装Pixi](#installingpixiwithgit)
    3. [使用Node和Gulp安装Pixi](#installingpixiwithnodeandgulp)
3. [创建舞台(Stage)和渲染器(Renderer)](#renderer)
4. [Pixi精灵(Sprites)](#sprites)
5. [将图片载入纹理缓存(Texture Cache)](#loading)
6. [显示精灵(Sprites)](#displaying)
    1. [使用别名](#usingaliases)
    2. [进一步了解加载](#alittlemoreaboutloadingthings)
        1. [从普通的JavaScript图片对象或Canvas创建精灵](#makeaspritefromanordinaryjavascriptimageobject)
        2. [为已加载的文件命名](#assigninganametoaloadingfile)
        3. [监控加载进度](#monitoringloadprogress)
        4. [更多关于Pixi的加载器](#moreaboutpixisloader)
7. [放置精灵(Sprites)](#positioning)
8. [尺寸与缩放](#sizenscale)
9. [旋转](#rotation)

<a id='introduction'></a>
## **介绍**
Pixi’s is an extremely fast 2D sprite rendering engine. What does that
mean? It means that it helps you to display, animate and manage
interactive graphics so that it's easy for you to make games and
applications using
JavaScript and other HTML5 technologies. It has a sensible,
uncluttered API and includes many useful features, like supporting
texture atlases and providing a streamlined system for animating
sprites (interactive images). It also gives you a complete scene graph so that you can
create hierarchies of nested sprites (sprites inside sprites), as well
as letting you attach mouse and touch events directly to sprites. And,
most
importantly, Pixi gets out of your way so that you can use as much or
as little of it as you want to, adapt it to your personal coding
style, and integrate it seamlessly with other useful frameworks.

Pixi’s API is actually a refinement of a well-worn and battle-tested
API pioneered by Macromedia/Adobe Flash. Old-skool Flash developers
will feel right at home. Other current sprite rendering frameworks use
a similar API: CreateJS, Starling, Sparrow and Apple’s SpriteKit. The
strength of Pixi’s API is that it’s general-purpose: it’s not a game
engine. That’s good because it gives you total expressive freedom to make anything you like, and wrap your own custom game engine around it.

In this tutorial you’re going to find out how to combine Pixi’s
powerful image rendering features and scene graph to start making
games. You’re also going to learn how to prepare your game graphics
with a texture atlas, how to make particle effects using the Proton
particle engine, and how to integrate Pixi into your own custom game
engine. But Pixi isn't just for games - you can use these same
techniques to create any interactive media applications. That means
apps for phones!

What do you need to know before you get started with this tutorial?

You should have a reasonable understanding of HTML and
JavaScript. You don't have to be an expert, just an ambitious beginner
with an eagerness to learn. If you don't know HTML and JavaScript, the
best place to start learning it is this book:

[Foundation Game Design with HTML5 and JavaScript](http://www.apress.com/9781430247166)

I know for a fact that it's the best book, because I wrote it!

There are also some good internet resources to help get you started:

[Khan Academy: Computer
Programming](http://www.khanacademy.org/computing/cs)

[Code Academy:
JavaScript](http://www.codecademy.com/tracks/javascript)

Choose whichever best suits your learning style.

Ok, got it?
Do you know what JavaScript variables, functions, arrays and objects are and how to
use them? Do you know what [JSON data
files](http://www.copterlabs.com/blog/json-what-it-is-how-it-works-how-to-use-it/)
are? Have you used the [Canvas Drawing API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_graphics_with_canvas)?

To use Pixi, you'll also need to run a webserver in your root project
directory. Do you know what a webserver is and
how to launch one in your project folder? The best way is to use
[node.js](http://nodejs.org) and then to install the extremely easy to use
[http-server](https://github.com/nodeapps/http-server). However, you need to be comfortable working with the Unix
command line if you want to do that. You can learn how to use
Unix [in this
video](https://www.youtube.com/watch?feature=player_embedded&v=cX9ASUE3YAQ)
and, when you're finished, follow it with [this
video](https://www.youtube.com/watch?v=INk0ATBbclc). You should learn
how to use Unix - it only takes a couple of hours to learn and is a
really fun and easy way to interact with your computer.

But if you don't want to mess around with the command line just yet, try the Mongoose
webserver:

[Mongoose](http://cesanta.com/mongoose.shtml)

Or, just write your all your code using the excellent [Brackets text
editor](http://brackets.io). Brackets automatically launches a webserver
and browser for you when you click the lightening bolt button in its
main workspace.

Now if you think you're ready, read on!

(Request to readers: this is a *living document*. If you have any
questions about specific details or need any of the content clarified, please
create an **issue** in this GitHub repository and I'll update the text
with more information.)

<a id='settingup'></a>
## **安装**
Before you start writing any code, create a folder for your project, and launch a
webserver in the project's root directory. If you aren't running a
webserver, Pixi won't work.

Next, you need to install Pixi. There are two ways to do it: the
**simple** way, with **Git** or with **Gulp and Node**. 

<a id='installingpixithesimpleway'></a>
### 安装Pixi的简单方法

The version used for this introduction is **v4.0.0**
and you can find `pixi.min.js` file on [Pixi's release page for v4.0.0](https://github.com/pixijs/pixi.js/releases/tag/v4.0.0).
Or you can get the latest version from [Pixi's main release page](https://github.com/pixijs/pixi.js/releases).

This one file is all you need to use Pixi. You can ignore all the
other files in the repository: **you don't need them.**

Next, create a basic HTML page, and use a
`<script>` tag to link the
`pixi.min.js` file that you've just downloaded. The `<script>` tag's `src`
should be relative to your root directory where your webserver is
running. Your `<script>` tag might look something like this:
```html
<script src="pixi.min.js"></script>
```
Here's a basic HTML page that you could use to link Pixi and test that
it's working:
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
  <script src="pixi.min.js"></script>
<body>
  <script type="text/javascript">
    var type = "WebGL"
    if(!PIXI.utils.isWebGLSupported()){
      type = "canvas"
    }

    PIXI.utils.sayHello(type)
  </script>
</body>
</html>
```

If Pixi is linking correctly,
something like this will be displayed in your web browser's JavaScript console by default:
```
 Pixi.js 4.0.0 - ✰ WebGL ✰      http://www.pixijs.com/    ♥♥♥ 
```

Now you can start working with Pixi!

<a id='installingpixiwithgit'></a>
### 使用Git安装Pixi

You can also use Git to install use Pixi. (What is **git**? If you don't know [you can find out
here](https://github.com/kittykatattack/learningGit).) This has some advantages:
you can just run `git pull origin master` from the command line to update Pixi to
the latest version. And, if you think you've found a bug in Pixi, 
you can fix it and submit a pull request to have the bug fix added to the main repository.

To clone the Pixi repository with Git,  `cd`
into your root project directory and type:
```
git clone git@github.com:pixijs/pixi.js.git
```
This automatically creates a folder called `pixi.js` and loads the **latest version** of Pixi into it.
Keep in mind that this manual is tailored around *version 4.0.0*.
To get this version simply checkout cloned `pixi.js` repository using tag like this:
```
git checkout tags/v4.0.0
```

After Pixi is installed, create a basic HTML document, and use a
`<script>` tag to include the
`pixi.js` file from Pixi's `bin` folder. The `<script>` tag's `src`
should be relative to your root directory where your webserver is
running. Your `<script>` tag might look something like this:
```html
<script src="pixi.js/bin/pixi.js"></script>
```
(If you prefer, you could link to the `pixi.min.js` file instead as I
suggested in the previous section. The
minified file might actually run slightly faster, and it will
certainly load faster. The advantage to using the
un-minified plain JS file is that if the compiler thinks there's a bug in Pixi's
source code, it will give you an error message that displays the questionable code
in a readable format. This is useful while you're working on a
project, because even if the bug isn't in Pixi, the error might give
you a hint as to what's wrong with your own code.)

In this **Learning Pixi** repository (what you're reading now!) you'll find a folder called
`examples`. Open it and you'll find a file called `helloWorld.html`.
Assuming that the webserver is running in this repository's root directory, this is
how the `helloWorld.html` file correctly links to Pixi and checks that it's
working:
```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World</title>
</head>
<body>
  <script src="../pixi.js/bin/pixi.js"></script>
</body>
</html>
```
If Pixi is linking correctly, something like this will be displayed in your web browser's JavaScript console by default:
```
 Pixi.js 4.0.0 - ✰ WebGL ✰      http://www.pixijs.com/    ♥♥♥ 
```

<a id='installingpixiwithnodeandgulp'></a>
### 使用Node和Gulp安装Pixi

You can also install Pixi using [Node](https://nodejs.org) and [Gulp](http://gulpjs.com). If you need
to do a custom build of Pixi to include or exclude certain features,
this is the route you should take. [See Pixi's GitHub repository for
details on how](https://github.com/GoodBoyDigital/pixi.js). But, in general
there's no need to do this.

<a id='renderer'></a>
## **创建舞台(Stage)和渲染器(Renderer)**

Now you can start using Pixi!

But how? 

The first step is to create a rectangular
display area that you can start displaying images on. Pixi has a
`renderer` object that creates this for you. It
automatically generates an HTML `<canvas>` element and figures out how
to display your images on the canvas. You then need to create a
special Pixi `Container` object called the `stage`. As you'll see
ahead, this stage object is going to be used as the root container
that holds all the things you want Pixi to display. 

Here’s the code you need to write to create a `renderer`
and `stage`. Add this code to your HTML document between the `<script>` tags:
```js
//Create the renderer
var renderer = PIXI.autoDetectRenderer(256, 256);

//Add the canvas to the HTML document
document.body.appendChild(renderer.view);

//Create a container object called the `stage`
var stage = new PIXI.Container();

//Tell the `renderer` to `render` the `stage`
renderer.render(stage);
```
This is the most basic code you need write to get started using Pixi. 
It produces a black 256 pixel by 256 pixel canvas element and adds it to your
HTML document. Here's what this looks like in a browser when you run this code.

![Basic display](/examples/images/screenshots/01.png)

Yay, a [black square](http://rampantgames.com/blog/?p=7745)!

Pixi’s `autoDetectRenderer` method figures out whether to use the
Canvas Drawing API or WebGL to render graphics, depending on which is
available. Its first and second arguments are the width and height of the
canvas. However, you can include an optional third argument with some
additional values you can set. This third argument is an object
literal, and here's how you could use it to set anti-aliasing, transparency
and resolution:
```js
renderer = PIXI.autoDetectRenderer(
  256, 256,
  {antialias: false, transparent: false, resolution: 1}
);
```
This third argument (the options object) is optional - if you're happy with Pixi's default
settings you can leave it out, and there's usually no need to change
them. (But, if you need to, see Pixi's documentation on the [Canvas
Renderer](http://pixijs.download/release/docs/PIXI.CanvasRenderer.html)
and
[WebGLRenderer](http://pixijs.download/release/docs/PIXI.WebGLRenderer.html)
for more information.)

What do those options do?
```js
{antialias: false, transparent: false, resolution: 1}
```
`antialias` smoothes the edges of fonts and graphic primitives. (WebGL
anti-aliasing isn’t available on all platforms, so you’ll need to test
this on your game’s target platform.) `transparent` makes the canvas
background transparent. `resolution` makes it easier to work with
displays of varying resolutions and pixel densities. Setting
the resolutions is a little
outside the scope of this tutorial, but check out [Mat Grove's
explanation](http://www.goodboydigital.com/pixi-js-v2-fastest-2d-webgl-renderer/)
about how to use `resolution` for all the details. But usually, just keep `resolution`
at 1 for most projects and you'll be fine. 

(Note: The renderer has an additional, fourth, option called `preserveDrawingBuffer` that
defaults to `false`. The only reason to it set it
to `true` is if you ever need to call Pixi's specialized `dataToURL`
method on a WebGL canvas context.)

Pixi's renderer object will default to WebGL, which is good, because WebGL is
incredibly fast, and lets you use some spectacular visual effects that
you’ll learn all about ahead. But if you need to force Canvas Drawing
API rendering over WebGL, you can do it like this:
```js
renderer = new PIXI.CanvasRenderer(256, 256);
```
Only the first two arguments are required: `width` and `height`.

You can force WebGL rendering like this:
```js
renderer = new PIXI.WebGLRenderer(256, 256);
```
The `renderer.view` object is just a plain old ordinary `<canvas>`
object, so you can control it the same way you would control any other
canvas object. Here's how to give the canvas an optional dashed
border:
```js
renderer.view.style.border = "1px dashed black";
```
If you need to change the background color of the canvas after you’ve
created it, set the `renderer` object’s `backgroundColor` property to
any hexadecimal color value:
```js
renderer.backgroundColor = 0x061639;
```
If you want to find the width or the height of the `renderer`, use
`renderer.view.width` and `renderer.view.height`.

(Importantly: although the `stage` also has `width` and `height` properties, *they don't refer to
the size of the rendering window*. The stage's `width` and `height`
just tell you the area occupied by the things you put inside it - more
on that ahead!)

To change the size of the canvas, use the `renderer`’s `resize`
method, and supply any new `width` and `height` values. But, to make
sure the canvas is resized to match the resolution, set `autoResize`
to `true`.
```js
renderer.autoResize = true;
renderer.resize(512, 512);
```
If you want to make the canvas fill the entire window, you can apply this
CSS styling and resize the renderer to the size of the browser window.
```
renderer.view.style.position = "absolute";
renderer.view.style.display = "block";
renderer.autoResize = true;
renderer.resize(window.innerWidth, window.innerHeight);
```
But, if you do that, make sure you also set the default padding and
margins to 0 on all your HTML elements with this bit of CSS code:
```html
<style>* {padding: 0; margin: 0}</style>
```
(The asterisk, *, in the code above, is the CSS "universal selector",
which just means "all the tags in the HTML document".)

If you want the canvas to scale proportionally to any browser window
size, you can use [this custom scaleToWindow function.](https://github.com/kittykatattack/scaleToWindow).

<a id='sprites'></a>
## **Pixi精灵(Sprites)**
In the previous section you learned how to create a `stage` object,
like this:
```js
var stage = new PIXI.Container();
```
The `stage` is a Pixi `Container` object. You can think of a container
as a kind of empty box that will group together and store whatever you
put inside it.
The `stage` object that we created is the root container for all the visible
things in your scene. Pixi requires that you have one root container
object, because the `renderer` needs something to render:
```js
renderer.render(stage);
```
Whatever you put inside the `stage` will be
rendered on the canvas. Right now the `stage` is empty, but soon we're going to
start putting things inside it.

(Note: You can give your root container any name you like. Call it
`scene` or `root` if you prefer. The name
`stage` is just an old but useful convention, and one we'll be
sticking to in this tutorial.)

So what do you put on the stage? Special image objects called
**sprites**. Sprites are basically just images that you can control
with code. You can control their position, size, and a host of other
properties that are useful for making interactive and animated graphics. Learning to make and control sprites is really the most
important thing about learning to use Pixi. If you know how to make
sprites and add them to the stage, you're just a small step away from
starting to make games.

Pixi has a `Sprite` class that is a versatile way to make game
sprites. There are three main ways to create them:

- From a single image file.
- From a sub-image on a **tileset**. A tileset is a single, big image that
includes all the images you'll need in your game.
- From a **texture atlas** (A JSON file that defines the size and position of an image on a tileset.)

You’re going to learn all three ways, but, before you do, let’s find
out what you need to know about images before you can display them
with Pixi.

<a id='loading'></a>
## **将图片载入纹理缓存(Texture Cache)**

Because Pixi renders the image on the GPU with WebGL, the image needs
to be in a format that the GPU can process. A WebGL-ready image is
called a **texture**. Before you can make a sprite display an image,
you need to convert an ordinary image file into a WebGL texture. To
keep everything working fast and efficiently under the hood, Pixi uses
a **texture cache** to store and reference all the textures your
sprites will need. The names of the textures are strings that match
the file locations of the images they refer to. That means if you have
a texture that was loaded from `"images/cat.png"`, you could find it in the texture cache like this:
```js
PIXI.utils.TextureCache["images/cat.png"];
```
The textures are stored in a WebGL compatible format that’s efficient
for Pixi’s renderer to work with. You can then use Pixi’s `Sprite` class to make a new sprite using the texture.
```js
var texture = PIXI.utils.TextureCache["images/anySpriteImage.png"];
var sprite = new PIXI.Sprite(texture);
```
But how do you load the image file and convert it into a texture? Use
Pixi’s built-in `loader` object. 

Pixi's powerful `loader` object is all you need to load any kind of image. 
Here’s how to use it to load an image and call a function called `setup` when the 
image has finished loading:
```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  //This code will run when the loader has finished loading the image
}
```
[Pixi’s development team
recommends](http://www.html5gamedevs.com/topic/16019-preload-all-textures/?p=90907)
that if you use the loader, you should create the sprite by
referencing the texture in the `loader`’s `resources` object, like this:
```js
var sprite = new PIXI.Sprite(
  PIXI.loader.resources["images/anyImage.png"].texture
);
```
Here’s an example of some complete code you could write to load an image, 
call the `setup` function, and create a sprite from the loaded image:
```js
PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  var sprite = new PIXI.Sprite(
    PIXI.loader.resources["images/anyImage.png"].texture
  );
}
```
This is the general format we’ll be using to load images and create
sprites in this tutorial.

You can load multiple images at the same time by listing them with
chainable `add` methods, like this:
```js
PIXI.loader
  .add("images/imageOne.png")
  .add("images/imageTwo.png")
  .add("images/imageThree.png")
  .load(setup);
```
Better yet, just list all the files you want to load in
an array inside a single `add` method, like this:
```js
PIXI.loader
  .add([
    "images/imageOne.png",
    "images/imageTwo.png",
    "images/imageThree.png"
  ])
  .load(setup);
```
The `loader` also lets you load JSON files, which you'll learn
about ahead.

<a id='displaying'></a>
## **显示精灵(Sprites)**

After you've loaded an image, and used it to make a sprite, there
are two more things you have to do before you can actually see it on
the canvas:

-1. You need to add the sprite to Pixi's `stage` with the `stage.addChild` method, like this:
```js
stage.addChild(cat);
```
The stage is the main container that holds all of your sprites.

-2. You need to tell Pixi's `renderer` to render the stage.
```js
renderer.render(stage);
```
**None of your sprites will be visible before you do these two
things**.

Before we continue, let's look at a practical example of how to use what
you've just learnt to display a single image. In the `examples/images`
folder you'll find a 64 by 64 pixel PNG image of a cat.

![Basic display](/examples/images/cat.png)

Here's all the JavaScript code you need to load the image, create a
sprite, and display it on Pixi's stage:
```js
var stage = new PIXI.Container(),
    renderer = PIXI.autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//Use Pixi's built-in `loader` object to load an image
PIXI.loader
  .add("images/cat.png")
  .load(setup);

//This `setup` function will run when the image has loaded
function setup() {

  //Create the `cat` sprite from the texture
  var cat = new PIXI.Sprite(
    PIXI.loader.resources["images/cat.png"].texture
  );

  //Add the cat to the stage
  stage.addChild(cat);
  
  //Render the stage   
  renderer.render(stage);
}
```
When this code runs, here's what you'll see:

![Cat on the stage](/examples/images/screenshots/02.png)

Now we're getting somewhere!

If you ever need to remove a sprite from the stage, use the `removeChild` method:
```js
stage.removeChild(anySprite)
```
But usually setting a sprite’s `visible` property to `false` will be a simpler and more efficient way of making sprites disappear.
```js
anySprite.visible = false;
```
<a id='usingaliases'></a>
### 使用别名

You can save yourself a little typing and make your code more readable
by creating short-form aliases for the Pixi objects and methods that you
use frequently. For example, is `PIXI.utils.TextureCache` too much to
type? I think so, especially in a big project where you might use it
it dozens of times. So, create a shorter alias that points to it, like
this:
```js
var TextureCache = PIXI.utils.TextureCache
```
Then, use that alias in place of the original, like this:
```js
var texture = TextureCache["images/cat.png"];
```
In addition to letting you write more succinct code, using aliases has
an extra benefit: it helps to buffer you slightly from Pixi's frequently
changing API. If Pixi's API changes in future
versions - which it will! - you just need to update these aliases to
Pixi object and methods in one place, at the beginning of
your program, instead of every instance where they're used throughout
your code. So when Pixi's development team decides they want to
rearrange the furniture a bit, you'll be one step ahead of them!

To see how to do this, let's re-write the code we wrote to load an image and display it,
using aliases for all the Pixi objects and methods.
```js
//Aliases
var Container = PIXI.Container,
    autoDetectRenderer = PIXI.autoDetectRenderer,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Create a Pixi stage and renderer and add the 
//renderer.view to the DOM
var stage = new Container(),
    renderer = autoDetectRenderer(256, 256);
document.body.appendChild(renderer.view);

//load an image and run the `setup` function when it's done
loader
  .add("images/cat.png")
  .load(setup);

function setup() {

  //Create the `cat` sprite, add it to the stage, and render it
  var cat = new Sprite(resources["images/cat.png"].texture);  
  stage.addChild(cat);
  renderer.render(stage);
}

```
Most of the examples in this tutorial will use aliases for Pixi
objects that follow this same model. Unless otherwise stated, you can
assume that all the code examples use aliases like these.

This is all you need to know to start loading images and creating
sprites.

<a id='alittlemoreaboutloadingthings'></a>
### 进一步了解加载

The format I've shown you above is what I suggest you use as your
standard template for loading images and displaying sprites. So, you
can safely ignore the next few paragraphs and jump straight to the
next section, "Positioning sprites." But Pixi's `loader` object is
quite sophisticated and includes a few features that you should be
aware of, even if you don't use them on a regular basis. Let's
look at some of the most useful.

<a id='makeaspritefromanordinaryjavascriptimageobject'></a>
#### 1)从普通的JavaScript图片对象或Canvas创建精灵

For optimization and efficiency it’s always best to make a sprite from
a texture that’s been pre-loaded into Pixi’s texture cache. But if for
some reason you need to make a texture from a regular JavaScript
`Image`
object, you can do that using Pixi’s `BaseTexture` and `Texture`
classes:
```js
var base = new PIXI.BaseTexture(anyImageObject),
    texture = new PIXI.Texture(base),
    sprite = new PIXI.Sprite(texture);
```
You can use `BaseTexture.fromCanvas` if you want to make a texture
from any existing canvas element:
```js
var base = new PIXI.BaseTexture.fromCanvas(anyCanvasElement),
```
If you want to change the texture the sprite is displaying, use the
`texture` property. Set it to any `Texture` object, like this:
```js
anySprite.texture = PIXI.utils.TextureCache["anyTexture.png"];
```
You can use this technique to interactively change the sprite’s
appearance if something significant happens to it in the game.

<a id='assigninganametoaloadingfile'></a>
#### 2)为已加载的文件命名

It's possible to assign a unique name to each resource you want to
load. Just supply the name (a string) as the first argument in the
`add` method. For example, here's how to name an image of a cat as
`catImage`.
```js
PIXI.loader
  .add("catImage", "images/cat.png")
  .load(setup);
```
This creates an object called `catImage` in `loader.resources`.
That means you can create a sprite by referencing the `catImage` object, like this:
```js
var cat = new PIXI.Sprite(PIXI.loader.resources.catImage.texture);
```
However, I recommend you don't use this feature! That's because you'll
have to remember all names you gave each loaded files, as well as make sure
you don't accidentally use the same name more than once. Using the file path name, as we've done in previous
examples is simpler and less error prone.

<a id='monitoringloadprogress'></a>
#### 3)监控加载进度

Pixi's loader has a special `progress` event that will call a
customizable function that will run each time a file loads. `progress` events are called by the
`loader`'s `on` method, like this:
```js
PIXI.loader.on("progress", loadProgressHandler);
```
Here's how to include the `on` method in the loading chain, and call
a user-definable function called `loadProgressHandler` each time a file loads.
```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler() {
  console.log("loading"); 
}

function setup() {
  console.log("setup");
}
```
Each time one of the files loads, the progress event calls
`loadProgressHandler` to display "loading" in the console. When all three files have loaded, the `setup`
function will run. Here's the output of the above code in the console:
```js
loading
loading
loading
setup
```
That's neat, but it gets better. You can also find out exactly which file
has loaded and what percentage of overall files are have currently
loaded. You can do this by adding optional `loader` and
`resource` parameters to the `loadProgressHandler`, like this:
```js
function loadProgressHandler(loader, resource) { //...
```
You can then use `resource.url` to find the file that's currently
loaded. (Use `resource.name` if you want to find the optional name
that you might have assigned to the file, as the first argument in the
`add` method.) And you can use `loader.progress` to find what
percentage of total resources have currently loaded. Here's some code
that does just that.
```js
PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler(loader, resource) {

  //Display the file `url` currently being loaded
  console.log("loading: " + resource.url); 

  //Display the precentage of files currently loaded
  console.log("progress: " + loader.progress + "%"); 

  //If you gave your files names as the first argument 
  //of the `add` method, you can access them like this
  //console.log("loading: " + resource.name);
}

function setup() {
  console.log("All files loaded");
}
```
Here's what this code will display in the console when it runs:
```js
loading: images/one.png
progress: 33.333333333333336%
loading: images/two.png
progress: 66.66666666666667%
loading: images/three.png
progress: 100%
All files loaded
```
That's really cool, because you could use this as the basis for
creating a loading progress bar. 

(Note: There are additional properties you can access on the
`resource` object. `resource.error` will tell you of any possible
error that happened while
trying to load a file. `resource.data` lets you
access the file's raw binary data.)

<a id='moreaboutpixisloader'></a>
#### 4)更多关于Pixi的加载器

Pixi's loader is ridiculously feature-rich and configurable. Let's
take a quick bird's-eye view of its usage to
get you started.

The loader's chainable `add` method takes 4 basic arguments:
```js
add(name, url, optionObject, callbackFunction)
```
Here's what the loader's source code documentation has to say about
these parameters:

`name` (string): The name of the resource to load. If it's not passed, the `url` is used.  
`url` (string): The url for this resource, relative to the `baseUrl` of the loader.  
`options` (object literal): The options for the load.  
`options.crossOrigin` (Boolean): Is the request cross-origin? The default is to determine automatically.  
`options.loadType`: How should the resource be loaded? The default value is `Resource.LOAD_TYPE.XHR`.  
`options.xhrType`: How should the data being loaded be interpreted
when using XHR? The default value is `Resource.XHR_RESPONSE_TYPE.DEFAULT`  
`callbackFunction`: The function to call when this specific resource completes loading.

The only one of these arguments that's required is the `url` (the file that you want to
load.) 

Here are some examples of some ways you could use the `add`
method to load files. These first ones are what the docs call the loader's "normal syntax":
```js
.add('key', 'http://...', function () {})
.add('http://...', function () {})
.add('http://...')
```
And these are examples of the loader's "object syntax":
```js
.add({
  name: 'key2',
  url: 'http://...'
}, function () {})

.add({
  url: 'http://...'
}, function () {})

.add({
  name: 'key3',
  url: 'http://...'
  onComplete: function () {}
})

.add({
  url: 'https://...',
  onComplete: function () {},
  crossOrigin: true
})
```
You can also pass the `add` method an array of objects, or urls, or
both:
```js
.add([
  {name: 'key4', url: 'http://...', onComplete: function () {} },
  {url: 'http://...', onComplete: function () {} },
  'http://...'
]);
```
(Note: If you ever need to reset the loader to load a new batch of files, call the
loader's `reset` method: `PIXI.loader.reset();`)

Pixi's loader has many more advanced features, including options to
let you load and parse binary files of all types. This is not
something you'll need to do on a day-to-day basis, and way outside the
scope of this tutorial, so [make sure to check out the loader's GitHub repository
for more information](https://github.com/englercj/resource-loader).

<a id='positioning'></a>
## **放置精灵(Sprites)**

Now that you know how to create and display sprites, let's find out
how to position and resize them.

In the earlier example the cat sprite was added to stage at
the top left corner. The cat has an `x` position of
0 and a `y` position of 0. You can change the position of the cat by
changing the values of its `x` and `y` properties. Here's how you can center the cat in the stage by
setting its `x` and `y` property values to 96.
```js
cat.x = 96;
cat.y = 96;
```
Add these two lines of code anywhere inside the `setup`
function, after you've created the sprite. 
```js
function setup() {

  //Create the `cat` sprite
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Add the cat to the stage so you can see it
  stage.addChild(cat);

  //Render the stage
  renderer.render(stage);
}
```
(Note: In this example,
`Sprite` is an alias for `PIXI.Sprite`, `TextureCache` is an
alias for `PIXI.utils.TextureCache`, and `resources` is an alias for
`PIXI.loader.resources` as described earlier. I'll be
using alias that follow this same format for all Pixi objects and
methods in the example code from now on.)

These two new lines of code will move the cat 96 pixels to the right,
and 96 pixels down. Here's the result:

![Cat centered on the stage](/examples/images/screenshots/03.png)

The cat's top left corner (its left ear) represents its `x` and `y`
anchor point. To make the cat move to the right, increase the
value of its `x` property. To make the cat move down, increase the
value of its `y` property. If the cat has an `x` value of 0, it will be at
the very left side of the stage. If it has a `y` value of 0, it will
be at the very top of the stage.

![Cat centered on the stage - diagram](/examples/images/screenshots/04.png)

Instead of setting the sprite's `x` and `y` properties independently,
you can set them together in a single line of code, like this:
```js
sprite.position.set(x, y)
```
<a id='sizenscale'></a>
## **尺寸与缩放**

You can change a sprite's size by setting its `width` and `height`
properties. Here's how to give the cat a `width` of 80 pixels and a `height` of
120 pixels.
```js
cat.width = 80;
cat.height = 120;
```
Add those two lines of code to the `setup` function, like this:
```js
function setup() {

  //Create the `cat` sprite
  var cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Change the sprite's size
  cat.width = 80;
  cat.height = 120;

  //Add the cat to the stage so you can see it
  stage.addChild(cat);
}
```
Here's the result:

![Cat's height and width changed](/examples/images/screenshots/05.png)

You can see that the cat's position (its top left corner) didn't
change, only its width and height.

![Cat's height and width changed - diagram](/examples/images/screenshots/06.png)

Sprites also have `scale.x` and `scale.y` properties that change the
sprite's width and height proportionately. Here's how to set the cat's
scale to half size:
```js
cat.scale.x = 0.5;
cat.scale.y = 0.5;
```
Scale values are numbers between 0 and 1 that represent a
percentage of the sprite's size. 1 means 100% (full size), while
0.5 means 50% (half size). You can double the sprite's size by setting
its scale values to 2, like this:
```js
cat.scale.x = 2;
cat.scale.y = 2;
```
Pixi has an alternative, concise way for you set sprite's scale in one
line of code using the `scale.set` method.
```js
cat.scale.set(0.5, 0.5);
```
If that appeals to you, use it!

<a id='rotation'></a>
## **旋转**

You can make a sprite rotate by setting its `rotation` property to a
value in [radians](http://www.mathsisfun.com/geometry/radians.html).
```js
cat.rotation = 0.5;
```
But around which point does that rotation happen?

You've seen that a sprite's top left corner represents its `x` and `y` position. That point is
called the **anchor point**. If you set the sprite’s `rotation`
property to something like `0.5`, the rotation will happen *around the
sprite’s anchor point*.
This diagram shows what effect this will have on our cat sprite.

![Rotation around anchor point - diagram](/examples/images/screenshots/07.png)

You can see that the anchor point, the cat’s left ear, is the center of the imaginary circle around which the cat is rotating.
What if you want the sprite to rotate around its center? Change the
sprite’s `anchor` point so that it’s centered inside the sprite, like
this:
```js
cat.anchor.x = 0.5;
cat.anchor.y = 0.5;
```
The `anchor.x` and `anchor.y` values represent a percentage of the texture’s dimensions, from 0 to 1 (0%
to 100%). Setting it to 0.5 centers the texture over the point. The location of the point
itself won’t change, just the way the texture is positioned over it.

This next diagram shows what happens to the rotated sprite if you center its anchor point.

![Rotation around centered anchor point - diagram](/examples/images/screenshots/08.png)

You can see that the sprite’s texture shifts up and to the left. This
is an important side-effect to remember!

Just like with `position` and `scale`, you can set the anchor’s x and
y values with one line of code like this:
```js
sprite.anchor.set(x, y)
```
Sprites also have a `pivot` property which works in a similar way to
`anchor`. `pivot` sets the position
of the sprite's x/y origin point. If you change the pivot point and
then rotate the sprite, it will
rotate around that origin point. For example, the following code will
set the sprite's `pivot.x` point to 32, and its `pivot.y` point to 32
```js
cat.pivot.set(32, 32)
```
Assuming that the sprite is 64x64 pixels, the sprite will now rotate
around its center point. But remember: if you change a sprite's pivot
point, you've also changed its x/y origin point. 

So, what's the difference between `anchor` and `pivot`? They're really
similar! `anchor` shifts the origin point of the sprite's image texture, using a 0 to 1 normalized value.
`pivot` shifts the origin of the sprite's x and y point, using pixel
values. Which should you use? It's up to you. Just play around
with both of them and see which you prefer.
