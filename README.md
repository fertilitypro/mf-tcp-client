# TCPClient ![version](https://img.shields.io/gem/v/tcp-client?label=)

Use your TCP connections with working timeout.

- Gem: [rubygems.org](https://rubygems.org/gems/tcp-client)
- Source: [github.com](https://github.com/mblumtritt/tcp-client)
- Help: [rubydoc.info](https://rubydoc.info/gems/tcp-client/TCPClient)

## Description

This gem implements a customizable TCP client class that gives you control over time limits. You can set time limits for individual read or write calls or set a deadline for entire call sequences.
It has a very small footprint, no dependencies and is easily useable.

## Sample

```ruby
require 'tcp-client'

# create a configuration:
# - don't use internal buffering
# - use at least TLS 1.2
cfg =
  TCPClient::Configuration.create(
    buffered: false,
    ssl_params: {
      min_version: :TLS1_2
    }
  )

# request to Google.com:
# - limit all network interactions to 1.5 seconds
# - use the Configuration cfg
# - send a simple HTTP get request
# - read the returned message and headers
response =
  TCPClient.with_deadline(1.5, 'www.google.com:443', cfg) do |client|
    client.write("GET / HTTP/1.1\r\nHost: www.google.com\r\n\r\n") #=> 40
    client.readline("\r\n\r\n") #=> see response
  end

puts(response)
```

For more samples see [the examples dir](./examples)

## Installation

Use [Bundler](http://gembundler.com/) to add TCPClient in your own project:

Include in your `Gemfile`:

```ruby
gem 'tcp-client'
```

and install it by running Bundler:

```shell
bundle
```

To install the gem globally use:

```shell
gem install tcp-client
```

After that you need only a single line of code in your project to have it on board:

```ruby
require 'tcp-client'
```
