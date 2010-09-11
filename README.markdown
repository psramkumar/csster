# Csster

Small libary to generate CSS style rules within Javascript.

## Usage

<pre>
require('csster.js'); // however you manage dependencies

Csster.style({
  h1: {
    fontSize: 18,
    color: 'red'
  }
});

...
</pre>

### Format of CSS Rules

The *style* method accepts CSS rules passed either as arrays or hashes, arrays just being
a way to order the hashes. For example:

<pre>
{
    ul: {
      margin: 5;
      padding: 0;
    }
    'ul li:first': {
      paddingLeft: 20px;
    }
}
</pre>

Note that

* property names are automatically converted to the correct format from camelcase. Feel free to quote them as well.
* raw numbers are assumed to be "pixels" (or "px"), and rendered as such.
* any sort of selectors are allowed... they are just passed through to the stylesheet.

#### Nesting
Csster supports nesting of rules to keep things more concise:
<pre>
{
    ul: {
      margin: 5;
      li: {
        paddingLeft: 20;
      }
    }
}
</pre>

The "li" property in this case might be a selector or might be a property name. A list of valid
property names is used to identify properties right now, and otherwise it's considered a sub-selector.
(Think about this.)

#### Macros
It's all Javascript, so macros and more complex functions are easy to write. Just create a function
that returns a hash of values, for example:

<pre>
    function roundedCorners(radius) {
        return {
            '-webkit-border-radius': radius,
            '-moz-border-radius': radius,
            'border-radius': radius
        }
    }
</pre>

To "mix these in", use the "macro" key:

<pre>
{
    'div#featured_box': {
      backgroundColor: '#394c89';
      macro: roundedCorner(5);
    }
}
</pre>


## Todo

* Support more than one Macro
* Some color math
* Better name


## Motivation

This project comes from my frustration of trying to build standalone Javascript widgets. Web
projects always involve the combination of HTML DOM, CSS and Javascript. It's often simpler to
generate the necessary DOM within your Javascript, removing any coupling (and a simpler calling
convention) to a specific web page. But most widgets have certain style rules. To avoid
any coupling with the CSS at all, styles can be included inline, but these gets bulky 
and hard to read. The "rule" nature of CSS is nice. So widgets then have a Javascript
and CSS component. Wouldn't it be nice, though, to remove that CSS component. 

With the advent of SASS, the coupling is even more complicated, as now there's some other
tool completely unrelated to your component, written in some other language. Wouldn't
a unified approach be nice?


## Similar projects

http://revnode.com/oss/css/

## Legal

Copyright (c) 2010 Andrew J. Peterson
All Rights Reserved.