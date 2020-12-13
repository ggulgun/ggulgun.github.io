---
title: "iOS Biometric Login Authentication Bypass"
layout: post
---

# Introduction
2020-05-19
<br />

While I was recently hunting on a promising mobile target, I discovered iOS Biometric Login Auhentication Bypass. The application uses Touch ID for login authentication process. This includes both the older TouchID as well as newer FaceID features, collectively referred to as biometrics. One of features objection has is the ability to 'bypass' iOS biometrics. This includes both the older TouchID as well as newer FaceID features, collectively referred to as biometrics. To some, biometrics are seen as the pinnacle of authentication.
<br />

## Impact:

Attackers can gain access to account, or just one admin account to compromise the system. Depending on the domain of the application, this may allow money laundering, social security fraud, and identity theft, or disclosure of legally protected sensitive information. Objection Biometrics Bypass can be used to bypass LocalAuthentication. Objection uses Frida to instrument the evaluatePolicy function so that it returns True even if authentication was not successfully performed.

## Vulnerability:

In the application, Touch ID authentication is enabled. After clicking "Touch ID" selection, application login process go through with Touch ID. 

### Proof Of Concept

For bypass progress, Frida and Objection used. 

The application can enumerate by the following command.

{% highlight html %}
frida-ps -Ua
{% endhighlight %}

For bypassing, as I told you before Objection tool is used. POC is completed with the following commands.

{% highlight html %}
Enter -  objection --gadget "applicationName" explore
Next, Enter ios ui biometrics_bypass
{% endhighlight %}


## Re-mediation

Security needs to be part of the developing process from the beginning. That is the only way to ensure nothing can be abused in a way that was not thought about during developing, as those kinds of vulnerabilities are hard to look for afterwards. For prevention, developers must apply the following ways for authentication. Unlike macOS and Android, iOS currently (at iOS 12) does not support temporariness of an item's accessibility in the keychain: when there is no additional security check when entering the keychain (e.g. kSecAccessControlUserPresence or similar is set), then once the device is unlocked, a key will be accessible.

