# mdbook-viz

add [mdbook](https://github.com/rust-lang-nursery/mdBook) to support [Viz.js](https://github.com/mdaines/viz.js)

It turns this:
```
```dot
digraph {
    a -> b
}
` ``` `
```
into this:

## HowTo

Add the following to your `book.toml`
```
[output.html]
additional-js = ["viz.js", "lite.render.js", "viz-init.js"]
```

- viz.js and lite.render.js from [viz.js release](https://github.com/mdaines/viz.js/releases) into your source directory.
- viz-init.js contains the following code.

```javascript:
function rendorGraphvizElementClass() {
    var viz = new Viz();
   var dot = document.querySelector(".language-dot");
   viz.renderSVGElement(dot.textContent)
   .then(function(element) {
     dot.parentNode.innerHTML = element.outerHTML;
   })
   .catch(error => {
     console.log(error);
   });
}

rendorGraphvizElementClass() ;
```
