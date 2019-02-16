# nugu

This theme is based on the [vim-colors-off][] colorscheme.

[vim-colors-off]: https://github.com/pbrisbin/vim-colors-off

Supports both `background=light` and `background=dark`.

## Rationale

Almost all of the existing themes are wrong.
In my opinion ;).

Especially the popular ones.
Contemporary themes choose to put emphasis on the least important syntax
elements.

Let us explore.

Programming languages consist of roughly the following syntax elements:

- Keywords (reserved words by any given language)
- Identifiers (names, symbols, variables,…)
- Language Symbols (operators, quotation marks, braces, commas, semicolons,…)
- Comments (inline, docs, header,…)
- Literals (strings, numbers, bools,…)

These can be classified into 2 groups.

- Words with characters you choose
  - Identifiers
  - Comments
  - Literals
- Words with characters chosen for you by language
  - Keywords
  - Language Symbols

In my opinion, the first group is more important than the second.
Especially once you are familiar with a programming language, keywords and
symbols become second nature to you.
It is less important any more, that keywords "jump out" at you.

Let us examine an example with a language, that has a high keyword-ratio: `lua`.

**Typical style:**
<pre>
<b>local function</b> append_all(buffer, ...)
  <b>for</b> i=1,<b>select</b>("#", ...) <b>do</b>
    table.insert(buffer, (<b>select</b>(i, ...)))
  <b>end</b>
<b>end</b>
</pre>

Notice how almost *50%* of words (\w) are *keywords*.
Granted, most other languages have lesser keyword-ratios;
However, in visual design it is often helpful to examine the extreme cases,
because subtle effect get amplified and thus get more noticable.

**Proposed style:**
<pre>
local function <b>append_all</b>(<b>buffer</b>, ...)
  for <b>i</b>=<b>1</b>,select(<b>"#"</b>, ...) do
    <b>table.insert</b>(<b>buffer</b>, (select(<b>i</b>, ...)))
  end
end
</pre>

> We could argue wether `table.insert` belongs to "Keywords" or "Identifiers" or
> not, but in either case, I think the example works.

In order to judge the effectiveness of the 2 emphasis styles, we will look at
the emphasized elements exclusively and try to guess the semantics of the
remaining code.

**Typical:**
<pre>
<b>local function</b>
  <b>for</b>     <b>select</b>           <b>do</b>
                          <b>select</b>
  <b>end</b>
<b>end</b>
</pre>

**Proposed:**
<pre>
               <b>append_all</b> <b>buffer</b>
       <b>i</b> <b>1</b>        <b>"#"</b>
    <b>table.insert</b> <b>buffer</b>          <b>i</b>


</pre>

In my opinion, the second style conveys the important semantics far better.

> Btw, what the function actually does is to concatenate n+1 strings.

Notice that in the examples we have discussed only one dimension of text style;
boldness.
But themes offer many more dimensions to confuse us.

Let us look at some and think about their use.

- Boldness
- Italics
- Color (text)
- Color (background)
- Underline

There are many other highlighting techiques imaginable.
From silly things like <blink>blinking</blink> to more useful ones like:

- Boxes around words
- Different font family and/or size
- Concealing elements (e.g. displaying `λ` instead of `function`)

However, since either vim does not support those, or I have no opinion on them
(yet?), we will ignore these.

> If you are curious to experiment with these kinds of highlightig styles check
> out editors like [Textadept] or [Howl] which support them.

One of these styles, **bold**, *italic*,
<font color="red">c</font>
<font color="blue">o</font>
<font color="pink">l</font>
<font color="green">o</font>
<font color="orange">r</font>,
is not like the others.
Technically, color is a group of dimensions.
Every single color is its own style.
The reason why themes limit themselves to a color pallete is partly astethics,
but mostly in order trim down this enourmous color space to a handful of useful
states.
Imagine a theme would assign every possible color to something.

<pre>
<font color="#889934">local</font> <font color="#735010">function</font> append_all(buffer, ...)
  <font color="#234253">for</font> i=1,<font color="#318776">select</font>("#", ...) <font color="#630081">do</font>
    table.insert(buffer, (<font color=#318776>select</font>(i, ...)))
  <font color="#129945">end</font>
<font color="#129945">end</font>
</pre>

These colors are almost meaningless.
Any style must be used judiciously in order to quickly communicate *something*.
Furthermore, the amount of styles used in total, should be low enough so that
humans can remember what they mean.

The way I order the importance of syntax elements is to following, from most to
least important:

1. Comments (inline)
1. Literal
1. Identifiers
1. Language Symbols
1. Keywords
1. Comments (header, docs)

[Textadept]: https://foicica.com/textadept/
[Howl]: https://howl.io
