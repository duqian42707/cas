---
layout: default
title: CAS - Couchbase Ticket Registry
category: Ticketing
---

{% include variables.html %}

# Couchbase Ticket Registry

Couchbase integration is enabled by including the following dependency in the WAR overlay:

{% include_cached casmodule.html group="org.apereo.cas" module="cas-server-support-couchbase-ticket-registry" %}

[Couchbase](http://www.couchbase.com) is a highly available, open source NoSQL database server based on
[Erlang/OTP](http://www.erlang.org) and its mnesia database. The intention of this
registry is to leverage the capability of Couchbase server to provide high availability to CAS.

## Configuration

{% include_cached casproperties.html properties="cas.ticket.registry.couchbase" %}

The Couchbase integration currently assumes that the ticket registries are stored
in their own buckets. You may optionally set passwords for the buckets and optionally configure
redundancy and replication as per normal Couchbase configuration.

The only truly mandatory setting is the list of nodes.
The other settings are optional, but this is designed to store data in buckets
so in reality the bucket property must also be set.

## Expiration Policy

You will need to remember that every document in Couchbase contains the `expiry` property.
An expiration time-to-live value of `0` means that no expiration is set at all.
The expiration time starts when the document has been successfully stored on the server,
not when the document was created on the CAS server. In practice, the delta should be very very negligible.
Any expiration time larger than `30` days in seconds is considered absolute (as in a Unix time stamp)
and anything smaller is considered relative in seconds.

## Troubleshooting

To enable additional logging, configure the log4j configuration file to add the following
levels:

```xml
...
<Logger name="com.couchbase" level="debug" additivity="false">
    <AppenderRef ref="console"/>
    <AppenderRef ref="file"/>
</Logger>
...
```
