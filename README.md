# grpc-install

Installing all the tools you need for gRPC can be difficult.  This repo strives to solve this.

## Install gRPC binaries

Clone this library:

```sh
git clone https://github.com/gopherguides/grpc-install
```

CD into the project directory:

```sh
cd grpc-install
```

Run the following command to download the necessary libraries:
```sh
go mod tidy
```

That will make sure you have the correct version of the libraries, we now need to make sure you have the binaries installed that we will used to generate the code:

Run the following commands from the project root:

```sh
go install \
    github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway \
    github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2 \
    google.golang.org/protobuf/cmd/protoc-gen-go \
    google.golang.org/grpc/cmd/protoc-gen-go-grpc
```


## Install protoc binary

Download Protocol Buffer Compiler

[https://github.com/google/protobuf/releases](https://github.com/google/protobuf/releases)

You will need to choose the file that is most appropriate for your operating system and architecture.

### Mac/Unix Instructions

You will need to choose the file that is most appropriate for your operating system and architecture.

For example:

```
protoc-X.X.X-osx-x86_64.zip
```

This zip file will have a `include` and a `bin` folder, you will only need the the contents of the `bin` folder.


* Move the contents of the `bin` folder to your `$GOPATH/bin` directory.
* To find out what your current `$GOPATH` is, use the following command:

```command
go env GOPATH
```

It should return a result like:

```sh
/Users/corylanou/go
```

Which would make our `$GOPATH\bin`:

```sh
$HOME/go/bin
```

You should be able to run `protoc --version` when this is done and receive a successful version response.

Output:

```sh
libprotoc 3.17.4
```

If the file isn't found, your `go\bin` directory is not on your system path. You can add it to your current shell with:

```sh
export PATH="$HOME/go/bin:$PATH"
```

If you receive a `can't run process` error, you have to authorize the binary.  You can do this from the command line with:

```sh
xattr -d com.apple.quarantine protoc
```

or `System Preferences` -> `Security & Privacy`

#### Include Folder

The `include` folder contains definitions for `well known types`. While we'll cover these later, it is necessary to install them now.

The best place to put them is in your `$GOPATH/src` directory.

We only want the content's of the `include` directory starting with the `google` directory.  We do NOT want the `include` directory.

This will result in a path like:

```
/$HOME/go/src/google
└── protobuf
    ├── any.proto
    ├── api.proto
    ├── compiler
    │   └── plugin.proto
    ├── descriptor.proto
    ├── duration.proto
    ├── empty.proto
    ├── field_mask.proto
    ├── source_context.proto
    ├── struct.proto
    ├── timestamp.proto
    ├── type.proto
    └── wrappers.proto
```

### Windows Instructions

You will need to download the `win64` file.

For example:

```
protoc-X.X.X-win64.zip
```

This zip file will have a `include` and a `bin` folder.

* Move the contents of the `bin` folder to your `%GOPATH%\bin` directory.
* To find out what your current `%GOPATH%` is, use the following command:

```command
go env GOPATH
```

It should return a result like:

```sh
\Users\corylanou\go
```

Which would make our `$GOPATH\bin`:

```sh
%USERPROFILE%\go\bin
```

You should be able to run `protoc --version` when this is done and receive a successful version response.

Output:

```sh
libprotoc 3.17.4
```

If the file isn't found, your `go\bin` directory is not on your system path. You can add it to your path with the following instructions:

1. Click the "Start" menu
1. Type in environment variables and select "Edit environment variables for your account".
1. In the "User variables for <name>"
1. Select the Path variable
1. Click "Edit"
1. Click "New"
1. Type %USERPROFILE%\go\bin
1. Click "OK"
1. Click "OK" again to dismiss the environment variables window

#### Include Folder

The `include` folder contains definitions for `well known types`. While we'll cover these later, it is necessary to install them now.

The best place to put them is in your `%GOPATH%\src` directory.

We only want the content's of the `include` directory starting with the `google` directory.  We do NOT want the `include` directory.

This will result in a path like:

```
\%USERPROFILE%\go\src\google
└── protobuf
    ├── any.proto
    ├── api.proto
    ├── compiler
    │   └── plugin.proto
    ├── descriptor.proto
    ├── duration.proto
    ├── empty.proto
    ├── field_mask.proto
    ├── source_context.proto
    ├── struct.proto
    ├── timestamp.proto
    ├── type.proto
    └── wrappers.proto
```


