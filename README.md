# DwpEncodedLogger
[![Build Status](https://travis-ci.org/dwp/encoded-logger-output.svg?branch=master)](https://travis-ci.org/dwp/encoded-logger-output) [![Known Vulnerabilities](https://snyk.io/test/github/dwp/encoded-logger-output/badge.svg)](https://snyk.io/test/github/dwp/encoded-logger-output)

This is a simple project that provides DWPs Health PDU standard Java Logger 
implementations for standard Java Logging Libraries

This project was originally created to mitigate the **Heap_Inspection** vulnerability :-

_`The application writes audit logs upon security-sensitive actions. Since the audit log includes user input that is neither checked for data type validity nor subsequently sanitized, the input could contain false information made to look like legitimate audit log data`_

### [Breaking Change with Java17](https://spring.io/blog/2022/05/24/preparing-for-spring-boot-3-0)
A breaking change is introduced with version 3.0.0 which is Java 17 upgrade.

Jakarta EE 9 a new top-level jakarta package, replacing EE 8’s javax top-level package. For example, the Servlet specification in Jakarta EE 8 uses a javax.servlet package but this has changed to jakarta.servlet in EE 9.

Generally speaking, it’s not possible to mix Java EE and Jakarta EE APIs in the same project. You need to ensure that your own code, as well as all third-party libraries are using jakarta.* package imports.

## Implementations
There are implementations for `LogBack` and `Log4j2`

The library assumes that the desired logging implementation  is provided on the 
class path.  The default log level is **_INFO_**.

#### Project inclusion

properties entry in pom

    <properties>
        <dwp.encoded_logger>x.x</dwp.encoded_logger>
    </properties>

dependency reference

    <dependency>
        <groupId>uk.gov.dwp.logging</groupId>
        <artifactId>encoded-logger-output</artifactId>
        <version>${dwp.encoded_logger}</version>
    </dependency>
    

and include the relevant logging system `Logback` or `Log4j2`

## Configuration
### Logback
The default configuration provided by this package assumes that there is an 
`application.yml` file in the root of the classpath that contains -- at least --
`app_name` and `app_version` attributes that are set to the specific values.

### Log4j2
The default configuration provided by this package assumes that there are two
system properties `app_name` and `app_version` set the relevant values. How these
are set is up the specific application.

** WINDOWS USERS **

This test suite uses a file to match the logging output against the expected values.  The default file encoding for windows command-line is not *UTF8* and (as such) will cause characters like the pound sign to be interpreted differently to that of the logger's character set.  In order to enforce *UTF8* encoding please set the following environment variable

    JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF8