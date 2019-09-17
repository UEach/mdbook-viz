# mdbook-viz

add [mdbook](https://github.com/rust-lang-nursery/mdBook) to support [Viz.js](https://github.com/mdaines/viz.js)

hint from [this Issues](https://github.com/rust-lang-nursery/mdBook/issues/762#issuecomment-502830041)

## HowTo

Add the following to your `book.toml`

    [output.html]
    additional-js = ["viz.js", "lite.render.js", "viz-init.js"]

- viz.js and lite.render.js from [viz.js release](https://github.com/mdaines/viz.js/releases) into your source directory.
- viz-init.js contains the following code.

```javascript
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

written Markdown `code` element for example

    ```dot
    digraph {
        a -> b
    }
    ```
and build it
