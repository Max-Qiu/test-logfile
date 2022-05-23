a complete yet minimal sample for [The logfile in the configuration center does not take effect for actuator](https://github.com/spring-projects/spring-boot/issues/31144)

> hint :

- The `nacos` test server has been set up : [http://150.158.165.26:8848/nacos/](http://150.158.165.26:8848/nacos/)  (The username and password are in file `bootstrap.yml`)
- `SpringBoot` -> 2.6.8



> debug log:

1. `LogFile.get(PropertyResolver propertyResolver)` will be executed four times
   - The first two times by  `LoggingApplicationListener.initialize()`
   - Third by `PropertySourceBootstrapConfiguration.initialize()`
   - Fourth by `PropertySourceBootstrapConfiguration.reinitializeLoggingSystem()` ,this is the only time to get the configuration center configuration
2. `LogFileWebEndpointAutoConfiguration` will create `LogFileWebEndpoint`，but at `LogFileWebEndpoint logFileWebEndpoint(ObjectProvider<LogFile> logFile,LogFileWebEndpointProperties properties)` , the `logFile.getIfAvailable()` is old







PS: My English is not very good, so the translation may not be accurate.
