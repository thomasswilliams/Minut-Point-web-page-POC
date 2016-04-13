# Minut-Point-web-page-POC
A proof-of-concept to chart Minut Point data, retrieved using the Point REST API, on a web page.

## Why?
Recently I received a device that I Kickstarted back in November 2014 - [Point by Minut](https://www.minut.com/index.html)

The Point device is simple and efficient and does exactly what it says on the box - collects temperature, sound level, and humidity readings, displaying them in charts on an iOS (and soon Android) app.

Interestingly, the Minut web site at https://www.minut.com/support/ states: 
> IS THERE A WEB INTERFACE? No, we're considering it for the future, but it's not currently planned...

I started looking at how my Point device talks to the Point servers to see if I could replicate it on a web page. This project - a single web page - is the result.

## How does it work?
This single web page is (in my mind) the bare minimum required to display charts on a web page from my Point device.

Anyone who wants to get this single web page working should review the following:

1. The web page can't be served using the `file://` protocol; it must be hosted by a web server. If you are running OSX, this is as simple as:
  * download the web page to a folder
  * open a terminal window at the folder, and run: `python -m SimpleHTTPServer 8000`
  * in your web browser, browse to http://localhost:8000/

2. Your Point username and password will be passed as clear text. If you are not comfortable with this, don't proceed any further.

3. Your Point data will be passing through a 3rd-party web site that is not under my control. As mentioned above, in the interests of bare minimum required, I re-used an existing 3rd-party web site to forward requests to the Point API and set the correct CORS headers. There are most certainly other, better ways of doing this. The 3rd-party web site is http://thingproxy.freeboard.io (freeboard's thingproxy, see Git repo at https://github.com/Freeboard/thingproxy).

5. The web page depends on content delivery network for libraries like jQuery, Bootstrap and Font Awesome, and on Google for the Google charts library. This means that while the web page may work right now, things could break in future - and I won't be maintaining this web page to fix them.

6. I'm not an expert programmer or ace designer so there are bugs and undiscovered issues with the web page. I took a lot of shortcuts. There's not much original work here either - see comments in the code for detailed source attribution. Oh, and I used Bootstrap too.

7. The web page does not talk to your Point. It talks to the Point servers using the officially-documented REST API. The REST API may change or break in future, most likely breaking this web page.

8. **I do not support or maintain this web page/project.** It was written by me as a proof of concept for my use only and is shared because, well, I felt like it. As at April 2016, the web page works for me; beyond that, use at your own risk. There are better/faster/simpler ways to display charts on a web page from my Point device - for instance, https://www.npmjs.com/package/point-cli or https://github.com/reoring/point_client.

9. The code behind the web page is open source, licensed under the MIT license - I hope someone else makes good use of it!

## How do I set it up? 
Now that I have the grim warnings out of the way, below is how I've set it up on my computer, running OSX:
- download the web page to a folder 
- the web page should be named `index.html`
- open a terminal window at the folder, and run: `python -m SimpleHTTPServer 8000`
- in your web browser, browse to http://localhost:8000/
- you should see the web page you downloaded; click the button labelled "Log in"
- enter your Point user name and password and click "Get my devices" 
- if all went well, after about a minute the 3 graphs will be populated with today's data from your Point device 
  * I've only got one Point device so I only tested the web page with one Point device 
  * I limited the data retrieved to today only 

## Credits
This web page is based on the following:
* the Point REST API, documented at https://api.minut.com/draft1/docs
* Google charts library, documented at https://google-developers.appspot.com/chart/interactive/docs/gallery/linechart
* Bootstrap 4 docs at http://v4-alpha.getbootstrap.com/getting-started/introduction/
* http://www.desert-home.com/2013/07/using-google-charts-api-with-xively.html and http://www.santarosa.edu/~jperetz/projects/ajax-json/ - two samples of getting Google charts working with JSON data 
* free [Burp Proxy](https://portswigger.net/burp/proxy.html) which helpfully generated `curl` commands for testing, see tutorial at https://support.portswigger.net/customer/portal/articles/1841108-configuring-an-ios-device-to-work-with-burp
* "stacks" of jQuery/Bootstrap answers on Stack Overflow 
