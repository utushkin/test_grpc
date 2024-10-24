go get google.golang.org/protobuf/cmd/protoc-gen-go
go get google.golang.org/grpc/cmd/protoc-gen-go-grpc

cd ./user
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative --experimental_allow_proto3_optional user.proto

---
Если

```shell
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative --experimental_allow_proto3_optional user.proto

protoc-gen-go: program not found or is not executable
Please specify a program using absolute path or make sure the program is available in your PATH system variable
--go_out: protoc-gen-go: Plugin failed with status code 1.
```

go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

export PATH="$PATH:$(go env GOPATH)/bin"
source ~/.bashrc  # или source ~/.bash_profile или source ~/.zshrc

which protoc-gen-go
which protoc-gen-go-grpc
---

Если
```shell
protoc-gen-go: unable to determine Go import path for "user.proto"

Please specify either:
        • a "go_package" option in the .proto source file, or
        • a "M" argument on the command line.

See https://protobuf.dev/reference/go/go-generated#package for more information.

--go_out: protoc-gen-go: Plugin failed with status code 1
```

Откройте ваш файл user.proto и добавьте строку с option go_package.
```protobuf
syntax = "proto3";
package yourpackage;
option go_package = "path/to/your/package;yourpackage";
```



