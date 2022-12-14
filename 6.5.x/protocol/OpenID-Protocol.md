---
layout: default
title: CAS - OpenID Protocol
category: Protocols
---

{% include variables.html %}

# OpenID Protocol

OpenID is an open, decentralized, free framework for user-centric digital identity. Users represent
themselves using URIs. For more information see the [http://www.openid.net](http://www.openid.net).

<div class="alert alert-warning"><strong>Usage</strong>
<p><strong>This feature is deprecated and is scheduled to be removed in the future.</strong> If you can, consider using
a more mainstream and recent authentication protocol.</p>
</div>

CAS supports both the "dumb" and "smart" modes of the OpenID protocol. Dumb mode acts in a similar fashion
to the existing CAS protocol. The smart mode differs in that it establishes an association between the client and
the openId provider (OP) at the beginning. Thanks to that association and the key exchange done during association,
information exchanged between the client and the provider are signed and verified using this key. There is no need
for the final request (which is equivalent in CAS protocol to the ticket validation).

OpenID identifiers are URIs. The default mechanism in CAS support is an uri ending with the actual user login
(ie. `http://my.cas.server/openid/myusername` where the actual user login id is `myusername`).
This is not recommended and you should think of a more elaborated way of providing URIs to your users.

<div class="alert alert-info"><strong>Pay Attention!</strong><p>OpenID protocol is <strong>NOT</strong> the same thing
as the OpenId Connect protocol whose details are <a href="OIDC-Protocol.html">documented here</a>.</p></div>

## Configuration

Support is enabled by including the following dependency in the WAR overlay:

{% include_cached casmodule.html group="org.apereo.cas" module="cas-server-support-openid-webflow" %}

{% include_cached casproperties.html properties="cas.authn.openid." %}

## Register Clients

Register clients in the CAS service registry:

```json
{
  "@class" : "org.apereo.cas.services.RegexRegisteredService",
  "serviceId" : "https://openid.example.org/myapp",
  "name" : "openid",
  "description" : "OpenID Sample Application",
  "id" : 10
}
```

## Sample Client Applications

- [OpenID Client Webapp](https://github.com/apereo/openid-sample-java-webapp)

# OpenID Provider Delegation

Using the OpenID protocol, the CAS server can also be configured to [delegate the authentication](../integration/Delegate-Authentication.html) to an OpenID provider.
