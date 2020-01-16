# Dev Kit Development Environment

## Intro

This project is for developers.  It's purpose is to help them set up a local node where they can work on the Block Explorer and API.  Some instructions may be assuming you're on a MacBook.

## Instructions

* Clone the following into directories next to this one:
    * [ravencore-node](https://github.com/RavenDevKit/ravencore-node)
    * [insight-api](https://github.com/RavenDevKit/insight-api)
    * [insight-ui](https://github.com/RavenDevKit/insight-ui)

    Your directory structure should now look like this:
    ```bash
    ├── devnode
    ├── insight-api
    ├── insight-ui
    └── ravencore-node
    ```

* Go into each of the three new directories and run `npm install`.

* Install [Ravencoin](https://ravencoin.org/wallet/).

* Copy `ravencore-node.json.template` to `ravencore-node.json` and fill in the missing configuration:
    - `servicesConfig/ravend/exec`: set to the absolute path to the `ravend` executible you just installed.
    - `servicesConfig/ravend/datadir`: set to the absulute path to your `devnode/data` directory.

* Install and set up MongoDB for stats support
    - `brew tap mongodb/brew`
    - `brew install mongodb-community`
    - `brew services start mongodb-community`
    - `mongo`
        - `>use raven-api-regtest`
        - `>db.createUser( { user: "test", pwd: "test1234", roles: [ "readWrite" ] } )`
        - `>exit`

* Make sure you're in the `devnode` directory and run `bin/start`.  You should see some logging scroll by as the node loads up.  When it's ready try out the [Block Explorer](http://localhost:3001/blocks) and the [API](http://localhost:3001/api/status?q=getInfo).

## Troubleshooting

Some quirks we've come across with helpful hints.

* `Error: Cannot find module '../build/Release/zmq.node'`:
    - Try running `npm install zeromq` from the `ravencoin-node` directory.