# Professional website: damienjacques.com

This directory contains the code of my professional website. In terms of design, my goal is to create something timeless (so I don't want to change it every year) by its minimalist and sober side. 

In terms of content, the goal is also to showcase the different dimensions of my professional experience in a clear and simple way. It should also be possible to find more detailed content if the visitor wishes.

From a code architecture point of view, I chose to start from a blank page avoiding frameworks in order to control a maximum of personalization of the site and that it can be hard on a github page.

I make intensive use of the `w3IncludeHTML()` function introduced by [w3](https://www.w3schools.com/howto/howto_html_include.asp).

```
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

This function allows me to integrate HTML into an HTML page in a very simple way (to my knowledge, although a rather obvious function, it is not natively integrated into the HTML code).  Thanks to this, I can organize my code in small chunks in the content folder, making it much easier to develop the site and read the code.

The disadvantage is the blinking effect when the different elements load. I think this should be fixable with some javascript but I haven't yet taken the time to go deeper into this problem. 

Translated with www.DeepL.com/Translator (free version)
