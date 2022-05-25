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



PS:If `nacos` cannot connect or the password is incorrect,Use the following command to quickly start a `nacos` with Docker,The default username and password are both `nacos`



```
docker run -d --restart always --name nacos -p 8848:8848 -p 9848:9848 -e MODE=standalone nacos/nacos-server:v2.1.0
```





PS: My English is not very good, so the translation may not be accurate.
