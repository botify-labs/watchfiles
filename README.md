# Overview

`Watchfiles` is a simple bash script that uses `inotifywait` from
`inotify-tools` to watch for events in a path. When an event occur on a file,
`watchfiles` writes the name of the event and the path the file either on
stdout or in a named piped if it was provided. 

Its purpose is to be and to stay simple. Any complex processing should be done
in a process that reads watchfiles's stdout or named pipe.

Any feedback and enhancement is welcome :).

# Examples

The line below will write events and paths, separated by a `\t` on stdout:

```sh
$ watchfiles /path/to/dir
```

The line below will write in the `watch.fifo` named pipe:

```sh
$ watchfiles /path/to/dir watch.fifo
```

Other processes can read the named pipe to get the events and paths (you can
`cat watch.fifo` to get them).

Launch as a daemon:

```sh
$ nohup ./watchfiles dir watch.fifo 0<&- &>/dev/null &
```
