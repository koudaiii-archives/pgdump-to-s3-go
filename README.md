# pgdump-to-s3-go

[![Build Status](https://travis-ci.org/koudaiii/pgdump-to-s3-go.svg?branch=master)](https://travis-ci.org/koudaiii/pgdump-to-s3-go)
[![Docker Repository on Quay](https://quay.io/repository/koudaiii/pgdump-to-s3-go/status "Docker Repository on Quay")](https://quay.io/repository/koudaiii/pgdump-to-s3-go)
[![GitHub release](https://img.shields.io/github/release/koudaiii/pgdump-to-s3-go.svg)](https://github.com/koudaiii/pgdump-to-s3-go/releases)

## Description

pgdump-to-s3-go create pg_dump, put dump file in the specified s3 URL.
Also change the file name and put it in s3 URL where all the past dump files are stored (ex: `<backet_name>/<prefix_name>s/<file_name>.YYYYMMDD_HHMMSS`)

## Table of Contents

* [pgdump-to-s3-go](#pgdump-to-s3-go)
  * [Description](#description)
  * [Table of Contents](#table-of-contents)
  * [Requirements](#requirements)
  * [Installation](#installation)
    * [Using Homebrew (OS X only)](#using-homebrew-os-x-only)
    * [Precompiled binary](#precompiled-binary)
    * [From source](#from-source)
    * [Run in a Docker container](#run-in-a-docker-container)
  * [Usage](#usage)
    * [Options](#options)
  * [Development](#development)
  * [Contribution](#contribution)
  * [Author](#author)
  * [License](#license)

## Requirements

- `pg_dump` command
- You need to set AWS credentials beforehand, or you can also use [named profile](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-multiple-profiles) written in `~/.aws/credentials`.

```shell-session
export AWS_ACCESS_KEY_ID=XXXXXXXX
export AWS_SECRET_ACCESS_KEY=XXXXXXXX
# or configure them in ~/.aws/credentials

export AWS_REGION=xx-yyyy-0
```

## Installation

### Using Homebrew (OS X only)

Formula is available at [koudaiii/homebrew-tools](https://github.com/koudaiii/homebrew-tools).

```shell-session
$ brew tap koudaiii/pgdump-to-s3-go
$ brew install pgdump-to-s3-go
```

### Precompiled binary

Precompiled binaries for Windows, OS X, Linux are available at [Releases](https://github.com/koudaiii/pgdump-to-s3-go/releases).

### From source
To install, use `go get`:

```shell-session
$ go get -d github.com/koudaiii/pgdump-to-s3-go
$ cd $GOPATH/src/github.com/koudaiii/pgdump-to-s3-go
$ make deps
$ make install
```

### Run in a Docker container

docker image is available at [quay.io/koudaiii/pgdump-to-s3-go](https://quay.io/repository/koudaiii/pgdump-to-s3-go).

```shell-session
# -t is required to colorize logs
$ docker run \
    --rm \
    -t \
    -e AWS_ACCESS_KEY_ID=XXXXXXXX \
    -e AWS_SECRET_ACCESS_KEY=XXXXXXXX \
    -e AWS_REGION=xx-yyyy-0 \
    quay.io/koudaiii/pgdump-to-s3-go:latest \
    --db-url=postgresq://hoge:hoge@hoge:5432/dbname \
    --s3-url=s3://hogehoge/dump/db.dump \
    --dry-run
```

## Usage

```shell-session
pgdump-to-s3-go --db-url=postgresq://hoge:hoge@hoge:5432/dbname --output s3://hogehoge/dump/db.dump

Uploaded!
  s3://hogehoge/dump/db.dump
  s3://hogehoge/dumps/db.dump.20180204_231110
```

- `--dry-run`

```shell-session
pgdump-to-s3-go --db-url=postgresq://hoge:hoge@hoge:5432/dbname --output s3://hogehoge/dump/db.dump --dry-run

Upload URL
  s3://hogehoge/dump/db.dump
  s3://hogehoge/dumps/db.dump.20180204_231110
```

### Options

|Option|Description|Required|Default|
|---------|-----------|-------|-------|
|`--help`|Print command line usage|||
|`-v`, `--version`|Print version|||

## Development

Clone this repository and build using `make`.

```shell-session
$ go get -d github.com/koudaiii/pgdump-to-s3-go
$ cd $GOPATH/src/github.com/koudaiii/pgdump-to-s3-go
$ make
```

## Contribution

1. Fork ([https://github.com/koudaiii/pgdump-to-s3-go/fork](https://github.com/koudaiii/pgdump-to-s3-go/fork))
1. Create a feature branch
1. Commit your changes
1. Rebase your local changes against the master branch
1. Run test suite with the `go test ./...` command and confirm that it passes
1. Run `gofmt -s`
1. Create a new Pull Request

## Author

[koudaiii](https://github.com/koudaiii)

## License

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)
