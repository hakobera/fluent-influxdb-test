# fluent influxdb test

This is an influxdb with fluentd sample project for Mac OS X.

## How to use

### Install InfluxDB and run as service

```
$ brew install influxdb
$ ln -sfv /usr/local/opt/influxdb/*.plist ~/Library/LaunchAgents
$ brew services start influxdb
```

### Create test database

```
curl -X POST 'http://localhost:8086/db?u=root&p=root' \
  -d '{"name": "test"}'
```

### Get sample project

```
$ git clone https://github.com/hakobera/fluent-influxdb-test
$ cd fluent-influxdb-test
$ bundle install
```

### Run fluentd

```
$ bundle exec fluentd -c conf/fluent.conf
```

### Import dummy data

Open another console, import dummy data using [dummer](https://github.com/sonots/dummer).

```
$ bundle exec dummer -c conf/dummer.conf
```

### Get data from InfluxDB

For example, get access count for each URL and each 10 secound.

```
$ curl "http://localhost:8086/db/test/series?u=root&p=root&q=SELECT%20uri%2C%20COUNT(id)%20FROM%20dummy.test%20GROUP%20BY%20uri%2C%20time(10s)"
```
