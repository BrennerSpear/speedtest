# speedtest

> HTML5 Speedtest

This speedtest uses [the same algorithm](doc/algorithm.md) as the Ookla / speedtest.net test. Because of that it gives about the same results.

It has a responsive interface, and can be used on desktop, tablets and phones.

![speedtest-dark](https://user-images.githubusercontent.com/6455542/83277443-589b5380-a1d2-11ea-83e6-c620326ed3e1.png)

## Development / Build Setup

- as usual, you need nodejs and yarn
- you need to have the Go compiler (golang) installed, version 1.6 or later
  (for debian jessie, there's a modern enough version in jessie-backports)
- the Makefile for the server sets GOPATH to $HOME. That means the build
  environment will put the go library dependencies in ~/src and ~/pkg. You
  might have to create ~/src first. If your setup is different, edit server/Makefile.

Then clone the repo and build:

``` bash
# clone repo
cd ~/src
git clone https://github.com/miquels/speedtest.git
cd speedtest

# install dependencies
yarn

# install configuration file
cp static/config.json.example static/config.json
vim static/config.json

# serve with hot reload at localhost:8080
yarn serve

# build for production with minification
yarn build
```

## Run the server
``` bash
# build server
cd server
go dep
go build
cd ..

# run server
server/server
```

If you point yout browser at localhost:8080, you should see the webinterface.

If it doesn't work, use your browsers debugger/inspector, and look at the
javascript console - that should give you a hint as to what is going on.
For example, Chrome on OSX, press Option + Command + J.

## Production use

```
# build
yarn build

# copy files to your webservers root
cp -av dist/* /path/to/www/html
cp static/config.json /path/to/www/html/static
```

You also need to run the API server as a daemon- that's OS specific, and
no sysv / systemd / whatever files have been included yet. The easiest
solution is to run it in a ``screen'' session for now :)

