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

In my blog, you can notice the random image on the home page, the picture changes with each access.

## Random Picture Service

Needing a using to call directly inside my browser the daily picture provide by [Bing](https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=8).
### JSON Retrieve
```json
{
	"images": [{
		"startdate": "20161129",
		"fullstartdate": "201611290800",
		"enddate": "20161130",
		"url": "/az/hprichbg/rb/GrizzlyPeakSFVideo_EN-US11282703590_1920x1080.jpg",
		"urlbase": "/az/hprichbg/rb/GrizzlyPeakSFVideo_EN-US11282703590",
		"copyright": "San Francisco-Oakland Bay Bridge with San Francisco in the background, California (© Engel Ching/Alamy)",
		"copyrightlink": "http://www.bing.com/search?q=san+francisco-oakland+bay+bridge&form=hpcapt&filters=HpDate:%2220161129_0800%22",
		"wp": false,
		"hsh": "35dd89dd65f7f7ba97fb1b61fd9d2ace",
		"drk": 1,
		"top": 1,
		"bot": 1,
		"hs": []
	}, ...	
	{
		"startdate": "20161122",
		"fullstartdate": "201611220800",
		"enddate": "20161123",
		"url": "/az/hprichbg/rb/ThailandWaterfall_EN-US7044305410_1920x1080.jpg",
		"urlbase": "/az/hprichbg/rb/ThailandWaterfall_EN-US7044305410",
		"copyright": "Erawan National Park, Kanchanaburi Province, Thailand (© Banana Republic Images/Shutterstock)",
		"copyrightlink": "http://www.bing.com/search?q=Erawan+National+Park&form=hpcapt&filters=HpDate:%2220161122_0800%22",
		"wp": false,
		"hsh": "0e5cc7555e82e922359b3cdb4dc68900",
		"drk": 1,
		"top": 1,
		"bot": 1,
		"hs": []
	}],
	"tooltips": {
		"loading": "Loading...",
		"previous": "Previous image",
		"next": "Next image",
		"walle": "This image is not available to download as wallpaper.",
		"walls": "Download this image. Use of this image is restricted to wallpaper only."
	}
}
```

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
        '&url=' + encodeURIComponent('https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=8') +
        '&format=json&callback=?';
    $.getJSON(url, function(result) {
        var random = Math.round(Math.random() * 8 - 0.5);
        var img = result.query.results.json.images[random];
        var $dailyPictureContainer = $('#daily_picture_container');
        $dailyPictureContainer.css("background-image", "url(//www.bing.com" + img.urlbase + "_800x600.jpg)");
        $dailyPictureContainer.attr("title",  img.copyright);
        $dailyPictureContainer.on('click', function() {
            window.open(img.copyrightlink,'_blank');
        });
    });
```

And it's work :-)

![The sample is working](/images/JavaScript-How-to-call-a-remote-service-with-using-a-JSONP-Proxy-2.png "The sample work's :-)")

## References
- [YQL](https://developer.yahoo.com/yql/)
- [CORS Header](https://www.html5rocks.com/en/tutorials/cors/) 
- [Bing daily picture](https://www.bing.com/HPImageArchive.aspx?format=js&idx=0&n=1)