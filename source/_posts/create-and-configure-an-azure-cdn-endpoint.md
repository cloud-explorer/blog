---
title: Create and Configure an Azure CDN Endpoint
date: 2016-03-01 20:37:46
tags: ["CDN", "Azure"]
categories: "How to"
excerpt: "In my last post we discussed the benefits of delivering your site’s content through a Content Delivery Network (CDN). Azure CDN as I had mentioned is gaining popularity. If you are in the Microsoft stack and are already using Azure, then it’s CDN offering is an excellent choice. In this post we will look at creating and configuring an Azure CDN endpoint to be used with your site."
---

In my last post we discussed the benefits of delivering your site’s content through a Content Delivery Network (CDN). Azure CDN as I had mentioned is gaining popularity. If you are in the Microsoft stack and are already using Azure, then it’s CDN offering is an excellent choice. In this post we will look at creating and configuring an Azure CDN endpoint to be used with your site.

#### Creating a CDN Profile

1.  Go to the Azure Management Portal at <http://portal.azure.com>

2.  On the resources blade on the left, click on “New”

3.  On the New blade select Media + CDN, then select CDN.

4.  On the New CDN profile blade, fill in the name of the profile. A CDN Profile is bucket which may contain one or more CDN endpoint. So choose a name that will make sense for your business
	
	{% asset_img "image1.jpeg" "Creating an Azure CDN Profile" %}
   
5.  Choose a location. This is the location of the data center where you profile information will be stored. This is not the POP location.

6.  Choose an existing resource group or create a new one. Typically, a resource group is comprised of resources related to a specific application. For example, you can choose to group the web app, database and CDN for the website under the same resource group.

7.  Choose either the Standard S1 or Premium P1 as the pricing tier. A detailed list of features for each of these tier can be found on the Azure CDN’s site <https://azure.microsoft.com/en-us/services/cdn/>

8.  Select the Azure Subscription you want to create this under and press the Create button.

9.  This will kick-off the request for the creation of the CDN profile. You will be notified when the CDN profile creation successfully completes.

    {% asset_img "image2.gif" "CDN Profile creationg notification" %}

Now that you have a CDN profile it is time to create a CDN endpoint.


#### Creating a CDN Endpoint.

1.  Under the newly created CDN profile, click on the Add Endpoint button

    {% asset_img "image3.png" "Create CDN Endpoint" %}

2.  Enter a name for the endpoint. This has to be a unique name across all Azure CDN endpoints. When created your CDN endpoint will be accessible at http://&lt;endpointname&gt;.azureedge.net/

3.  Choose an origin type and origin hostname. Your choices are

    1.  *Storage* and then select an existing blob storage container (Container needs to be publically accessible) from your subscription

    2.  *Cloud Service* and the select a website deployed on a VM or a Cloud Service (IaaS)

    3.  *WebApp* and select a website deployed as PaaS, or

    4.  *Custom Origin* and select custom origin URL or IP address. This can point to any publically accessible URL or IP Address.

4.  If the content to be retrieved is hosted under a specific directory path, specify the Origin Path. This is optional and need not be filled in if it is not applicable.

5.  Then enter the host header the needs to be sent to the origin with each request. If there are more than one virtual domains hosted on a physical server, the hostname and IP address from the host header can used by the origin server to identify the incoming request. If you leave this blank, the request hostname determines this value.

6.  Select the HTTP protocols you want the CDN support and their port numbers.

7.  Click Add to kick-off the request for creation of this endpoint.

8.  Once the endpoint is created it will appear in a list under the CDN profile blade

	{% asset_img "image4.png" "CDN endpoint creation. See the end points listed on the CDN profile blade" %}


#### Configuring the Endpoint

1.  On the CDN profile page, click on the endpoint to launch the Endpoint blade.

2.  Click Configure

3.  If you desire to turn to turn on compression for files, toggle the compression button to on. Optionally you can add or remove the content types to be compressed. By default, azure list all static resource content types that are generally compressed for content delivery.

4.  Then you can select the query string caching behavior. The choices are to

    1.  Ignore query string when caching.

    2.  To bypass caching for URLs that contain query strings.

    3.  To cache every request with a unique URL

5.  You can also change the protocol, the origin host header and the origin path on this blade

    {% asset_img "image5.png" "CDN endpoint configuration" %}


{% alert warning %}
<br>
Please note that the endpoint will not be available for use immediately. It may take up to 90 minutes for the registration to propagate through the CDN network. If you try to access the CDN endpoint immediately, you will get a 404 – NOT FOUND response until the content becomes available on the CDN
{% endalert %}

