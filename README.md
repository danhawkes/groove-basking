# Basking

Sync a Grooveshark library to disk.

[![Build Status](http://arcs.co/jenkins/buildStatus/icon?job=basking)](http://arcs.co/jenkins/job/basking/)

## Features

* Command line API for use as a scheduled job
  * `$ basking -dir "~/music" -user "username" -pass "password"`
* Playlist generation
  * `GS Favorites` and `GS Collection.m3u`  
* Robust system for keeping everything in sync with the API
  * Grooveshark identifier is embedded in IDv3 tag, so files can be renamed/retagged without getting lost.
  * Deletions/removed favorites are propagated to the local library

## Installation

### Java

With Maven:

```xml
<dependency>
	<groupId>co.arcs.groove</groupId>
	<artifactId>basking</artifactId>
	<version>X.X.X</version>
</dependency>
```

Or Gradle:

```groovy
compile 'co.arcs.groove:basking:X.X.X'
```

Find the latest version on [maven central](http://search.maven.org/#search|ga|1|g%3A%22co.arcs.groove%22%20AND%20a%3A%22basking%22).

### Command line

Get the [distribution package](http://search.maven.org/#search|ga|1|g%3A%22co.arcs.groove%22%20AND%20a%3A%22basking%22).

The jar-with-dependencies and wrapper script need adding to the path. On linux or OSX that would look something like this:

```bash
unzip basking-1.5.3-dist.zip
sudo cp -r basking-1.5.3 /usr/local/bin
sudo ln -s -f /usr/local/bin/basking-1.5.3/basking /usr/local/bin/basking
```

## Usage

### Java

```java
Config config = new Config();
config.syncPath = new File("./music");
config.username = "user@email.com";
config.password = "password"

SyncService service = new SyncService(config);
ListenableFuture<SyncOutcome> outcome = service.start();
```

### Command line

```bash
Usage: basking [options]
  Options:
    -cfg, --config
       JSON configuration file to load.
    -dry, --dry-run
       Do not modify the disk.
       Default: false
    -h, --help
       Show this help.
       Default: false
    -num, --num-concurrent
       Number of concurrent downloads.
       Default: 1
  * -pass, --password
       Grooveshark user password.
  * -dir, --sync-dir
       Directory to sync. Will be created if it does not already exist.
  * -user, --username
       Grooveshark user name.
```

## Licence

Apache 2.0. See `LICENCE.txt` for details.
