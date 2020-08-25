A way to automate unliking all of your old tweets.

Step 1: Go to your Twitter profile page and click 'likes', or visit the URL:
twitter.com/username/likes

Step 2: Open the Chrome console (F12), and type in the following command:

setInterval(function(){ var divs = document.getElementsByTagName('div') 
var arr = Array.prototype.slice.call( divs) 
var hearts = arr.filter(x => x.getAttribute('data-testid') == 'unlike') 
hearts.forEach(h => h.click()) 
window.scrollTo(0, document.body.scrollHeight); },1000); 
