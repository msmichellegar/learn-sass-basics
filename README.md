# Learn SASS Basics

This is a simple tutorial for learning SASS basics in about 30 minutes to an hour. Based on the official [Learn SASS](http://sass-lang.com/guide) guide, but a tad more verbose.

## What is SASS?

SASS stands for Syntactically-Awesome Style Sheets. It's a "pre-compiler" for CSS. Basically, it's software that allows you to write your CSS in really simple, convenient shorthand. So instead of writing *real* CSS, you write all your stylesheets in shorthand, and then use SASS to compile your docs into fully-functional CSS to include in your HTML docs. Pretty neat.

## Installing SASS

First things first, you've got to install SASS.

#### Linux Users

You'll have to [install Ruby](https://www.ruby-lang.org/en/documentation/installation/) first. Once you've done that, run this command in your terminal:

```sudo su -c "gem install sass"```

#### Mac Users

Congratulations, you already have Ruby installed. Just run this command in your terminal:

```gem install sass```

Check it has installed correctly by running ```sass -v```. Your terminal should return the current version of SASS (something like ```Sass 3.4.15 (Selective Steve)```).

If it didn't work correctly, read the official installation instructions [here](http://sass-lang.com/install).

## Setting up your SASS Docs

You'll need to set up your docs for this tutorial.

#### 1. Create a SCSS file

This guide uses SCSS (Sassy CSS) syntax, which is the primary SASS syntax (there's also pure SASS, but don't worry about it).

This means we need a file with a SCSS extension. So in your preferred directory, create a file named something like "*style.scss*".

#### 2. Link it to a CSS file

In your terminal, navigate to the directory where you've saved the SCSS file. Run this command:

```sass style.scss style.css```

This command will link your input SCSS file to an output CSS file. It will create the output file for you with your given name (you can also link it to a pre-existing file, but it will override any content).

It should also create a file called something like "*style.css.map*" that will map one file to the other.

#### 3. "Watch" the files

Your files won't compile automatically, so you need to put them on "watch". This means that whenever you make changes in the SCSS file, the CSS will automatically update. Run this command:

```sass --watch style.scss:style.css```

## Writing SASS

You can write regular CSS in your SCSS files, but you should take advantage of all the cool features of SASS. Here are the most important ones.

#### Nesting

With SASS you can create a clear, visual hierarchy like in HTML. Nesting is one of the most intuitive parts of SASS — it's something you've probably always wanted to do in CSS anyway (just me?).

Check this out. You can put all your styles for the navbar in the same block.

```CSS
navbar {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 10px;
    text-decoration: none;
  }
}
```

Still have your "*style.css*" file open? Save the SCSS file, and if you check now, it should have converted your SCSS code into regular, boring ol' CSS. You should see it running it in the terminal too.

#### Variables

Variables are an awesome way to store styles you'll want to reuse often in your CSS. Use them for fonts, colours, whatever you fancy. You define them using the ```$``` sign. Like so:

```CSS
$main-font: Helvetica, sans-serif;
$main-color: #F4F4F4;

body {
  font: $main-font;
  color: $main-color;
}
```

Once again, check your CSS file and that should convert to real values.

#### Partials

SASS lets you modularise your CSS in really cool ways, just like your JavaScript. You can create little snippets of styles to import and use elsewhere. These are called "partials". To create a partial, save a SCSS file with an underscore, like "*_partial.scss*".

There are lots of cool ways to use partials. For example, you can store all your variables in a partial and import them to your main SCSS file.

Create a partial file called "*_variables.scss*". Move your font and colour variables from above to this file. Then, in your "*style.scss*" file, you need to import the partial, like so.

```@import 'variables';```

Your files should now look like this:

#####_variables.scss

```CSS
$main-font: Helvetica, sans-serif;
$main-color: #F4F4F4;
```

#####main.scss
```CSS
@import 'variables';

body {
  font: $main-font;
  color: $main-color;
}

navbar {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 10px;
    text-decoration: none;
  }
}
```

Your CSS file will merge all your "imported" partials into one stylesheet.

#### Mixins

Mixins let you group CSS declarations together, so you don't have to repeat them tediously. This is especially useful for vendor prefixes like "webkit" and "moz". Now they won't have to clutter up your stylesheets. You write them like so, and then "import" them when necessary.

```CSS
@mixin transition($transition) {
  -webkit-transition: $transition;
     -moz-transition: $transition;
       -o-transition: $transition;
      -ms-transition: $transition;
          transition: $transition;
}

.button:hover {
  filter: alpha(opacity=30);
  opacity: 0.6;
  @include transition (all 0.3s ease);
}
```
As with variables, it's a good idea to save them in a separate module (like "*_mixins.scss*") for ease of reference.

#### Extend

The @extend feature of SASS lets you use the properties of one element for another. This saves any repetition, and saves you having to write multiple class names in HTML.

In this example (from [Learn Sass](http://sass-lang.com/guide)), the properties of ```.message``` are included in ```.sucess```, ```.error``` and ```.warning```.

```CSS
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```

#### Operators

SASS also lets you do maths in your stylesheets. Haven't you always dreamed of this? Feel free to throw standard mathematical operators into your SCSS files.

For example, convert all your widths and heights to percentages.

```CSS
.container {
  width: 100%;
}

.article {
  float: left;
  width: 600px / 960px * 100%;
}

.aside {
  float: right;
  width: 300px / 960px * 100%;
}
```

## Enjoy the SASS Magic

Now you can write SASS! If you're looking for more resources, you can find the official documentation [here](http://sass-lang.com/documentation/file.SASS_REFERENCE.html), which should clue you into more extravagant, magical features.
