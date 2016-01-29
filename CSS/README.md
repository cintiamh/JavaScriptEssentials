# CSS Reference

* https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
* http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048
* http://tutorialzine.com/2013/10/12-awesome-css3-features-you-can-finally-use/

## Selectors

### Element

```css
span {
  background-color: DodgerBlue;
  color: #ffffff;
}
```

```html
<span>Here's a span with some text.</span>
<p>Here's a p with some text.</p>
```

### Class

```css
span.classy {
  background-color: DodgerBlue;
}
```

```html
<span class="classy">Here's a span with some text.</span>
<span>Here's another.</span>
```

### Id

```css
span#identified {
  background-color: DodgerBlue;
}
```

```html
<span id="identified">Here's a span with some text.</span>
<span>Here's another.</span>
```

### Universal Selectors

`*` matches a single element of any type.
`*.warning` and `.warning` are considered equal.

* `ns|*` matches all elements in namespace ns
* `*|*` matches all elements
* `|*` matches all elements without any declared namespace

```css
* [lang^=en] {
  color:green;
}
*.warning {
  color:red;
}
*#maincontent {
  border: 1px solid blue;
}
```

```html
<p class="warning">
  <span lang="en-us">A green span</span> in a red paragraph.
</p>
<p id="maincontent" lang="en-gb">
  <span class="warning">A red span</span> in a green paragraph.
</p>
```

### Attribute Selectors

Select an element using the presence of a given attribute or attribute value.

* `[attr]` element with an attribute name of `attr`.
* `[attr=value]` element with an attribute name of `attr` and whose value is exactly "value".
* `[attr~=value]` element with an attribute name of `attr` whose value is a whitespace-separated list of words, one of which is exactly "value".
* `[attr|=value]` element with an attribute name of `attr`. Its value can be exactly “value” or can begin with “value” immediately followed by “-” (U+002D). It can be used for language subcode matches.
* `[attr^=value]` element with an attribute name of `attr` and whose value is prefixed by "value".
* `[attr$=value]` element with an attribute name of `attr` and whose value is suffixed by "value".
* `[attr*=value]` element with an attribute name of `attr` and whose value contains at least one occurrence of string "value" as substring.
* `[attr operator value i]` Adding an i before the closing bracket causes the value to be compared case-insensitively (for characters within the ASCII range).

```css
/* All spans with a "lang" attribute are bold */
span[lang] {font-weight:bold;}

/* All spans in Portuguese are green */
span[lang="pt"] {color:green;}

/* All spans in US English are blue  */
span[lang~="en-us"] {color: blue;}

/* Any span in Chinese is red, matches
   simplified (zh-CN) or traditional (zh-TW) */
span[lang|="zh"] {color: red;}

/* All internal links have a gold background */
a[href^="#"] {background-color:gold}

/* All links to urls ending in ".cn" are red */
a[href$=".cn"] {color: red;}

/* All links to with "example" in the url have a grey background */
a[href*="example"] {background-color: #CCCCCC;}

/* All email inputs have a blue border */
/* This matches any capitalization of
   "email", e.g. "email", "EMAIL", "eMaIL", etc. */
input[type="email" i] {border-color: blue;}
```

```html
<div class="hello-example">
    <a href="http://example.com">English:</a>
    <span lang="en-us en-gb en-au en-nz">Hello World!</span>
</div>
<div class="hello-example">
    <a href="#portuguese">Portuguese:</a>
    <span lang="pt">Olá Mundo!</span>
</div>
<div class="hello-example">
    <a href="http://example.cn">Chinese (Simplified):</a>
    <span lang="zh-CN">世界您好！</span>
</div>
<div class="hello-example">
    <a href="http://example.cn">Chinese (Traditional):</a>
    <span lang="zh-TW">世界您好！</span>
</div>
```
