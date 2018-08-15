# Rainbow Wall

## What is this?
It's a very simple website that will handle dynamic input without actually requiring a dynamic website. What I mean by that, is that the content can change without user input, even though there isn't a backend to handle the user input.


## How does it work?
Well, thank you for asking!

It works via inotify. Essentially, `monitor_files.c` will create a listener for file accesses to the files/ directory. When these files are accessed (a GET request from the front end to files/blue, for example), this invokes a file read, which triggers a "callback".


## Well don't you need a webserver to host the content?
Well duh, they need to be served somehow. nginx is what this code is deployed against, but it doesn't actually matter! Essentially static files need to be accessible.

This is good when you don't have control over which ports can be opened, or when you have insufficient permissions to modify the nginx configs, to allow you hooking up your own web server.

I (ab)use query strings to ensure the GET requests are not cached.

## Why did you write this in C?, this is a few lines in Python!
This is being run on a shared server in practice, so I want to keep the memory and CPU usage as minimal as possible.

In the future I plan to make some improvements in memory consumption.

## Setting up
Make the binary via `make`. I recommend running the cronscript every hour or so, to notify whether the "server" is running and can handle input. You'll probably need to modify some strings in the monitorfile.c file, just because there's some hardcoded strings.


## TODO:
 * reduce footprint/memory consumption of daemon
 * make prettier
