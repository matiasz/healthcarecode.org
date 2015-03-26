
Healthcarecode.org
=============

Healthcarecode.org is a fork of [govcode.org](https://github.com/dlapiduz/govcode.org).

From the [Govcode.org REAMDE](https://github.com/dlapiduz/govcode.org/blob/master/README.md):

> Govcode.org is an application that lists government open source projects. The purpose is to track what is being worked on and build analytics on top of it.

Healthcarecode.org is meant to provide the same type of service, except for open source projects specific to healthcare — including, but not limited to:
  - health informatics research,
  - open health data, and
  - mHealth.

Since this is a fork of [govcode.org](https://github.com/dlapiduz/govcode.org), I've copied Govcode's installation instructions below.


## Running locally

This application is structured as an API and a front end. The `common`, `govcode` and `govcoded` directories
hold the API code while the `front` directory holds the front end.

All the steps mentioned below assume that you cloned the repo into a local folder.

To setup the API you need to do the following:
1. Build the `govcode` tool:
```
cd govcode
go build
```
1. Get a github api key, go to https://github.com/settings/applications#personal-access-tokens and click "generate new token".
1. Set up a postgres database with a new user, password and db just for govcode.
1. Set the environment variables for the Postgres database and Github API key:
```
export GH_KEY="xxx"
export PG_CONN_STR="postgres://govcode_user:govcode_pass@127.0.0.1/govcode_db?sslmode=disable"
```
1. Migrate the database to build all the tables:
  `./govcode migrate`
1. (Optionally) Run an import to populate the DB:
  `./govcode import`

Now we have a loaded DB with the settings in the environment.

To actually run the server:
```
cd govcoded
go run main.go
```

Or use [gin](https://github.com/codegangsta/gin):
```
go get github.com/codegangsta/gin
cd govcoded
gin
```

This should start the API on port 3000. You can change the port by setting the `PORT` environment variable.

To run the front end:
1. Install required npm packages:
```
cd front
npm install
npm install -g bower
```
1. Install the bower packages:
`bower install`
1. Run the server:
`grunt serve`
1. Go to `http://localhost:9000` on your browser

If you see an error about `compass` you might need to install the [compass ruby gem](http://compass-style.org/install/):
`gem install compass`

## Contributing

All contributions are welcome.
 
Please create an issue describing what you want to work on
to avoid duplicate efforts.

## License

This project is licensed under the [MIT license](LICENSE).
