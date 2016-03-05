---
title: What is a cdn and why do you need to care?
date: 2016-02-23 
tags: ['CDN', 'Web Optimization']
categories: Information
excerpt: "The success of the websites we build is heavily influenced by its latency: the time it takes for the hosting server to receive, process, and deliver a request for a page (html, images, js, css, etc.). The latency a site visitor experiences is largely based on how far he/she is from the server and is compounded by the size and number of resources on the page. In this post we will explore the latency experienced by a website hosted in a single location, with a large international user-base experiences and how the addition of a Content Delivery Network (CDN) can drastically improve the situation."
---

The success of the websites we build is heavily influenced by its latency: the time it takes for the hosting server to receive, process, and deliver a request for a page (html, images, js, css, etc.). The latency a site visitor experiences is largely based on how far he/she is from the server and is compounded by the size and number of resources on the page. In this post we will explore the latency experienced by a website hosted in a single location, with a large international user-base experiences and how the addition of a Content Delivery Network (CDN) can drastically improve the situation. 

#### Scenario 1: No CDN

{% asset_img "image1.jpg" "No CDN" %}

1.	The user requests a resource on your website through the internet
2.	The request bounces back and forth between different networks on the internet before reaching the origin server (Red lines in the diagram)
3.	The origin server processes the request and its response again travels through the internet taking several hops before reaching the user’s HTTP client (Black lines in the diagram). Even for the most optimized website, this “network hop” dance negatively impacts latency by several seconds.


According to [this](http://loadstorm.com/2014/04/infographic-web-performance-impacts-conversion-rates/) 2014 study by LoadStorm, **25%** of users will abandon a website that takes more than 4 seconds to load, **75%** of mobile users will quit after 5 seconds. The worst part is almost **50%** of the users will never return to a poorly performing website. This is the exact problem a Content Delivery Network (CDN) tries to solve by caching static resources in geographically distributed edge servers.

{% alert success %}
<br/>

<strong>Origin Server: </strong> As the name suggests, this is the server(s) where the customer host their content.
<br/>
<strong>POP: </strong>POP stands for Point Of Presence. This is also sometime referred to as the <strong>CDN Edge Network</strong>. These are the geographical locations where CDN edge servers are located

{% endalert %}

#### Scenario 2: With CDN - First Request (Origin Pull)

{% asset_img "image2.jpg" "First Request Scenario" %}


1.	The user requests a resource on your website through the internet
2.	The request reaches the “closest” POP location to the user (POP-U in diagram). Close here refers to network closeness and not necessarily geographical closeness.
3.	Since the edge network is aware of its locations, POP-U requests the resource from the POP closest to the origin server (POP-O in diagram). This request will travel from POP-U to POP-O using the most optimal route available.
4.	POP-O request the resource from the origin, caches the response and communicates it back to POP-U.
5.	POP-U caches the response and communicates it back to the user


#### Scenario 3: With CDN - Subsequent Request

{% asset_img "image3.jpg" "Subsequent Requests Scenario" %}

1.  The user requests a resource on your website through the internet
2.  The request reaches the “closest” POP location to the user. If a cached version of the resource is available, it is communicated back to the user. If a cached version was not found, the resource will be pulled from the origin (scenario 2).
With the CDN Edge Network, the number of “hops” required to pull a resource from the origin server is reduced significantly. Once the resource is cached, it is directly served from a POP that is “closest” to the requester. This dramatically improves the latency of the website.

#### Scenario 4: With CDN – Request from a different POP location

{% asset_img "image4.jpg" "Request from a different POP location Scenario" %}

1.  The user requests a resource on your website through the internet
2.  Just like in scenario 2 the POP closest to the user (POP-U) receives the request and forward it directly to the POP (POP-O) closest to the origin.
3.  If POP-O has a cached version of the resource, it responds back **without** requesting it from the origin. If not, it performs an origin pull.

As can be seen the introduction of a CDN allows the website to respond to unpredictable user loads in a predictable manner. Content is always pulled and cached by the POP closest to the origin. As and when user load increases, the load on the CDN edge network increases never affecting the origin server.

#### Is a CDN must for every website?

It depends on the purpose and user distribution of the website. A CDN may not make much difference in the following scenarios

1.  If the content of the website is very dynamic with very little chance of reuse.

2.  If the majority of the users are in a location very close to the origin server. In this case the origin may be better suited to deliver the content in the most optimal route.

There are several CDN offerings available such as Akamai, Amazon CloudFront, Azure, MaxCDN, etc. Clearly Akamai and Amazon are industry leader but with some the new functionalities and capabilities announced in late 2015, Azure CDN has become a serious competitor for the big 2. Azure CDN has no upfront-costs, no termination fees and you only pay for what you use. RESTful APIs are available to manage CDN Configuration (create/update/delete) and CDN Endpoints (purge, preload, compression, querystring). In my next post we will cover commissioning, configuring an Azure CDN Endpoint to be used with your website.
