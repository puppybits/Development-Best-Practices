# Performance Tips

#### Things that cause reflow

```

  Element-level
	clientHeight clientLeft clientTop clientWidth focus 
	getBoundingClientRect getClientRects innerText offsetHeight
	offsetLeft offsetParent offsetTop offsetWidth outerText
	scrollByLines scrollByPages scrollHeight scrollIntoView 
	scrollIntoViewIfNeeded scrollLeft scrollTop scrollWidth

	MouseEvent-level
	layerX layerY offsetX offsetY

	Window-level
	getComputedStyle scrollBy scrollTo scrollX scrollY
	Frame, Document & Image

	height width
```

#### Ways to miminie repaints

* for large changes remove element parent from the DOM into a document fragment, make edits, reattach. This will always trigger 2 repaints
* change class instead of setting styles inline. (jQuery animate and other functions are built to do this wrong)
* use position absolute on a parent element to limit the affects of an internal reflow


#### Things that are slow in JS

```

    JSON.parse, XMLHttpRequest, document.*, element.*

```

#### Things that are slow in the DOM

* `<img src="">`
 * causes an HTTP request
 * parsing a large image
 * inflates the image to an uncompressed state (in the case of PNG it roughly 3 times bigger)
 * allocates a huge region in the memory heap
 * triggers a repaint event
 * can trigger a reflow depending on the CSS properties
* creating lots of new DOM elements and destoring them
 * use object pooling minimize alloc/dealloc of DOM elements
 * don't create lots of DOM elements while other processor intensive things are happening (ie. scrolling, loading network resources)
* `<table>`  

#### example of how to defer work localy in a function

    function active(ids){
      if(cfg.delay)
      {
        setTimeout(function(){
          // do part of the work
          // in the next timeout do more
          // when all finished remove the timer
          // if new ids are passed in they will be executed on the next timeout
        },cfg.delay)
      }
    }

#### Saving memory is critical on low power devices

* single page web apps have to fre memory because browser can't change page to dealloc memory and clean up
* minimze throwaway objects.
 * when the object goes back to the pool. if you set it to a default state can cause a repaint.
* beware of CSS that causing compositing, opacities and effects. (background-position, background-repeat)
* only opacity and transforms are hardware accelerated. 
* images over 1024 are turned into a tile layer
* things that cause layer compositing: opacity, overflow, -webkit-transform, z-index, position, element overlaps
* check Webkit source for layers `WebCore/rendering/RenderBoxModelObject.h`
* magic CSS can cause new images going to the graphics card and getting redrawn
* caution with things like text-indent where the GPU could draw a huge layer and crash memory
* `translateZ(0)` puts things on it's own layer. Needs to be played with to get smooth on mobile devices.

`defaults write com.apple.Safari IncludeInternalDebugMenu 1`

#### Resources
[https://developers.google.com/speed/articles/reflow](https://developers.google.com/speed/articles/reflow)
[https://developers.google.com/speed/articles/browser-paint-events](https://developers.google.com/speed/articles/browser-paint-events)
[https://developers.google.com/speed/articles/javascript-dom](https://developers.google.com/speed/articles/javascript-dom)
[http://www-archive.mozilla.org/newlayout/doc/reflow.html](http://www-archive.mozilla.org/newlayout/doc/reflow.html)
[https://developers.google.com/chrome-developer-tools/docs/timeline](https://developers.google.com/chrome-developer-tools/docs/timeline)
[http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)


[Chrome flag switches](http://peter.sh/experiments/chromium-command-line-switches/)

