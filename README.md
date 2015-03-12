# go-collectd

Utilities for using [collectd](https://collectd.org/) together with [Go](http://golang.org/).

# Synopsis

    package main
    
    import (
        "time"
        
        "collectd.org/api"
        "collectd.org/exec"
    )
    
    func main() {
        vl := api.ValueList{
            Identifier: api.Identifier{
                Host:   exec.Hostname(),
                Plugin: "golang",
                Type:   "gauge",
            },
            Time:     time.Now(),
            Interval: exec.Interval(),
            Values:   []api.Value{api.Gauge(42)},
        }
        exec.Putval.Dispatch(vl)
    }

# Description

This is a very simple package and very much a *Work in Progress*, so expect
things to move around and be renamed a lot.

The reposiroty is organized as follows:

* Package `collectd.org/api` declares data structures you may already know from
  the *collectd* source code itself, such as `ValueList`.
* Package `collectd.org/exec` declares some utilities for writing binaries to
  be executed with the *exec plugin*. It provides some utilities (getting the
  hostname, e.g.) and an executor which you may use to easily schedule function
  calls.
* Package `collectd.org/format` declares functions for formatting *ValueLists*
  in other format. Right now, only `PUTVAL` is implemented. Eventually I plan
  to add parsers for some formats, such as the JSON export.
* Package `collectd.org/network` implements collectd's
  [binary network protocol](https://collectd.org/wiki/index.php/Binary_protocol).
  Currently, only a client implementation is available.

# Author

Florian "octo" Forster &lt;ff at octo.it&gt;
