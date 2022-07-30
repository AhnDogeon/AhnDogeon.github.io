# Initial_post

Initial Post
This article offers a sample of basic Markdown syntax that can be used in Hugo content files.

{{< admonition >}} This article is a shameful copy of the great Grav original page.

If you want to know about the extented Markdown syntax of LoveIt theme, please read extended Markdown syntax page. {{< /admonition >}}

Let's face it: Writing content for the Web is tiresome. WYSIWYG editors help alleviate this task, but they generally result in horrible code, or worse yet, ugly web pages.

Markdown is a better way to write HTML, without all the complexities and ugliness that usually accompanies it.

Some of the key benefits are:

Markdown is simple to learn, with minimal extra characters, so it's also quicker to write content.
Less chance of errors when writing in Markdown.
Produces valid XHTML output.
Keeps the content and the visual display separate, so you cannot mess up the look of your site.
Write in any text editor or Markdown application you like.
Markdown is a joy to use!
John Gruber, the author of Markdown, puts it like this:

The overriding design goal for Markdown’s formatting syntax is to make it as readable as possible. The idea is that a Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions. While Markdown’s syntax has been influenced by several existing text-to-HTML filters, the single biggest source of inspiration for Markdown’s syntax is the format of plain text email.

{{< style "text-align: right;" >}}-- John Gruber{{< /style >}}

Without further delay, let us go over the main elements of Markdown and what the resulting HTML looks like!

{{< admonition tip >}} :(far fa-bookmark fa-fw): Bookmark this page for easy future reference! {{< /admonition >}}

1. Headings
Headings from h2 through h6 are constructed with a # for each level:

## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading
The HTML looks like this:

<h2>h2 Heading</h2>
<h3>h3 Heading</h3>
<h4>h4 Heading</h4>
<h5>h5 Heading</h5>
<h6>h6 Heading</h6>
{{< admonition note "Heading IDs" >}} To add a custom heading ID, enclose the custom ID in curly braces on the same line as the heading:

### A Great Heading {#custom-id}
The HTML looks like this:

<h3 id="custom-id">A Great Heading</h3>
{{< /admonition >}}

2. Comments
Comments should be HTML compatible.

<!--
This is a comment
-->
Comment below should NOT be seen:

3. Horizontal Rules
The HTML <hr> element is for creating a "thematic break" between paragraph-level elements. In Markdown, you can create a <hr> with any of the following:

___: three consecutive underscores
---: three consecutive dashes
***: three consecutive asterisks
The rendered output looks like this:

4. Body Copy
Body copy written as normal, plain text will be wrapped with <p></p> tags in the rendered HTML.

So this body copy:

Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri,
animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex,
soluta officiis concludaturque ei qui, vide sensibus vim ad.
The HTML looks like this:

<p>Lorem ipsum dolor sit amet, graecis denique ei vel, at duo primis mandamus. Et legere ocurreret pri, animal tacimates complectitur ad cum. Cu eum inermis inimicus efficiendi. Labore officiis his ex, soluta officiis concludaturque ei qui, vide sensibus vim ad.</p>
A line break can be done with one blank line.

5. Inline HTML
If you need a certain HTML tag (with a class) you can simply use HTML:

Paragraph in Markdown.

<div class="class">
    This is <b>HTML</b>
</div>

Paragraph in Markdown.
6. Emphasis
6.1. Bold
For emphasizing a snippet of text with a heavier font-weight.

The following snippet of text is rendered as bold text.

**rendered as bold text**
__rendered as bold text__
The HTML looks like this:

<strong>rendered as bold text</strong>
6.2. Italics
For emphasizing a snippet of text with italics.

The following snippet of text is rendered as italicized text.

*rendered as italicized text*
_rendered as italicized text_
The HTML looks like this:

<em>rendered as italicized text</em>
6.3. Strikethrough
In [GFM]^(GitHub flavored Markdown) you can do strikethroughs.

~~Strike through this text.~~
The rendered output looks like this:

Strike through this text.

The HTML looks like this:

<del>Strike through this text.</del>
6.4. Combination
Bold, italics, and strikethrough can be used in combination.

***bold and italics***
~~**strikethrough and bold**~~
~~*strikethrough and italics*~~
~~***bold, italics and strikethrough***~~
The rendered output looks like this:

bold and italics

strikethrough and bold

strikethrough and italics

bold, italics and strikethrough

The HTML looks like this:

<em><strong>bold and italics</strong></em>
<del><strong>strikethrough and bold</strong></del>
<del><em>strikethrough and italics</em></del>
<del><em><strong>bold, italics and strikethrough</strong></em></del>
7. Blockquotes
For quoting blocks of content from another source within your document.

Add > before any text you want to quote:

> **Fusion Drive** combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.
The rendered output looks like this:

Fusion Drive combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.

The HTML looks like this:

<blockquote>
  <p>
    <strong>Fusion Drive</strong> combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.
  </p>
</blockquote>
Blockquotes can also be nested:

> Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue.
Nunc augue augue, aliquam non hendrerit ac, commodo vel nisi.
>> Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula. Donec auctor
odio non est accumsan facilisis. Aliquam id turpis in dolor tincidunt mollis ac eu diam.
The rendered output looks like this:

Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue. Nunc augue augue, aliquam non hendrerit ac, commodo vel nisi.

Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula. Donec auctor odio non est accumsan facilisis. Aliquam id turpis in dolor tincidunt mollis ac eu diam.

8. Lists
8.1. Unordered
A list of items in which the order of the items does not explicitly matter.

You may use any of the following symbols to denote bullets for each list item:

* valid bullet
- valid bullet
+ valid bullet
For example:

* Lorem ipsum dolor sit amet
* Consectetur adipiscing elit
* Integer molestie lorem at massa
* Facilisis in pretium nisl aliquet
* Nulla volutpat aliquam velit
  * Phasellus iaculis neque
  * Purus sodales ultricies
  * Vestibulum laoreet porttitor sem
  * Ac tristique libero volutpat at
* Faucibus porta lacus fringilla vel
* Aenean sit amet erat nunc
* Eget porttitor lorem
The rendered output looks like this:

Lorem ipsum dolor sit amet
Consectetur adipiscing elit
Integer molestie lorem at massa
Facilisis in pretium nisl aliquet
Nulla volutpat aliquam velit
Phasellus iaculis neque
Purus sodales ultricies
Vestibulum laoreet porttitor sem
Ac tristique libero volutpat at
Faucibus porta lacus fringilla vel
Aenean sit amet erat nunc
Eget porttitor lorem
The HTML looks like this:

<ul>
  <li>Lorem ipsum dolor sit amet</li>
  <li>Consectetur adipiscing elit</li>
  <li>Integer molestie lorem at massa</li>
  <li>Facilisis in pretium nisl aliquet</li>
  <li>Nulla volutpat aliquam velit
    <ul>
      <li>Phasellus iaculis neque</li>
      <li>Purus sodales ultricies</li>
      <li>Vestibulum laoreet porttitor sem</li>
      <li>Ac tristique libero volutpat at</li>
    </ul>
  </li>
  <li>Faucibus porta lacus fringilla vel</li>
  <li>Aenean sit amet erat nunc</li>
  <li>Eget porttitor lorem</li>
</ul>
8.2. Ordered
A list of items in which the order of items does explicitly matter.

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis in pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Aenean sit amet erat nunc
8. Eget porttitor lorem
The rendered output looks like this:

Lorem ipsum dolor sit amet
Consectetur adipiscing elit
Integer molestie lorem at massa
Facilisis in pretium nisl aliquet
Nulla volutpat aliquam velit
Faucibus porta lacus fringilla vel
Aenean sit amet erat nunc
Eget porttitor lorem
The HTML looks like this:

<ol>
  <li>Lorem ipsum dolor sit amet</li>
  <li>Consectetur adipiscing elit</li>
  <li>Integer molestie lorem at massa</li>
  <li>Facilisis in pretium nisl aliquet</li>
  <li>Nulla volutpat aliquam velit</li>
  <li>Faucibus porta lacus fringilla vel</li>
  <li>Aenean sit amet erat nunc</li>
  <li>Eget porttitor lorem</li>
</ol>
{{< admonition tip >}} If you just use 1. for each number, Markdown will automatically number each item. For example:

1. Lorem ipsum dolor sit amet
1. Consectetur adipiscing elit
1. Integer molestie lorem at massa
1. Facilisis in pretium nisl aliquet
1. Nulla volutpat aliquam velit
1. Faucibus porta lacus fringilla vel
1. Aenean sit amet erat nunc
1. Eget porttitor lorem
The rendered output looks like this:

Lorem ipsum dolor sit amet
Consectetur adipiscing elit
Integer molestie lorem at massa
Facilisis in pretium nisl aliquet
Nulla volutpat aliquam velit
Faucibus porta lacus fringilla vel
Aenean sit amet erat nunc
Eget porttitor lorem {{< /admonition >}}
8.3. Task Lists
Task lists allow you to create a list of items with checkboxes. To create a task list, add dashes (-) and brackets with a space ([ ]) before task list items. To select a checkbox, add an x in between the brackets ([x]).

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
The rendered output looks like this:

 Write the press release
 Update the website
 Contact the media
9. Code
9.1. Inline Code
Wrap inline snippets of code with `.

In this example, `<section></section>` should be wrapped as **code**.
The rendered output looks like this:

In this example, <section></section> should be wrapped as code.

The HTML looks like this:

<p>
  In this example, <code>&lt;section&gt;&lt;/section&gt;</code> should be wrapped with <strong>code</strong>.
</p>
9.2. Indented Code
Or indent several lines of code by at least four spaces, as in:

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code
The rendered output looks like this:

// Some comments
line 1 of code
line 2 of code
line 3 of code
The HTML looks like this:

<pre>
  <code>
    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code
  </code>
</pre>
9.3. Block Fenced Code
Use "fences" ``` to block in multiple lines of code with a language attribute.

{{< highlight markdown >}}

Sample text here...
{{< / highlight >}}

The HTML looks like this:

<pre language-html>
  <code>Sample text here...</code>
</pre>
9.4. Syntax Highlighting
[GFM]^(GitHub Flavored Markdown) also supports syntax highlighting.

To activate it, simply add the file extension of the language you want to use directly after the first code "fence", ```js, and syntax highlighting will automatically be applied in the rendered HTML.

For example, to apply syntax highlighting to JavaScript code:

{{< highlight markdown >}}

grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
{{< / highlight >}}

The rendered output looks like this:

grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
{{< admonition >}} Syntax highlighting page in Hugo Docs introduces more about syntax highlighting, including highlight shortcode. {{< /admonition >}}

10. Tables
Tables are created by adding pipes as dividers between each cell, and by adding a line of dashes (also separated by bars) beneath the header. Note that the pipes do not need to be vertically aligned.

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
The rendered output looks like this:

Option	Description
data	path to data files to supply the data that will be passed into templates.
engine	engine to be used for processing templates. Handlebars is the default.
ext	extension to be used for dest files.
The HTML looks like this:

<table>
  <thead>
    <tr>
      <th>Option</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>data</td>
      <td>path to data files to supply the data that will be passed into templates.</td>
    </tr>
    <tr>
      <td>engine</td>
      <td>engine to be used for processing templates. Handlebars is the default.</td>
    </tr>
    <tr>
      <td>ext</td>
      <td>extension to be used for dest files.</td>
    </tr>
  </tbody>
</table>
{{< admonition note "Right or center aligned text" >}} Adding a colon on the right side of the dashes below any heading will right align text for that column.

Adding colons on both sides of the dashes below any heading will center align text for that column.

| Option | Description |
|:------:| -----------:|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
The rendered output looks like this:

Option	Description
data	path to data files to supply the data that will be passed into templates.
engine	engine to be used for processing templates. Handlebars is the default.
ext	extension to be used for dest files.
{{< /admonition >}}	
11. Links {#links}
11.1. Basic Link
<https://assemble.io>
<contact@revolunet.com>
[Assemble](https://assemble.io)
The rendered output looks like this (hover over the link, there is no tooltip):

https://assemble.io

contact@revolunet.com

Assemble

The HTML looks like this:

<a href="https://assemble.io">https://assemble.io</a>
<a href="mailto:contact@revolunet.com">contact@revolunet.com</a>
<a href="https://assemble.io">Assemble</a>
11.2. Add a Title
[Upstage](https://github.com/upstage/ "Visit Upstage!")
The rendered output looks like this (hover over the link, there should be a tooltip):

Upstage

The HTML looks like this:

<a href="https://github.com/upstage/" title="Visit Upstage!">Upstage</a>
11.3. Named Anchors
Named anchors enable you to jump to the specified anchor point on the same page. For example, each of these chapters:

## Table of Contents
  * [Chapter 1](#chapter-1)
  * [Chapter 2](#chapter-2)
  * [Chapter 3](#chapter-3)
will jump to these sections:

## Chapter 1 <a id="chapter-1"></a>
Content for chapter one.

## Chapter 2 <a id="chapter-2"></a>
Content for chapter one.

## Chapter 3 <a id="chapter-3"></a>
Content for chapter one.
{{< admonition >}} The specific placement of the anchor tag seems to be arbitrary. They are placed inline here since it seems to be unobtrusive, and it works. {{< /admonition >}}

12. Footnotes
Footnotes allow you to add notes and references without cluttering the body of the document. When you create a footnote, a superscript number with a link appears where you added the footnote reference. Readers can click the link to jump to the content of the footnote at the bottom of the page.

To create a footnote reference, add a caret and an identifier inside brackets ([^1]). Identifiers can be numbers or words, but they can’t contain spaces or tabs. Identifiers only correlate the footnote reference with the footnote itself — in the output, footnotes are numbered sequentially.

Add the footnote using another caret and number inside brackets with a colon and text ([^1]: My footnote.). You don’t have to put footnotes at the end of the document. You can put them anywhere except inside other elements like lists, block quotes, and tables.

This is a digital footnote[^1].
This is a footnote with "label"[^label]

[^1]: This is a digital footnote
[^label]: This is a footnote with "label"
This is a digital footnote1.

This is a footnote with "label"2

13. Images
Images have a similar syntax to links but include a preceding exclamation point.

![Minion](https://octodex.github.com/images/minion.png)
Minion

or:

![Alt text](https://octodex.github.com/images/stormtroopocat.jpg "The Stormtroopocat")
Alt text

Like links, images also have a footnote style syntax:

![Alt text][id]
Alt text

With a reference later in the document defining the URL location:

[id]: https://octodex.github.com/images/dojocat.jpg  "The Dojocat"
Footnotes
This is a digital footnote ↩

This is a footnote with "label" ↩
