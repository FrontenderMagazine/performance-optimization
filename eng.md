![][1]

Delays in performance have the potential to impact user [engagement][2], 
[experience][3] and [revenue][4]. Thankfully, Google's 'Make The Web Faster'
team recommend a set of best-practice[rules][5] for keeping your pages lean,
fast and smooth. These include minifying resources like CSS and JavaScript, 
optimizing images, inlining and removing unused styles and so on.

If you have complete control over your server, an excellent [PageSpeed][6] 
[Module][7] for [Apache][8] and [Nginx][9] exists with filters for many of
these tasks. If not however, or you feel the module isn’t quite for you, a 
number of build-tasks exist for tools you’re probably already using to fill in 
the gaps with more granular control.

The below represent [Grunt][10] and [Gulp][11] tasks the Yeoman team regularly
use in our projects. We’ve tried our best to keep this list focused and exclude 
previous suggestions which no-longer offer as much value, but there’s plenty 
here to help you keep your pages and their resources as small as possible.

**Note:** Yeoman's [Grunt][12] and [Gulp][13] webapp generators include tasks
for optimizing images and concatenating and minifying HTML/CSS/JS. We feel that 
this provides a healthy baseline, but this post will cover tasks which go 
further.

## Compress & optimize images

The average web page is now over [1.5MB][14] in size, with images responsible
for the bulk of this. We aim to keep our image sizes as lean as possible to 
reduce the time it takes for a user to wait for that resource to load.

With the right balance of compression and formatting it's possible to still
ship images as a part of your page whilst minimizing load time as much as 
possible. This is really important for users on mobile with limited data plans 
or slow connections.

#### Grunt

*   [grunt-contrib-imagemin][15]
*   [grunt-imageoptim][16] (OSX only)

Why two tasks? Well, here’s an excellent [breakdown][17] of differences between
the two. Choose the one that is most suitable for you.

#### Gulp

At the time of writing there isn't a Gulp plugin available available for
ImageOptim just yet.

**Note:** Etsy found that just by [adding][18] 160KB of images to their pages
on mobile, their bounce rate increased by 12%. If you can't cut down on the 
images used in your pages, at least run them through an optimizer.

## Generate responsive images for the `<picture>` element

If you have a responsive site which is visually flexible on multiple devices,
you'll want a strategy to make images flexible too.

Serving unnecessarily large images to the browser can [impact][19] both
rendering and load performance, but these aren't the only metrics that can 
suffer when large images are shipped to the browser.

This is one reason we need responsive images, and it's great to see 
[srcset][20] - hopefully leading to a full implementation of `<picture>`

There are a number of Grunt tasks available that can help generate multi-
resolution images as part of your build process.

#### Grunt

In addition, if you need to just resize/normalize images that are large in
dimension, you can use[grunt-image-resize][21].

**Note:** Tim Kaldec's research into responsive images has [suggested][22] a
responsive images strategy could lead to savings of up to 72% on image weight. 
Whilst it is still early to opt for a spec-compatible, cross-browser approach to
responsive images the BBC and Guardian have been using Imager.js for this 
successfully.

## Minify SVG images

SVG files created with editors usually contain a large quantity of redundant
information (metadata, comments, hidden elements and so forth). This content can
be safely removed or converted to a more minimal form without imacting the final
SVG that's being rendered.

#### Grunt

#### Gulp

## Generate spritesheets

#### Grunt

#### Gulp

## Convert images to WebP

WebP is a recent image format that offers lossless and lossy compression for
images on the web. WebP lossless images are up to 26% smaller in size compared 
to PNGs and WebP lossy images are 25-34% smaller in size compared to JPEGs. That
's quite a saving and thankfully there exist tasks for encoding to WebP for both
Grunt and Gulp.

#### Grunt

#### Gulp

**Note:** This [test][23] from WebPageTest suggests that compared to JPEG, WebP
encoded images complete loading much quicker due to their smaller filesizes. The
Chrome Web Store[found][24] that switching to WebP saw a 30% average saving on
bytes, saving them several terabytes of bandwidth a day.

## Build SVG sprites with support for various browsers

### Grunt

### Gulp

We consider inlining images using Data URIs to now be an anti-pattern given
their[poor][25] performance on mobile.

## Minify CSS

Minification eliminates unnecessary space, line breaks, indendation and
characters in your files, which are generally unnecessary in production. 
Compacting down your HTML, CSS and JS can improve on parsing, execution and 
doanload times. For CSS specifically, we recommend:

#### Grunt

#### Gulp

## Remove unused CSS

In projects using CSS frameworks like Bootstrap, Foundation and so forth you
typically don’t use the entire kitchen-sink of styles available. Rather than 
shipping the full framework to production, use UnCSS to remove unused styles 
across your pages. Some developers have seen anything up to 85% savings in 
stylesheet filesize.

#### Grunt

#### Gulp

**Note:** A question developers regularly ask is whether UnCSS, or the process
of removing unused CSS can also work with styles injected into the page 
dynamically. The answer is 'yes'. UnCSS works in tandem with PhantomJS in order 
to make this happen. Devs have seen anything between[10][26]-[120KB][27] in
savings on a typical Bootrap page and UnCSS also works wel with other frameworks.

## Inline CSS

If the external CSS resources for a particular page are small, you can inline
those directly in your markup to save on additional requests. Inlining small CSS
in this way allows the browser to proceed with rendering the page.

#### Grunt

#### Gulp

## Combine media queries

This isn't a PageSpeed recommendation, but allows you to combine matching media
queries into a single media query definition. We've found it useful for handling
CSS generated by preprocessors which may use nested media queries.

#### Grunt

*   [grunt-combine-media-queries][28]

#### Gulp

*   [gulp-combine-media-queries][29]

## JavaScript

### Minify, compress JS

#### Grunt

*   [grunt-contrib-uglify][30]
*   [grunt-closure-compiler][31]

#### Gulp

*   [gulp-uglify][32]
*   [gulp-closure-compiler][33]

## RequireJS (optimization via r.js)

#### Grunt

#### Gulp

## Minify HTML

#### Grunt

#### Gulp

## Simple concatenation

#### Grunt

#### Gulp

## General compression for files/folders

#### Grunt

#### Gulp

## Zopfli compression

The Zopfli Compression Algorithm is an open-source compression library that
generates output typically 3–8% smaller compared to zlib at maximum compression.
It is best suited for apps where data is compressed just once and then sent over
the network lots of times.

#### Grunt

#### Gulp

**Note:** When Google Fonts switched to using Zopfli fonts were ~6% smaller on
average, and in some cases up to 15% smaller. According to[Ilya Grigorik][34],
for the case of Open Sans it was more than 10% smaller, translating to faster 
rendering and loading times. Zopfli images can however take longer to decode 
than JPGs so measure the metrics that matter to you when deciding whether to use
WebP.

## Inline Critical path CSS

The critical path represents the code and resources needed to render the "above
-the-fold" content in the page - i.e what your users will first see when they 
load up your page. PageSpeed recommends inlining your critical path CSS for 
improved performance. Whilst tools like[mod_pagespeed][35] are highly efficient
at achieving this, it’s more difficult to optimize for the critical path with 
other tooling.

You could probably use PhantomJS along with the above the fold scripts from 
[speedreport][36] to get an idea of what CSS is above the fold and can then
work on optimizing this manually.

**Note:** Paul Kinlan wrote a [bookmarklet][37] for estimating the above-the-
fold CSS for a page which is also worth checking out.

## Asset pipeline (auto-handle all optimizations)

On the ‘tools to keep an eye on’ list is [AssetGraph][38].

AssetGraph looks at projects as a set of graph problems where the nodes are
considered assets (HTML, CSS, Images, JS) and edges, the relationships between 
them (image tags, anchor tag, script tags etc
).

As AssetGraph can determine how project assets relate to each other it can
perform many of the common performance optimizations developers may want to 
achieve on their own automatically. This works particularly well on smaller 
projects and support for larger projects is being worked on.

#### Grunt

#### Gulp

Gulp users should just use AssetGraph directly.

## Benchmarking

The following benchmarking tasks are useful to integrate as a part of
Continuous Integration. Although the following are currently only available for 
Grunt, you can use[gulp-grunt][39] to run Grunt tasks from Gulp. We recommend
:

*   [grunt-pagespeed][40] - fantastic for automating checking your PageSpeed
    score as a part of CI.
   
*   [grunt-topcoat-telemetry][41] - get smoothness, load time and other stats
    from Telemetry as part of CI. This could help you set up a performance 
    benchmarking dashboard similar to the one used by
   [TopCoat][42] 
*   [grunt-wpt][43] - CI for WebPageTest scores
*   [grunt-phantomas][44] - response times for requests, responses, time to
    first image/CSS/JS, onDOMReady and more.
   

## Framework Optimization

#### Grunt

#### Gulp

*   [gulp-ngmin][45]
*   [gulp-react][46]
*   [gulp-vulcanize][47]

#### Misch

## Conclusions

Delays in performance have the potential to impact user engagement, experience
and revenue. Take time to experiment with the tasks available for performance 
optimization, find out what practical gains they can offer to your projects.

Visitors to your page will be happier as a result of a snappier experience and
a faster web is better for all.

~ Addy Osmani

*With thanks to Sindre Sorhus, Pascal Hartig and Stephen Sawchuk for their
review*

 [1]: img/tasks.1c7b.jpg
 [2]: https://twitter.com/igrigorik/status/300226402496704512

 [3]: http://www.smashingmagazine.com/2013/06/10/pinterest-paint-performance-case-study/
 [4]: https://speakerdeck.com/lara/design-for-performance
 [5]: https://developers.google.com/speed/docs/insights/rules
 [6]: https://developers.google.com/speed/pagespeed
 [7]: https://developers.google.com/speed/pagespeed/module
 [8]: https://developers.google.com/speed/pagespeed/module/download

 [9]: https://developers.google.com/speed/pagespeed/module/build_ngx_pagespeed_from_source
 [10]: http://gruntjs.com
 [11]: http://gulpjs.com
 [12]: http://github.com/yeoman/generator-webapp
 [13]: http://github.com/yeoman/generator-gulp-webapp

 [14]: http://httparchive.org/interesting.php?a=All&l=Aug%2015%202013#bytesperpage
 [15]: https://github.com/gruntjs/grunt-contrib-imagemin
 [16]: https://github.com/JamieMason/grunt-imageoptim
 [17]: http://jamiemason.github.io/ImageOptim-CLI

 [18]: http://programming.oreilly.com/2014/01/web-performance-is-user-experience.html
 [19]: http://timkadlec.com/2013/11/why-we-need-responsive-images-part-deux/

 [20]: http://blog.chromium.org/2014/02/chrome-34-responsive-images-and_9316.html?m=1
 [21]: https://www.npmjs.org/package/grunt-image-resize
 [22]: http://timkadlec.com/2013/06/why-we-need-responsive-images/

 [23]: http://www.webpagetest.org/video/compare.php?tests=130125_6N_KZA%2C130125_NH_KZ8&thumbSize=200&ival=100&end=full

 [24]: http://www.igvita.com/2013/03/07/faster-smaller-and-more-beautiful-web-with-webp/
 [25]: http://www.mobify.com/blog/data-uris-are-slow-on-mobile/
 [26]: https://twitter.com/efexen/status/438672726996574209
 [27]: https://twitter.com/thisbetom/status/432575411138998273
 [28]: https://npmjs.org/package/grunt-combine-media-queries
 [29]: https://www.npmjs.org/package/gulp-combine-media-queries
 [30]: https://github.com/gruntjs/grunt-contrib-uglify
 [31]: https://github.com/gmarty/grunt-closure-compiler
 [32]: https://github.com/terinjokes/gulp-uglify
 [33]: https://github.com/sindresorhus/gulp-closure-compiler
 [34]: https://plus.google.com/+IlyaGrigorik/posts/1sxencNkbNS
 [35]: https://code.google.com/p/modpagespeed/
 [36]: https://github.com/r3b/speedreport/

 [37]: http://addyosmani.com/blog/detecting-critical-above-the-fold-css-with-paul-kinlan-video/
 [38]: https://github.com/assetgraph/assetgraph
 [39]: https://npmjs.org/package/gulp-grunt
 [40]: https://npmjs.org/package/grunt-pagespeed
 [41]: https://github.com/topcoat/topcoat-grunt-telemetry
 [42]: http://bench.topcoat.io/
 [43]: https://npmjs.org/package/grunt-wpt
 [44]: https://www.npmjs.org/package/grunt-phantomas
 [45]: https://github.com/sindresorhus/gulp-ngmin
 [46]: https://github.com/sindresorhus/gulp-react
 [47]: https://github.com/sindresorhus/gulp-vulcanize