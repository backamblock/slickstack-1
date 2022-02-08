# What is this Branch?

I will track my changes here that i do not want to be merged into the littlebizzy/slickstack repo as it conflicts with the original idea and interests of littlebizzy.

Littlebizzys approach is to make it as stable and secure as possible, that means get rid of all bloatware and stuff that should usually be done at a server level like caching and backups... Which is a good thing as it enables hosting environments to offer reliable services!

But it also means that some exclusions are overkill for me, i don't really care if i double the disk space used by cache as i have 1GB site and 20GB storage. Also i really miss the snappy UX with Browser-Cache.

Now here comes the thing. Nginx caching is nice and fast for static sites but when you put WP-Rocket on top of it, it flies!

## Let me explain:
* Cloudflare adds Latency (TTFB) anywhere from 50-200ms 
* CDN is not needed for only locally relevant pages like a barber or restaurant
* The Browser-Caching of CF is better than nothing, but nowhere near good
* SlickStack has no css/js minify, Lazyload, image compression or crawler by default
* SlickStack caching does ONLY work on static sites by design, which makes sense

## To the moon
* here is where WP-Rocket comes into play...
* it adds Minification, GOOD Browser-Cache, Cache for logged in users
* and Cache for Users with items in the cart
* the lazy loading works as expected without layout shifts
* did i mention the wonderful link-preloading?
* combine it with image compression and webp and off you go
### And my personal #1 Reason: it works with Onlineshops!
Faster checkout time means less time to rethink the buying decision!  

These add bloat, yes! But when everything is cached and nginx takes the guest visitors, that doesn't really matter. In Cloudflare non-proxy mode i have a TTFB of 60-80ms without CDN, with proxy or CDN it is around 100-150ms

I did not notice any conflicts with ss-config in terms of reliability. it just doubles the caching. i will share my settings in another file sometime soon.

____
# Speed Comparison  
* look at First Byte, Document complete and Fully loaded
* you see first byte with wp-rocket is late because not much is loaded at all
* webpagetest.org settings: Chrome, FIOS (20/5mbit) connection, 9 runs, first and repeat view, no video
* NOT nearest server because always full. i choose Amsterdam instead of Frankfurt.
* VPS is Hetzner 2c/2gb with AMD (current lineup 2022)

* pure slickstack with Kadence theme, woocommerce and stock "Outdoor Shop" Starter site, no other changes  
![image](https://user-images.githubusercontent.com/20801141/150625991-04a8b64b-b349-415a-81e0-cc91a7c913b2.png)


* now with wp-rocket and all settings, WITHOUT image compression, still WITH Cloudflare Proxymode  
![image](https://user-images.githubusercontent.com/20801141/150626090-af03c681-82dc-4867-81b6-be4a1f4f2447.png)


* now + wp-rocket + image compression + webP + cloudflare proxy
* sadly, webpagetest has updated to new design which does not show all values anymore :/ so no nice picture will ever come here
* i can tell you, it is VERY fast tho. google pagespeed shows 97-99 mobile between tests, 100 desktop no matter what
* fully loaded times for first visit are around 1 second for desktop which would compare to the fully loaded on WPT before
* since this is obviously fast enough, i kept CF proxy mode as with these loading times, 50ms is not really worth the loss of CF
* here is at least a picture proof of google pagespeed :)
![image](https://user-images.githubusercontent.com/20801141/152898836-b4a3f49a-3478-4edd-b6fd-2ecfea138359.png)


* comparison: maxed out litespeed enterprise + no wp-rocket, with image compression and webP, with QUIC.cloud CDN
![image](https://user-images.githubusercontent.com/20801141/150626076-90029c69-6604-45a2-b582-bff20c2c538e.png)

____
## Things to keep in mind:
* you need to manually flush WP-Rocket
* after that, flush slickstack caches
* after that, start wp-rocket preload
____
## Things changed over original:
* commented wp-rocket in blacklist
* commented imagify in blacklist
* ...
