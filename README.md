# Professional website: damienjacques.com

This directory contains the code of my professional website. In terms of design, my goal was to create something timeless (I don't want to change it every year) by its minimalist and sober aspect. I was greatly inspired by [Ulf Aslak's website](https://ulfaslak.com/b), whose graphic direction I like very much.

In terms of content, the aim is to showcase the different dimensions of my professional experience in a clear and simple way. It should also be possible to find more detailed content if the visitor wishes.

From a code architecture point of view, I decided to start from a blank page by not using any existing framework or development tools for two reasons: (i) complete control of each component (ii) easy to render on a github page.

I make intensive use of the `w3IncludeHTML()`, a function introduced by [w3](https://www.w3schools.com/howto/howto_html_include.asp):

```js
function w3IncludeHTML(cb) {
    var z, i, elmnt, file, xhttp;
    z = document.getElementsByTagName("*");
    for (i = 0; i < z.length; i++) {
        elmnt = z[i];
        file = elmnt.getAttribute("w3-include-html");
        if (file) {
            xhttp = new XMLHttpRequest();
            xhttp.onreadystatechange = function () {
                if (this.readyState == 4 && this.status == 200) {
                    elmnt.innerHTML = this.responseText;
                    elmnt.removeAttribute("w3-include-html");
                    w3IncludeHTML(cb);
                }
            }
            xhttp.open("GET", file, true);
            xhttp.send();
            return;
        }
    }
    if (cb) cb();
}
```

This function allows me to integrate HTML chunks into an HTML page in a very simple way (to my knowledge, although a rather obvious function, it is not natively integrated into the HTML code).  Thanks to this, I can organize my code in small chunks in the content folder, making it much easier to develop the site and read the code.

The disadvantage is the blinking effect when the different elements load. I think this should be fixable with some javascript but I haven't yet taken the time to go deeper into this problem. 

To import js scripts and css stylesheet, I use a simulated approach by including in the header using `link rel="import"`:

```html
<link rel="import" href="header.html">
```

If you use this approach, it's worth noting that `<meta>` tags must still be included in each individual page (especially `viewport` to ensure responsiveness):

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```

