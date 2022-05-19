

## Without Proxy

```js
// create a image DOM element
// append image DOM to html body
// return a function which
  // 1. with img url param
  // 2. assign url param to image DOM src

const myImage = (function() {
  const img = document.createElement('img');
  document.body.appendChild(img);

  return function(imgUrl) {
    img.src = imgUrl;
  };
})();


myImage('largePic.png');
```

&nbsp;

## with Virtual Proxy

```js
const myImage = (function() {
  const image = document.createElement('img');
  document.body.appendChild(image);

  return function(imgUrl) {
    image.src = imgUrl
  };
})();


// create a proxy function to assign img url
// create a image object
// only when image loaded successfully assign url to myImage
// return a function which
  // 1. accept img url param
  // 2. set a loading imgUrl to myImage
  // 3. set image object src prop to  url param

const proxyImage = (function() {
  const image = new Image();

  image.onload = function() {
    myImage(this.src);
  }

  return function(imgUrl) {
    myImage('loading.gif');
    image.src = imgUrl;
  };
})();

proxyImage('largePic.png');
```