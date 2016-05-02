# ![spam](https://cloud.githubusercontent.com/assets/1236790/14952933/3679edc8-1065-11e6-920a-207f8443f141.png)

spam.js is a small library to create modern [Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) maps with [D3](https://github.com/mbostock/d3). It makes it easy to create static or zoomable maps with automatic projection and retina resolution.

Custom projections, click/hover events,`d3.geo` path generators and multiple map features are supported.

Check the [API docs](https://github.com/lukasappelhans/spam.js/wiki/API) or continue reading for [examples](#examples).

## Introduction
When using spam.js you are still in charge of painting everything. However the library creates the canvas boilerplate and tries to handle as much as possible without putting constraints on the user.

In order to improve performance, spam.js uses two painting phases. The 'static' layer is created once (for every zoom level) and should contain the majority of operations. After these operations complete, the canvas is saved into a picture.

Now every time the canvas needs a repaint (e.g. for hover effects), spam.js enters the 'dynamic' painting phase. Here we provide the option to paint dynamic content, while painting the 'static' image in the background.

In order to get the most out of spam.js, we encourage you to think about which parts of your map are static and dynamic beforehand and then use the appropriate callbacks. The more code runs in the 'static' functions, the faster spam.js will become.

## Getting started
spam.js depends on [D3](https://github.com/mbostock/d3), [TopoJSON](https://github.com/mbostock/topojson) and [rbush](https://github.com/mourner/rbush).

Until PRs in [D3](https://github.com/mbostock/d3/pull/2784) and [TopoJSON](https://github.com/mbostock/topojson/pull/279) are merged, you'll need to use [our](https://github.com/lukasappelhans/d3) [forks](https://github.com/lukasappelhans/topojson). We have included a copy of each fork on the repo.

Clone the repository ([or download the zip](https://github.com/lukasappelhans/spam.js/archive/master.zip)) and include `spam.js` after D3, TopoJSON and rbush in your website.

````html
<script src="lib/d3.min.js"></script>
<script src="lib/topojson.min.js"></script>
<script src="rbush.min.js"></script>
<script src="spam.js"></script>
```

Here's the most basic map you can do:

```javascript
d3.json("map.json", function(error, d) {
    topojson.presimplify(d)

    var map = new StaticCanvasMap({
        element: "body",
        data: [
            {
                features: topojson.feature(d, d.objects["map"]),
                static: {
                    paintfeature: function(parameters, d) {
                        parameters.context.stroke()
                    }
                }
            }
        ]
    })
    map.init()
})
```

And that's it! A simple, static map in just a few lines of code! It will be automagically projected and centered in your container, nothing else needed.

## Examples
The best way to start making maps with spam.js is reading the examples. You can use the same structure in your maps and fork them with your own TopoJSON.

- [Basic static map](http://bl.ocks.org/martgnz/c48aa019de720fcd86030d3b07990d8d)
- [Basic zoomable map](http://bl.ocks.org/martgnz/fa8187c716c8a6d788eab7d51095b419)
- [Static map with labels](http://bl.ocks.org/martgnz/e5c0387a5bb675b061a2c0a9f573f86a)
- [Static data visualization](http://bl.ocks.org/martgnz/9023a67f080cca8b31ef5d6b1dcf4637)
- [Custom projection](http://bl.ocks.org/martgnz/d8bc3d6c29e712e3255f095671a51967)
- [Canvas globe](http://bl.ocks.org/martgnz/c1a5addfb6c2ec914f2d0bc9b3112b71)
- [Static choropleth](http://bl.ocks.org/martgnz/56664c7ea8efef56f93ca948ef855d06)
- [Zoomable choropleth](http://bl.ocks.org/martgnz/a61c2da0e45a108c857e)

## API
Check the [API docs](https://github.com/lukasappelhans/spam.js/wiki/API) on the wiki for more information.

## License
MIT © [newsapps.io](https://github.com/newsappsio).
