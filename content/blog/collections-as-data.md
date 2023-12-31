---
title: Using Digital Collections as Data
date: May 5, 2017
minutes: 3 minute read
layout: post
url: collections-as-data
summary: It's all about reducing barriers to access
---

# Using Digital Collections as Data

Collections as Data is a phrase bandied about the internet, and one that has recently grabbed our attention here at Wayne State. As far as I understand it, it means providing access to online digital library collections in a way that facilitates programmatic research. Here at Wayne State, we have been busy redesigning our digital collections platform, both its front-end display as well as the back-end data that powers the website (its API). In doing so, we couldn’t help but be a bit inspired by the collections as data movement and see if we could work toward tilting our collections to harness some of those concepts.

A bit of info on how our digital collections work. The front-end display (aka website) show alls the public-available image and digital resources from our repository. This data (metadata, rights statements, links to images, etc) all comes from our API. When a page loads, it queries the API for the associated data and after a bit of arranging, loads the page. These are two separate systems, each with unique ways of working. Users are free to use the front-end display to browse normally or to use the API to see all of our metadata ins our repository; the problem is that we had different ways of interacting with each. You might type in [http://OUR_URL/item/ITEM_ID](http://OUR_URL/item/ITEM_ID) to see the web page for an item record and [http://OUR_URL/WSUAPI/?functions[]=singleObjectPackage&PID=ITEM_ID](http://OUR_URL/WSUAPI/?functions[]=singleObjectPackage&PID=ITEM_ID) to see the API data for that same item. For two systems that are tied together, this is not very intuitive for anyone. And, if you are into the idea of Collections as Data, you have added a confusing layer for anyone who wants to use the larger metadata store underneath the digital collections. We had the idea that people who were interested in the API (and doing some programmatic research with our collections) would first navigate the website and get familiar with its content then switch to the API. Unfortunately, with the current setup, they would have to learn a completely new way of navigating with the API. This is where content-negotiation comes in.

As part of the HTTP standard ([https://en.wikipedia.org/wiki/Content_negotiation](https://en.wikipedia.org/wiki/Content_negotiation)), content negotiation is the ability to ask for different representations of the same information by specifying its content-type. This could be something as simple as asking for HTML (text/html), PDF (application/pdf), or even a structured data like JSON (application/json). Remember that I said earlier that we were rebuilding our API and our front-end display. We had determined that, regardless of the system used--the API or the website--we were basically showing the same information to people just in different display formats. Therefore, it made a lot of sense to make the systems mirror each other. Now, to be clear, the ultimate use of content-negotiation might have been to merge the two. First, you type in the url, for example, [http://OUR_URL/item/ITEM_ID](http://OUR_URL/item/ITEM_ID). Next, if you wanted structured data (normally available from an API), you'd ask for JSON; if you wanted a webpage with arranged data, you'd ask for HTML, using that same url. We're unfortunately not there yet. We need two different systems because they accomplish more than just what I've described (aka, there's complications). But, a nice middle ground, and one to gets us closer to providing researchers accesss to our collections as data, is to make sure the API and the front-end do the same thing with the same URL patterns.

Therefore, we have ended up with this: our API and our front-end are still two distinct systems. But, you can get the same information from them by using the same url pattern. If you want the api, you'll include the word api in the url, and if you want the HTML web page, you'll remove it. [http://OUR_URL/api/item/ITEM_ID](http://OUR_URL/api/item/ITEM_ID) vs [http://OUR_URL/item/ITEM_ID](http://OUR_URL/item/ITEM_ID).

We're currently working to put this redesign into production. We hope that this will get us that much closer to making our digital collections more transparent and usable to end users looking for the data that powers it all. Look for a new blog post about this new system after it debuts!


More resources:
[http://digitalpreservation.gov/meetings/dcs16/AsDataExecutiveSummary_final.pdf](http://digitalpreservation.gov/meetings/dcs16/AsDataExecutiveSummary_final.pdf)

[http://digitalpreservation.gov/meetings/dcs16/tpadilla_OnaCollectionsasDataImperative_final.pdf](http://digitalpreservation.gov/meetings/dcs16/tpadilla_OnaCollectionsasDataImperative_final.pdf)