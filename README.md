# Sprinklr CSS Styleguide

## Table of Contents

 1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)
  1. [CSS](#css)
    - [Naming Conventions and Methodologies](#naming-conventions-and-methodologies)
    - [Syntax and Formatting](#syntax-and-formatting)
    - [Comments](#comments)
    - [ID Selectors](#id-selectors)
    - [Shorthand Notation](#shorthand-notation)
    - [Pixels vs rem](#pixels-vs-rem)
    - [Color Units](#color-units)
    - [Border](#border)
    - [Quotes](#quotes)
    - [!important](#!important)
    - [Vertical Margins](#vertical-margins)
    - [Calculations](#Calculations)
  1. [What Next?](#what-next)
    - [Must-Watch CSS Videos](#must-watch-css-videos)
    - [CSS Reading List](#css-reading-list)
    - [Websites to follow](#websites-to-follow)
    - [Podcasts](#podcasts)
    - [Twitter Accounts to follow](#twitter)

## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```css
.container {
  font-size: 1.2rem;
  line-height: 1.5;
}
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```
In gist:

```css
[selector] {
  [property]: [value];
  [<--declaration--->]
}
```

## CSS

###Naming Conventions and Methodologies

We will be using BEM for our naming convention. BEM stands for “Block”, “Element”, “Modifier”. It is a front-end methodology: a new way of thinking when developing Web interfaces.

Further Read: [Official BEM Website](https://en.bem.info/)

#####Block
A block is an independent entity, a “building block” of an application. A block can be either simple or compound (containing other blocks).

Block names must be unique within a project to unequivocally designate which block is being described. Only instances of the same block can have the same names.

A block name follows the block-name scheme and defines a namespace for elements and modifiers.

*Example*
```
menu
lang-switcher
```

*HTML*
```html
<div class="menu">...</div>
```

*CSS*

```css
.menu { color: red; }
```

#####Element
An element is a part of a block that performs a certain function. Elements are context-dependent: they only make sense in the context of the block that they belong to.

An element name is delimited by a double underscore (__).

Element names must be unique within the scope of a block. An element can be repeated several times.

*Example*

```
menu__item
lang-switcher__lang-icon
```

*HTML*

```html
<div class="menu"> ... <span class="menu__item"></span> </div>
```

*CSS*

```css
.menu__item { color: red; }
```

#####Modifier
A modifier defines a different state or version of a block or an element.

A modifier name is delimited by double hyphens (--).

*Example*

```
menu--hidden
```

*HTML*

```html
<div class="menu menu--hidden">...</div>
```

>Incorrect notation

>```html
><div class="menu--hidden">...</div>
>```
>Here the notation is missing the block that is affected by the modifier.

*CSS*

```css
.menu--hidden { 
  @include hidden; /* Using Bootstrap */  
}
```

The naming convention follows this pattern:

```css
.block {}
.block__element {}
.block--modifier {}
```

.block represents the higher level of an abstraction or component.
.block__element represents a descendent of .block that helps form .block as a whole.
.block--modifier represents a different state or version of .block.

The reason for double rather than single hyphens and underscores is so that your block itself can be hyphen delimited, for example:

```css
.site-search {} /* Block */
.site-search__field {} /* Element */
.site-search--full {} /* Modifier */
```

By reading some HTML with some classes in, you can see how – if at all – the chunks are related; something might just be a component, something might be a child, or element, of that component, and something might be a variation or modifier of that component. To use an analogy/model, think how the following things and elements are related:

```css
.person {}
.person__hand {}
.person--female {}
.person--female__hand {}
.person__hand--left {}
```

Taking the previous .site-search example again, with ‘regular’ naming:

```html
<form class="site-search full">
    <input type="text" class="field">
    <input type="Submit" value ="Search" class="button">
</form>
```

These classes are fairly loose, and don’t tell us much. Even though we can work it out, they’re very inexplicit. With BEM notation we would now have:

```html
<form class="site-search site-search--full">
    <input type="text" class="site-search__field">
    <input type="Submit" value ="Search" class="site-search__button">
</form>
```

>Important Note

>Never reference ```js-``` prefixed class names from CSS files. ```js-``` are used exclusively from JS files.

>Use the ```is-``` prefix for state rules that are shared between CSS and JS.

###Syntax and Formatting

* Use soft tab (2 spaces) for indentation
* Use dashes instead of camelCasing in class names.
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put a trailing semi-colon (;) on your last declaration.
* Put blank lines between rule declarations
* Write your CSS in alphabetical order
* 0 as a length should have no unit (e.g., Use 0 instead of 0rem)
* Don't prefix property values with a leading zero (e.g., Use .5 instead of 0.5 and -.5rem instead of -0.5rem).

*Bad*

```css
.avatar{
  border-radius:50%;
  border:0.2rem solid #fff;
  margin-right: 0.5rem; }
.no, .nope, .not_good {
  // ...
}
```

*Good*

```css
.avatar {
  border-radius: 50%;
  border: .2rem solid #fff;
  margin-right: .5rem;
}

.one,
.selector,
.per-line {
  // ...
}
```

Long, comma-separated property values - such as collections of shadows - or function arguments - such as those for gradients - should be arranged across multiple lines in an effort to improve readability and produce more useful diffs.

*Example*

```css
.selector {
  background-image:
    repeating-linear-gradient(
      -45deg,
      transparent,
      transparent 2.5rem,
      #ccc 2.5rem
    );
  box-shadow:
    .1rem .1rem .1rem #000,
    .2rem .2rem .2rem .2rem #ccc inset;
}
```

*Important Note*

Exception to multi-line CSS rule is for similar rulesets that only carry one declaration each.

*Example*

```css
.icon {
  background-image: url(/img/sprite.svg);
  display: inline-block;
  height: 1.6rem;
  width:  1.6rem;
}

.icon--search   { background-position:   0     0  ; }
.icon--help     { background-position: -16px   0  ; }
.icon--home     { background-position:   0   -16px; }
.icon--settings { background-position: -16px -16px; }
```

###Comments

* Prefer comments on their own line. Avoid end-of-line comments.

*Example*

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * TODO: This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

If you must use an id selector (#selector) make sure that you have no more than one in your rule declaration. 

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### Shorthand Notation

Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values. Common overused shorthand properties include:

* padding
* margin
* font
* background
* border
* border-radius

Excessive use of shorthand properties often leads to sloppier code with unnecessary overrides and unintended side effects.

**Bad**

```css
.element {
  margin: 0 0 1rem;
  background: #fff;
  background: url("image.jpg");
  border-radius: .3rem .3rem 0 0;
}
```

**Good**

```css
.element {
  margin-bottom: 1rem;
  background-color: #fff;
  background-image: url("image.jpg");
  border-top-left-radius: .3rem;
  border-top-right-radius: .3rem;
}
```

Further Read: [Mozilla Developer Network - Shorthand Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)

### Pixels vs. rem

Use `rem` instead of `px` in your styles. Using rem units gives us flexibility in our designs, and the ability to scale elements up and down, instead of being stuck with fixed sizes. We can use this flexibility to make our designs easier to adjust during development, more responsive, and to allow browser users to control the overall scale of sites for maximum readability.

The greatest power that rem units offer is not just that they give consistent sizing regardless of element inheritance. Rather, it’s that they give us a way to have user font size settings influence every single aspect of a site’s layout by using rem units where we used to use px units.

*Important Note*

Don’t use rem for Multi Column Layout Widths. Column widths in a layout should typically be % based so they can fluidly fit unpredictably sized viewports.

However single columns should still generally incorporate rem values via a max-width setting

*Example*

```css
.container {
  max-width: 75rem;
  width: 100%;
}
```
### Color Units

When implementing feature styles, you should only be using color variables provided by _variables.scss/variables.less.

When adding a color variable to _variables.scss, using hex color units are preferred over RGB, named, HSL, or HSLA values.

Lowercase all hex values. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.

Use shorthand hex values where available, e.g., #fff instead of #ffffff. 

**Bad**

```css
rgb(50, 50, 50);
white;
hsl(120, 100%, 50%);
hsla(120, 100%, 50%, 1);
```

**Good**

```css
#fff;
#fafafa;
```

### Border

Use `0` instead of `none` to specify that a style has no border.

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```

### Quotes

Quotes are optional in CSS and SCSS. You should use single quotes as it is visually clearer that the string is not a selector or a style property.

**Bad**

```css
background-image: url(/img/you.jpg);
font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
```

**Good**

```css
background-image: url("/img/you.jpg");
font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial;
```

### !important

Inspiration from [Stephanie Rewis](https://twitter.com/stefsull/status/70631020352913408):

>Using !important in your CSS usually means you're narcissistic & selfish or lazy. 
Respect the devs to come...

When an important rule is used on a style declaration, this declaration overrides any other declarations. Although technically !important has nothing to do with specificity, it interacts directly with it. **Using !important is bad practice** and should be avoided because it makes debugging more difficult by breaking the natural cascading in your stylesheets. When two conflicting declarations with the !important rule are applied to the same element, the declaration with greater specificity will be applied.

Some rules of thumb:

* Always look for a way to use specificity before even considering !important
* Only use !important on page-specific CSS that overrides site-wide or foreign CSS (from external libraries, like Bootstrap or normalize.css).
* Never use !important when you're writing a plugin/mashup.
* Never use !important on site-wide css.

Instead of using !important, you can:

* Make better use of CSS cascading properties
* Use more specific rules. 

Further Read: [Implications of using important](http://stackoverflow.com/questions/3706819/what-are-the-implications-of-using-important-in-css)

### Vertical Margin

Don’t use ```margin-top```. Vertical margins collapse. Always prefer ```padding-top``` or ```margin-bottom``` on preceding elements.

Further Read: [What You Should Know About Collapsing Margins](https://css-tricks.com/what-you-should-know-about-collapsing-margins/) and [Sitepoint's Collapsing Margins](http://www.sitepoint.com/web-foundations/collapsing-margins/)

### Calculations

Top-level numeric calculations should always be wrapped in parentheses. Not only does this requirement dramatically improve readability, it also prevents some edge cases by forcing css to evaluate the contents of the parentheses.

**Bad**

```css
.foo {
  width: 100% / 3;
}
```

**Good**

```css
.foo {
  width: (100% / 3);
}
```

## What Next?

### Must-Watch CSS Videos

*This is a collection of well-received talks about CSS, covering topics such as CSS frameworks, Sass, SVG, animation, scalability, CSS performance, tooling, mobile tips, and more.*

####2015

1. [mdo-ular CSS](http://jqueryuk.com/2015/videos.php?s=mdo-ular-css): Mark Otto, jQuery UK `30:06`
1. [PostCSS: The Future After Sass and LESS](https://www.youtube.com/watch?v=1yUFTrAxTzg&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Andrey Sitnik, CSSConf.US `29:09`
1. [Your Very Own Component Library](https://www.youtube.com/watch?v=zSYo7m5kGHQ&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Alex Sexton, JSConf.AR `20:03`
1. [Let's Move](https://www.youtube.com/watch?v=J6wUmQDQBkw&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Benjamin De Cock, CSSConf.AU `24:52`
1. [Motion Design with CSS](https://www.youtube.com/watch?v=TjsXqt-UxLo&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Val Head, OpenVis Conf `29:39`
1. [Cascading Shit Show](https://www.youtube.com/watch?v=iniwPUEbPUM&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Jacob Thornton, Code Genius `42:07`
1. [Inline Styles Are About to Kill CSS](https://www.youtube.com/watch?v=NoaxsCi13yQ&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Colin Megill, CSSConf.US `36:11`
1. [Let's Talk About Our CSS](https://www.youtube.com/watch?v=NHpSmJrEvRQ&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Michelle Bu, TXJS `18:11`
1. [Photoshop Is Dead!: Editing Images in CSS](https://www.youtube.com/watch?v=LY65F2e4B5w&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Una Kravets, CSSConf.EU `28:42`
1. [Enhancing Responsiveness With Flexbox](https://www.youtube.com/watch?v=_98SE8WUvLk&index=10&list=PL37ZVnwpeshHoV6GgvG9WWAP6rjnEdAs9): Zoe M. Gillenwater, CSSConf.EU `37:13`
1. [Move Slow and Fix Things](https://www.youtube.com/watch?v=zmjfh099zYg&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Daniel Eden, dotCSS `15:06`

####2014

1. [What Is a CSS Framework Anyway?](https://vimeo.com/95734680): Harry Roberts, Industry Conf `48:48`
1. [CSS Is a Mess](https://vimeo.com/99877232): Jonathan Snook, Beyond Tellerand `53:49`
1. [10 Commandments for Efficient CSS Architecture](https://www.youtube.com/watch?v=FYcu-wWrNqo&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Kushagra Gour, CSSConf.Asia `35:55`
1. [Slaying the Dragon: How to Refactor CSS for Maintainability](https://vimeo.com/100501790): Alicia Liu, Front-Trends `33:21`
1. [CSS in Your Pocket - Mobile CSS Tips from the Trenches](https://www.youtube.com/watch?v=vBHt61yDO9U&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Angelina Fabbro, CSSConf.US `34:19`
1. [Styling and Animating Scalable Vector Graphics with CSS](https://www.youtube.com/watch?v=lf7L8X6ZBu8&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Sara Soueidan, CSSConf.EU `29:16`
1. [Play Nice With CSS Tools and Methodologies](https://www.youtube.com/watch?v=-bZSTMLqf8Q&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Brad Westfall, HTML5DevConf `42:47`
1. [Build Scalable, Automated CSS](https://www.youtube.com/watch?v=Tk_0qYEFtAY&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Christian Lilley, CSSConf.Asia `48:47`
1. [CSS and the Critical Path](https://www.youtube.com/watch?v=_0Fk85to6hA&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Patrick Hamann, CSSConf.EU `33:42`
1. [All the Right Moves: How to Put Your UI in Motion](http://new.livestream.com/accounts/6779986/events/2928486/videos/51426837): Val Head, Multi-Mania `45:49`
1. [Present and Future of CSS Layout](https://vimeo.com/98746172): Tab Atkins, CSS Day `49:31`
1. [Managing CSS Projects with ITCSS](https://www.youtube.com/watch?v=1OKZOV-iLj4&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Harry Roberts, DaFED `1:13:51`
1. [Thinking Beyond "Scalable CSS"](https://www.youtube.com/watch?v=L8w3v9m6G04&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Nicolas Gallagher, dotCSS `28:46`
1. [Web Components & the Future of CSS](https://www.youtube.com/watch?v=QHxrr6Q82yI&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Philip Walton, SFHTML5 `40:02`
1. [CSS Performance Tooling](https://www.youtube.com/watch?v=FEs2jgZBaQA&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Addy Osmani, CSSConf.EU `46:27`
1. [3.14 Things I Didn’t Know About CSS](https://vimeo.com/100264064): Mathias Bynens, CSS Day `45:35`
1. [Effortless Style](http://vimeo.com/101718785): Heydon Pickering, CSS Day `49:51`


####2013

1. [When Bootstrap Attacks](https://www.youtube.com/watch?v=xbpnqbM6cRk&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Pamela Fox, CSSConf.US `28:48`
1. [CSS in the 4th Dimension](https://www.youtube.com/watch?v=NTJUFQmHbvc&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Lea Verou, JSConf.Asia `44:49`
1. [Automated CSS Testing](https://www.youtube.com/watch?v=2PU6JX4S7zI&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Jakob Mattsson, JSConf.Asia `42:07`
1. [CSSConf.EU Keynote](https://www.youtube.com/watch?v=ue-Z_HxS3cc&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Nicole Sullivan, CSSConf.EU `20:57`
1. [CSS Application Architecture](https://vimeo.com/74359951): Nicolas Gallagher, SmashingConf `38:36`
1. [Realigning & Refactoring UI](https://www.youtube.com/watch?v=I82ytAWxzrI&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Jina Bolton, SassConf `48:08`
1. [Normalizing Designs for Better Quality CSS](https://www.youtube.com/watch?v=ldx4ZFxMEeo&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Harry Roberts, CSSConf.EU `43:40`
1. [Automating the Removal of Unused CSS](https://www.youtube.com/watch?v=833xr1MyE30&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Addy Osmani, Velocity Europe Conference `5:57`
1. [The Humble Border-Radius](https://www.youtube.com/watch?v=2iFw2GCOPj0&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Lea Verou, Future of Web Design `37:07`
1. [Sass and OOCSS Sitting in a Tree K-I-S-S-I-N-G](https://vimeo.com/66039168): Nicole Sullivan, TXJS `27:50`
1. [Architecting Scalable CSS](https://vimeo.com/70041549): Harry Roberts, Beyond Tellerand `41:57`
1. [More CSS Secrets: Another 10 Things You May Not Know about CSS](https://www.youtube.com/watch?v=3ikye7Qc7Ak&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Lea Verou, W3Conf `60:39`


####2012

1. [Open Source Tools and Libraries for Designers](https://www.youtube.com/watch?v=hFdbE6T9QGc&list=PLUS3uVC08ZaqVEGFkl_dS_3FUzILkOIzA): Julie Ann Horvath, HTML5DevConf `29:39`.
1. [GitHub's CSS Performance](https://vimeo.com/54990931): Jon Rohan, CSS Dev Conf `40:50`.


####2010

1. [Handcrafted CSS](https://vimeo.com/17091905): Dan Cederholm, Build Conference `44:29`.
1. [The Top 5 Mistakes of Massive CSS](https://www.youtube.com/watch?v=j6sAm7CLoCQ): Nicole Sullivan, Build Conference `37:53`.

### CSS Reading List

1. [A Visual Guide to CSS3 Flexbox](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)
1. [CSS Floats](http://alistapart.com/article/css-floats-101)

### Websites to follow

1. [Codrops](http://tympanus.net/codrops/)
1. [A to Z CSS](http://www.atozcss.com/start-here/)

### Podcasts

*Something to listen to while programming.*

* [Shop Talk Show](http://shoptalkshow.com/) - A live podcast with Chris Coyier and Dave Rupert about front end web design, development, and UX.
* [Style Guide Podcast](http://styleguides.io/podcast/index.html) - A small batch series of interviews on Style Guides, hosted by Anna Debenham and Brad Frost.
* [The Big Web Show](http://5by5.tv/bigwebshow/) - topics like web publishing, art direction, content strategy, typography, web technology, and more. It's everything web that matters.
* [The Web Ahead](http://5by5.tv/webahead/) - Conversations with world experts on changing technologies and future of the web.
* [Non Breaking Space Show](http://goodstuff.fm/nbsp) - Seeking out the best, brightest, and smartest creative people on digital art, design, and development.
* [The Changelog](https://changelog.com/) - The tagline for the Changelog says it all: “Open Source moves fast. Keep up.” This podcast, and the accompanying blog, is all about keeping you updated with the latest in Open Source Technology.

### Twitter

*Active accounts to follow.*

* [CSS Animation](https://twitter.com/cssanimation)
* [Andrey Sitnik](https://twitter.com/andreysitnik) - Author of @Autoprefixer, http://easings.net  and @PostCSS.
* [Evangelina Ferreira](https://twitter.com/evaferreira92) - Web Designer. Professor at @multimedial_utn HTML5 & CSS Freak. Ocassional Translator.
* [Sara Soueidan](https://twitter.com/SaraSoueidan) - Author of the @Codrops CSS Reference & Co-author of the Smashing Book #5.
* [Hugo Giraudel](https://twitter.com/HugoGiraudel) - CSS goblin & Sass hacker at @edenspiekermann.
* [Guy Routledge](https://twitter.com/guyroutledge) - Front-end dev, Teacher @GA_London, Screencaster at http://www.atozcss.com, property snob, Foodie.
* [Heydon Pickering](https://twitter.com/heydonworks) - Moderate consumer of rice. Also a UX designer, author, @smashingmag editor and programmer.
* [Adam Morse](https://twitter.com/mrmrs_) - Advocate for users and open-source.
* [Donovan Hutchinson](https://twitter.com/donovanh) - Designer, developer, writer. Occasionally blogs at http://Hop.ie , and currently building @cssanimation.
* [CSS Commits](https://twitter.com/CSScommits) - Latest commits to @CSSWG’s public Mercurial repository.
* [Scott Jehl](https://twitter.com/scottjehl) - Author of @responsiblerwd, now on sale from @abookapart.
* [Dudley Storey](https://twitter.com/dudleystorey) - Web development writer, teacher, and speaker.
* [Zoe M. Gillenwater](https://twitter.com/zomigi) - Web designer/developer specializing in CSS, RWD, UX, & accessibility.
* [Ben Briggs](https://twitter.com/ben_eb) - Final year web technologies student. node.js, javascript, open source modules, client side optimisation, web performance.
* [Paul Lewis](https://twitter.com/aerotwist) - Googler who noodles with code and design.
* [Thierry Koblentz](https://twitter.com/thierrykoblentz) - CSSer @ Yahoo Only Tweeting Tech.
* [Nicolas Gallagher](https://twitter.com/necolas) - Software Engineer at @twitter.
* [Harry Roberts](https://twitter.com/csswizardry)- Consultant Front-end Architect: @google, @Etsy, @kickstarter, @BBC, @Deloitte, @FT, more.
* [Phil Walton](https://twitter.com/philwalton) - Engineer at Google • Open Source Advocate • Developer • Designer • Writer.
* [Lea Verou](https://twitter.com/LeaVerou) - Research Assistant @MIT_CSAIL, @CSSWG IE, @OReillyMedia author, Ex @W3C staff.
* [Manoela Ilic](https://twitter.com/crnacura) - ...aka Mary Lou @codrops ༶ CSS & HTML are my crayons ༶ Interested in Cognitive Science, AI, HCI, UI Design & Astrophysics ༶ Digital nomad.
* [Una Kravets](https://twitter.com/Una) - Front-end @IBMDesign. Sassvocate, community builder, & handcrafter. STEMinist :) Open source all the things!
* [Chris Coyier](https://twitter.com/chriscoyier) - Designer @CodePen. Writer @Real_CSS_Tricks.
* [Nicole Sullivan](https://twitter.com/stubbornella) - GEEK!
* [Eric Bidelman](https://twitter.com/ebidel) - Engineer at Google working on Chrome, web components, and Polymer.
* [Patrick Hamann](https://twitter.com/patrickhamann) - Lover of mountains, craft beers and discovering new food.
* [Dave McFarland](https://twitter.com/davemcfarland) - Web developer, author of CSS: The Missing Manual, JavaScript & jQuery.
* [L. David Baron](https://twitter.com/davidbaron) - Mozilla developer, CSS and W3C standards diplomat.
* [Daniel Glazman](https://twitter.com/glazou)W3C CSS Working Group Co-chairman, entrepreneur, software engineer, geek, father of two, polyglot, duck lover. Nah. Tweets are strictly mine.
* [The Chris Eppstein](https://twitter.com/chriseppstein) - Loves love. Hates hate. Has a kick-ass family. Writes code. Leads stylesheet tech @LinkedIn.
* [앗킨스 탭](https://twitter.com/tabatkins) - Literally Jenn Schiffer's Mom.
* [Natalie Weizenbaum](https://twitter.com/nex3) - Trans coder lady. Lead designer/developer of @SassCSS, working for @google on @dart_lang.
* [Brad Frost](https://twitter.com/brad_frost) - Web designer, speaker, writer, consultant, musician.
* [Maxime Thirouin](https://twitter.com/MoOx) - Freelance front-end vigilante, UI/UX developer.
* [Mark Otto](https://twitter.com/mdo) - GitHub and Bootstrap. Formerly at Twitter. Huge nerd.
* [Simon](https://twitter.com/simurai) - UI designer, CSS doodler.
* [Connor Sears](https://twitter.com/connors) - Designer at GitHub.
* [Remy Sharp](https://twitter.com/rem) - All about CSS sizing units.
* [Jonathan Snook](https://twitter.com/snookca) - Designer, Developer, Writer, Speaker. I make stuff on the web. I wrote SMACSS.
