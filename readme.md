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
* combine it with imagify (free plan) for set-and-forget image compression and webp
### And my personal #1 Reason: it works with Onlineshops!
Faster checkout time means less time to rethink the buying decision!  

These add bloat, yes! But when everything is cached and nginx takes the guest visitors, that doesn't really matter. In Cloudflare non-proxy mode i have a TTFB of 60-80ms without CDN, with proxy or CDN it is around 100-150ms

I did not notice any conflicts with ss-config in terms of reliability. it just doubles the caching. i will share my settings in another file sometime soon.

# Speed Comparison (look at First Byte, Document complete and Fully loaded)
* pure slickstack with Kadence theme, woocommerce and stock "Outdoor Shop" Starter site, no other changes
![image](https://user-images.githubusercontent.com/20801141/150625991-04a8b64b-b349-415a-81e0-cc91a7c913b2.png)


* slickstack with wp-rocket and all settings, WITHOUT imagify, WITH Cloudflare Proxymode
![image](https://user-images.githubusercontent.com/20801141/150626090-af03c681-82dc-4867-81b6-be4a1f4f2447.png)


* slickstack + wp-rocket + imagify + cloudflare proxy


* slickstack + wp-rocket + imagify + cloudflare no-proxy


* comparison: maxed out litespeed enterprise + no wp-rocket, no imagify, no CDN
![image](https://user-images.githubusercontent.com/20801141/150626076-90029c69-6604-45a2-b582-bff20c2c538e.png)


## Things changed:
* commented wp-rocket in blacklist
* commented imagify in blacklist
* ...
