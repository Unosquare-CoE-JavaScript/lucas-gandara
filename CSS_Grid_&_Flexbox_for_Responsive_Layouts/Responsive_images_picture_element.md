# CSS Grid & Flexbox for Responsive Layouts

## Responsive Images & Picture element
The _prime directive_ is to only load one image even if many are specified. Try to always avoid this:
```html
<div class="fakeResponsive">
  <img src="tiny.jpg" class="tiny">
  <img src="big.jpg" class="big">
</div>
<style>
  @media (max-width: 200px) {
    .big { display: none; }
  }

  @media (min-width: 501px) {
    .tiny { display: none; }
  }
</style>
```
An alternative you may think of if doing like:
```html
<img src="big.jpg" alt="big image">

<style>
  img {
    width: 100%;
    max-width: 800px;
  }
</style> 
```
This would make sure your picture to always fit to it's container and over certain point avoid it to grow any more. But there is one problem which is that the same image is going to be loaded regardless the viewpoint, this is not performant.

### Art direction
_Art direction_ shows different images on different display sizes. A responsive image loads different sizes of the same image. Art direction takes this a step further and loads completely different images depending on the display. Use art direction to improve visual presentation. Art direction's benefits are purely aesthetic; it provides no performance benefit over responsive images.

Art direction uses the `<picture>`, `<source>`, and `<img>` tags.

`picture` tag provides a wrapper for zero or more `source` tags and one `<img>` tag. The `<source>` tag provides a media source and the `<img` tag provides a fallback. Consider:
```html
<picture>
  <source media="(max-width: 600px)" srcset="flower-square.jpg">
  <source media="(max-width: 1023px)" srcset="flower-rectangle.jpg">
  <source media="(min-width: 1024px)" srcset="flower-large.jpg">
  <img src="flower-large.jpg">
    </picture>
```
Another option is to embed everything in a `img` tag leveraging the attribute `size` like so:
```html
<img
  srcset="large.jpg 1024w,
          medium.jpg 640w,
          small.jpg 320w"

  sizes= "(min-width: 36em) 33.3vw, 100vw"

  alt="A rad wolf">
```
The `srcset` attribute now stands for file names and width of images in pixels, other units are not accepted. The `size` attribute is the size of the whole web page. So what it means is that if the _min-width_ is at least `36em`, display the image at 33.3vw, otherwise display at 100vw.