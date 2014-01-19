# Opal

[![Build Status](https://secure.travis-ci.org/opal/opal.png?branch=master)](http://travis-ci.org/opal/opal)
[![Gem Version](https://badge.fury.io/rb/opal.png)](http://badge.fury.io/rb/opal)
[![Code Climate](https://codeclimate.com/github/opal/opal.png)](https://codeclimate.com/github/opal/opal)

Opal is a ruby to javascript source-to-source compiler. It also has an
implementation of the ruby corelib.

Opal is [hosted on github](http://github.com/opal/opal), and there
is a Freenode IRC channel at [#opal](http://webchat.freenode.net/?channels=opal). There is also a [google group for opal](http://groups.google.com/forum/#!forum/opalrb).

## Usage

See the website, [http://opalrb.org](http://opalrb.org).

### Compiling ruby code

`Opal.compile` is a simple interface to just compile a string of ruby into a
string of javascript code.

```ruby
Opal.compile("puts 'wow'")  # => "(function() { ... })()"
```

Running this by itself is not enough, you need the opal runtime/corelib.

### Building the corelib

`Opal::Builder` can be used to build the runtime/corelib into a string.

```ruby
Opal::Builder.build('opal') #=> "(function() { ... })()"
```

### Running compiled code

You can write the above two strings to file, and run as:

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="opal.js"></script>
    <script src="app.js"></script>
  </head>
</html>
```

Just open a browser to this page and view the console.

## Running tests

First, install dependencies:

    $ bundle install

Rubyspecs must be cloned as a gitsubmodule:

    $ git submodule update --init

Tests can be run with phantomjs using:

    $ rake

Alternatively, you can just load up a rack instance using `rackup spec/config.ru`, and
visit `http://localhost:9292/` in any web browser.

## Code Overview

What code is supposed to run where?

* `lib/` code runs inside your ruby env. It compiles ruby to javascript.
* `opal/` is the runtime/corelib for our implementation (runs in browser)
* `stdlib/` is our implementation of ruby stdlib. It is optional (for browser).

### lib

The `lib` directory holds the opal parser/compiler used to compile ruby
into javascript. It is also built ready for the browser into `opal-parser.js`
to allow compilation in any javascript environment.

### corelib

This directory holds the opal runtime and corelib implemented in ruby and
javascript.

### stdlib

Holds the stdlib that opal currently supports. This includes Observable,
StringScanner, Date, etc.

### spec

* **opal** opal additions/special behaviour in the runtime/corelib
* **cli** specs for opal lib (parser, lexer, grammar, compiler etc)

## Browser support

* Internet Explorer 6+
* Firefox (Current - 1) or Current
* Chrome (Current - 1) or Current
* Safari 5.1+
* Opera 12.1x or (Current - 1) or Current

Any problem above browsers should be considered and reported as a bug.

(Current - 1) or Current denotes that we support the current stable version of
the browser and the version that preceded it. For example, if the current
version of a browser is 24.x, we support the 24.x and 23.x versions.

12.1x or (Current - 1) or Current denotes that we support Opera 12.1x as well
as last 2 versions of Opera. For example, if the current Opera version is 20.x,
we support Opera 12.1x, 19.x and 20.x but not Opera 15.x through 18.x.

Cross-browser testing sponsored by [BrowserStack](http://browserstack.com).

## Building Javascript Source Files

You'll need to have Ruby and [Node](http://nodejs.org/) installed.

```
git clone git@github.com:opal/opal.git
cd opal
gem install bundler
bundler install
npm install -g uglify-js
rake dist
```

The built files can then be found in `/build`.

## License

(The MIT License)

Copyright (C) 2013 by Adam Beynon

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/opal/opal/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

