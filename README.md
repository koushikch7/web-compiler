Web Compiler
------------

**Web Compiler** is an interactive compiler. The left-hand pane shows
 editable C, C++, Rust, Go, D, Haskell, Swift, Pascal (and some more!) code.
The right, the assembly output of having compiled the code with a given
 compiler and settings. Multiple compilers are supported, and the UI layout
 is configurable.
There is also an ispc compiler _[?](https://ispc.github.io/)_ for a C variant
 with extensions for SPMD.

Try out at [compiler.chkoushik.com](https://compiler.chkoushik.com)

**Web Compiler** follows a [Code of Conduct](CODE_OF_CONDUCT.md) which
 aims to foster an open and welcoming environment.

**Web Compiler** was started in 2012 to serve my needs at [my previous employer](https://drw.com) to show how
 C++ constructs translated to assembly code. It started out as a `tmux` session with `vi` running in one
 pane and `watch gcc -S foo.cc -o -` running in the other.
Since then, it has become a public website serving around [210,000 compilations per day](https://www.stathat.com/cards/Tk5csAWI0O7x).

### Developing

**Web Compiler** is written in [Node.js](https://nodejs.org/).

Assuming you have a compatible version of `node` installed, simply running
 `make` ought to get you up and running with an Explorer running on port 10240
 on your local machine: http://localhost:10240/.
 Currently **Web Compiler**
 [requires the latest LTS](CONTRIBUTING.md#node-version) `node` version
 (_v12_) installed, either on the path or at `NODE_DIR`
 (an environment variable or `make` parameter).

Running with `make EXTRA_ARGS='--language LANG'` will allow you to load
 `LANG` exclusively, where `LANG` is one for the language ids/aliases defined
 in `lib/languages.js`. The `Makefile` will automatically install all the
 third party libraries needed to run; using `npm` to install server-side and
 client side components.

Some languages need extra tools to demangle them, e.g. `rust`, `d`, or `haskell`.
 Such tools are kept separately in the
 [tools repo](https://github.com/mattgodbolt/compiler-explorer-tools).

The config system leaves a lot to be desired.
 [Work has been done](https://github.com/rabsrincon/ccs-js) on porting
 [CCS](https://github.com/hellige/ccs-cpp) to Javascript and then something
 more rational can be used.

### Running a local instance

If you want to point it at your own GCC or similar binaries, either edit the
 `etc/config/LANG.defaults.properties` or else make a new one with
 the name `LANG.local.properties`, substituting `LANG` as needed.
 `*.local.properties` files have the highest priority when loading properties.

When running in a corporate setting the URL shortening service can be replaced
 by an internal one if the default storage driver isn't appropriate for your
 environment. To do this, add a new module in `lib/shortener-myservice.js` and
 set the `urlShortenService` variable in configuration. This module should
 export a single function, see the [tinyurl module](lib/shortener-tinyurl.js)
 for an example.
