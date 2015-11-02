# phantomjs-html

The main goal of this project is to enable you to **retrieve the HTML output of URLs**. It also gives you some **ExpressJS middlewares and methods to implement SEO** for single page apps out of that.

## Development state

This project is just a born baby. I tried the nice [prerender](https://github.com/prerender/prerender) but found that one too complex for such a simple task. It also made our server crash a lot... So I made this, which is **a lot simpler**, **surely slower** because it dosen't keep multiple instances of PhantomJS running.


## How to use
```
var phantomjsHtml = require('phantomjs-html');
```

## Exemples :


### 1. Get HTML from an URL

```
phantomjsHtml.getHTML('https://google.com', function(err, output){
  if(err){
    console.log('ERROR', err);
  } else {
    console.log('SUCCESS', output);
  }
});
```
```


### 1. Use the ExpressJS SEO middleware

This middleware need to be used before any routing is done. It will detect if the current request is made from a crawler using the `user-agent` and `_escaped_fragment_`. If a crawler is detected, it will return a PhantomJS rendering of the page that crawlers will adore.

```
// output PhantomJS render of pages if the request is made by a crawler
app.use(phantomjsHtml.middleware.SEO);
```


### 3. delaying the PhantomJS output

In single pages apps, there is often JavaScript executed after the page has loaded to load or display datas. You can tell this module to wait until your app is ready like so :

In the `<head>` section of your HTML pages :
```
<script type="text/javascript">
  window.phantomjsHtmlReady = false;
</script>
```

And when your code is ready, just set `phantomjsHtmlReady` to true.

```
window.phantomjsHtmlReady = true;
```