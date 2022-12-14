---
layout: default
title: CAS - Password Management
category: Password Management
---

{% include variables.html %}

# Password Management - Custom

You may also inject your own implementation for password management into CAS that would itself handle account updates and retrievals.
In order to do this, you will need to design a configuration class that roughly matches the following: 

```java
package org.apereo.cas.pm;

@Configuration(value = "MyPasswordConfiguration", proxyBeanMethods = false)
@EnableConfigurationProperties(CasConfigurationProperties.class)
public class MyPasswordConfiguration {

    @Bean
    public PasswordManagementService passwordChangeService() {
        ...
    }
}
```

[See this guide](../configuration/Configuration-Management-Extensions.html) to learn more about how to register configurations into the CAS runtime.
