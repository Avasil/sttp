![sttp](https://github.com/softwaremill/sttp/raw/master/banner.png)

[![Join the chat at https://gitter.im/softwaremill/sttp](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/softwaremill/sttp?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://travis-ci.org/softwaremill/sttp.svg?branch=master)](https://travis-ci.org/softwaremill/sttp)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.softwaremill.sttp.client/core_2.12/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.softwaremill.sttp.client/core_2.12)

The Scala HTTP client that you always wanted!

sttp client is an open-source library which provides a clean, programmer-friendly API to define HTTP requests and execute them using one of the wrapped backends, such as akka-http, async-http-client, http4s or OkHttp.
 
```scala
import sttp.client._

val sort: Option[String] = None
val query = "http language:scala"

// the `query` parameter is automatically url-encoded
// `sort` is removed, as the value is not defined
val request = basicRequest.get(uri"https://api.github.com/search/repositories?q=$query&sort=$sort")
  
implicit val backend = HttpURLConnectionBackend()
val response = request.send()

// response.header(...): Option[String]
println(response.header("Content-Length")) 

// response.body: by default read into an Either[String, String] to indicate failure or success 
println(response.body)                     
```

## Documentation

sttp (v2) documentation is available at [sttp.readthedocs.io](http://sttp.readthedocs.io).

sttp (v1) documentation is available at [sttp.readthedocs.io/en/v1](https://sttp.readthedocs.io/en/v1).

scaladoc is available at [https://www.javadoc.io](https://www.javadoc.io/doc/com.softwaremill.sttp.client/core_2.12/2.0.0-RC1)

You can also take a look at the [introductory blog](https://softwaremill.com/introducing-sttp-the-scala-http-client/)
and its [follow-up](https://softwaremill.com/sttp-streaming-uri-interpolator/).

## Quickstart with Ammonite

If you are an [Ammonite](http://ammonite.io) user, you can quickly start experimenting with sttp by copy-pasting the following:

```scala
import $ivy.`com.softwaremill.sttp.client::core:2.0.0-RC1`
import sttp.client.quick._
quickRequest.get(uri"http://httpbin.org/ip").send()
```

This brings in the sttp API and an implicit, synchronous backend.

## Quickstart with sbt

Add the following dependency:

```scala
"com.softwaremill.sttp.client" %% "core" % "2.0.0-RC1"
```

Then, import:

```scala
import sttp.client._
```

Type `sttp.` and see where your IDE’s auto-complete gets you!

## Other sttp projects

sttp is a family of Scala HTTP-related projects, and currently includes:

* sttp client: this project
* [sttp tapir](https://github.com/softwaremill/tapir): Typed API descRiptions
* [sttp model](https://github.com/softwaremill/sttp-model): simple HTTP model classes (used by client & tapir)

## Contributing

If you have a question, or hit a problem, feel free to ask on our [gitter channel](https://gitter.im/softwaremill/sttp)!

Or, if you encounter a bug, something is unclear in the code or documentation, don’t hesitate and open an issue on GitHub.

We are also always looking for contributions and new ideas, so if you’d like to get into the project, check out the [open issues](https://github.com/softwaremill/sttp/issues), or post your own suggestions!

### Testing the Scala.JS backend

Running the tests using the JS backend has some prerequisities:

* Install [Google Chrome](https://www.google.com/chrome/)
* Download [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) and 
[install it](https://sites.google.com/a/chromium.org/chromedriver/getting-started)

Note that running the default `test` task will run the tests using both the JVM and JS backends.
If you'd like to run the tests using *only* the JVM backend, execute: `sbt rootJVM/test`.

### Building & testing the scala-native backend

By default, sttp-native will **not** be included in the aggregate build of the root project. To include it, define the `STTP_NATIVE` environmental variable before running sbt, e.g.:

```
STTP_NATIVE=1 sbt
```

You might need to install some additional libraries, see the [scala native](http://www.scala-native.org/en/latest/user/setup.html) documentation site.

On MacOS, you need to: `brew install llvm bdw-gc re2 libidn curl`. If your system curl is older than `7.56.0`, you'll need to use the updated brewl-curl when linking & compiling. To do that, create a `core/native/local.sbt` file, and add:

```
nativeCompileOptions += "-I/usr/local/opt/curl/include"
nativeLinkingOptions += "-L/usr/local/opt/curl/lib"
```

where the specific paths correspond to the output of the `brew install curl` command.

## Commercial Support

We offer commercial support for sttp and related technologies, as well as development services. [Contact us](https://softwaremill.com) to learn more about our offer!

## Copyright

Copyright (C) 2017-2019 SoftwareMill [https://softwaremill.com](https://softwaremill.com).
