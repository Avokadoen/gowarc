PROTOC_VERSION=3.11.4

.PHONY: all
.PHONY: clean

go_files := $(patsubst %.proto,%.pb.go,$(wildcard *.proto))
all: $(go_files)

clean:
	rm -rf tools

distclean:
	rm *.pb.go

tools:
	mkdir tools
	cd tools \
	&& wget -q https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip \
	&& unzip protoc-${PROTOC_VERSION}-linux-x86_64.zip \
	&& rm protoc-${PROTOC_VERSION}-linux-x86_64.zip
	go install google.golang.org/protobuf/cmd/protoc-gen-go

%.pb.go: %.proto
	tools/bin/protoc -Itools/include -I. --go_out=paths=source_relative:. $<
