# log-driver-fluentd
A stack used as example of Docker Logging Driver and Fluentd.


# flow
A dockerize [Spring Boot Application](https://spring.io/guides/gs/spring-boot-docker/) will be running and configured to send console output event to [Fluentd](https://www.fluentd.org/).

The event stream will be forward to [Elasticsearch](https://www.elastic.co/products/elasticsearch) for index this data.

Lastly [Kibana](https://www.elastic.co/products/kibana) will show centralized logging.


# hands-on
First, build dockerized application with [Gradle](https://gradle.org/):

```bash
./app/gradlew build
```


After that, start all services - except dockerized application:

```bash
docker-compose up -d --build fluentd elasticsearch sysctl kibana
```


Finally, just run dockerized application:

```bash
docker-compose up -d app
```


# next steps
Support nanosecond (sub-second precision).

Fluent has a closed [issue](https://github.com/fluent/fluentd/issues/461) for support nanosecond resolution.

[Fluentd v0.14.9](https://github.com/fluent/fluentd/blob/master/CHANGELOG.md) fixes sub-second precision time bug ([issue](https://github.com/fluent/fluentd/issues/1276)).

And [Elasticsearch plugin for Fluentd](https://github.com/uken/fluent-plugin-elasticsearch) have two pull request that resolve nanosecond: [#223](https://github.com/uken/fluent-plugin-elasticsearch/pull/223) and [#249](https://github.com/uken/fluent-plugin-elasticsearch/pull/249).

For while, modify [fluent.conf](fluentd/fluent.conf) as suggest on [Moby Project](https://mobyproject.org/) [issue](https://github.com/moby/moby/issues/17181).


# more info
Based on [Docker Logging via EFK](https://docs.fluentd.org/v0.12/articles/docker-logging-efk-compose) and [Docker Logging Driver and Fluentd](https://docs.fluentd.org/v0.12/articles/docker-logging).

See [Fluentd Blog](https://www.fluentd.org/blog/) for news.

[Forward protocol specification](https://github.com/fluent/fluentd/wiki/Forward-Protocol-Specification-v1).

About [Docker logger](https://docs.docker.com/engine/admin/logging/overview/) output and [Fluentd logging driver](https://docs.docker.com/config/containers/logging/fluentd/).
