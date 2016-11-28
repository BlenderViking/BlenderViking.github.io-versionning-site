---
title: '[JAVASCRIPT] How to call a remote service with using a JSONP Proxy'
date: 2016-11-27 21:41:13
categories:
 - Development
tags: 
 - JavaScript
 - JSONP
 - CORS Request
thumbnail: '/images/JavaScript-How-to-call-a-remote-service-with-using-a-JSONP-Proxy.png'
---

Hi,

Needing a using to call directly inside my browser the daily picture provide by [Bing](https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1).

## CORS Header
I discovered that it didn't work directly by Ajax request because Microsoft doesn't have add [CORS Header](https://www.html5rocks.com/en/tutorials/cors/) :-/

![CORS](/images/JavaScript-How-to-call-a-remote-service-with-using-a-JSONP-Proxy-1.png "The CORS error")

## JSONP Proxy service

So we needing a solution for resolve the _**Cross-Origin Request Blocked**_ on my browser

```
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1. (Reason: CORS header ‘Access-Control-Allow-Origin’ missing).
```

The solution for retrieve the expected json is use a public _**JSONP Proxy service**_ like [yql](https://developer.yahoo.com/yql/) (provide by Yahoo).

## Code sample
```javascript
    var url = '//query.yahooapis.com/v1/public/yql' + 
        '?q=' + encodeURIComponent('select * from json where url=@url') +
        '&url=' + encodeURIComponent('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1') +
        '&format=json&callback=?';
    $.getJSON(url, function(result) {
        $('#daily_picture_container').css("background-image", "url(//www.bing.com" + result.query.results.json.images.url + ")");
    });
```

And it's work :-)

![The sample is working](/images/JavaScript-How-to-call-a-remote-service-with-using-a-JSONP-Proxy-2.png "The sample work's :-)")

## References
- [YQL](https://developer.yahoo.com/yql/)
- [CORS Header](https://www.html5rocks.com/en/tutorials/cors/) 
- [Bing daily picture](https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1)