---
title: Integrating Sitecore with Azure CDN – Part 1
date: 2016-03-02 18:56:56
tags: ['Azure', 'CDN', 'Sitecore']
excerpt: "This will be the first in a multiple part blog series in which we discuss the various steps involved and option available while integrating a Sitecore with Azure CDN. In this post we will discuss what Sitecore has out of the box."
---

This will be the first in a multiple part blog series in which we discuss the various steps involved and option available while integrating a Sitecore with Azure CDN. In this post we will discuss what Sitecore has out of the box.

#### Prerequisites ####
1. 

#### Media.MediaLinkServerUrl ####

Out of the box Sitecore comes with a setting Media.MediaLinkServerUrl which can be used to set to base URL of your CDN

''' xml
<!--  MEDIA - MEDIA LINK SERVER URL
            The server URL to use when Sitecore generates media links and when Media.AlwaysIncludeServerUrl is set to true. This is typically
            used when all media is served from one or more dedicated instances or when your solution is configured to store Sitecore media on
            a content delivery network. 
            The URL must use this format: <protocol>://<hostname>, for example http://example.com 
            If the value is not set, the URL of the current server will be used.
            Default value: ""
      -->
    <setting name="Media.MediaLinkServerUrl" value="" />
'

Will this work now? can you hear me now?
