# Spring Boot Configuration Properties Support
A NetBeans plugin offering autocomplete support for spring boot configuration properties

This modules brings Spring Boot configuration properties support in NetBeans
in a similar manner as it's done in STS:

![NetBeans - Spring Boot Configuration Properties Support]
(images/nb-boot-conf-support-2.png)

![STS - Spring Boot Configuration Properties Support]
(https://raw.githubusercontent.com/kdvolder/spring-blog-2015-03/master/img/props-editor.png)


# How it works

This plugins uses [spring-boot-configuration-processor](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-tools/spring-boot-configuration-processor)
(read more [here](https://spring.io/blog/2015/03/18/spring-boot-support-in-spring-tool-suite-3-6-4#making-the-greeting-configurable)).
When this processor is added in the compilation classpath it adds a `META-INF/services/javax.annotation.processing.Processor`
which reads `@ConfigurationProperties` annotated classes and creates a `META-INF/spring-configuration-metadata.json` file with
entries describing configuration properties (name, type, description etc).

Now the metadata are generated but because this is not a standard format/schema for properties files, a plugin reading those
metadata is required for an IDE. For NetBeans' code completion API we have to read those metadata and add a specific provider
of autocompletion items to the IDE. This is what this plugin does for text/x-properties files and if spring-boot is on the
classpath.
