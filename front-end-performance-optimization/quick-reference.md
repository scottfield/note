###Messure Performance with RAIL Principle
###Text Content Optimization
- Minify Your Code(e.g. use to gulp minify)
- Compress Text Resources(e.g. enable server Gzip function)
- avoid to use large library only pick function what you need(e.g.[YOU MIGHT NOT NEED JQUERY](http://youmightnotneedjquery.com))
###Graphical Content Optimization
- Remove Unnecessary Images(e.g. replace with css implementation)
- Choose Appropriate Image Types(e.g. prefer jpg to png format)
- Remove Image Metadata()
- Resize Images(e.g. choose a suitable image size according to use intention)
- Reduce image quality(e.g. use [XNConvert](https://www.xnview.com/en/xnconvert/) to batch process image)
- Compress Images(e.g. [some useful tools to achieve this goal](http://enviragallery.com/9-best-free-image-optimization-tools-for-image-compression/))
- Replace Animated GIFs with Video
###Some Useful metric tools
- Lighthouse
- Google PageSpeed Insights
- WebPageTest
###Reduce HTTP Request
- Combine Text Resources(e.g. combine small css ,js file to one)
- Combine Graphical Resources(e.g. css spirit technical)
- JavaScript Position and Inline Push(e.g. put noncritical script before ending body tag)
- Use HTTP Cache(e.g. cache static resource)