## Define variables

# static variables
APP=rest-server-0
SOURCE=./...
CONF=local.toml
PKGPATH=github.com/lovemew67/cornerstone

# derived variables

# variables from shell
GOPATH=$(shell env | grep GOPATH | cut -d'=' -f 2)
REVISION=$(shell git rev-list -1 HEAD)
TAG=$(shell git tag --sort=-version:refname --points-at HEAD | head -n1)
BR=$(shell git rev-parse --abbrev-ref HEAD)
DATE=$(shell date -u +"%Y-%m-%dT%H:%M:%SZ")

# if-else blocks
ifeq ($(TAG),)
TAG=$(REVISION)
endif

# exported variables


## Define targets
vendor:
	- rm -f go.sum
	GO111MODULE=on go build -mod=mod -v $(SOURCE) 
	GO111MODULE=on go mod tidy

server: vendor
	go install -mod=mod -i -v -ldflags "-s -X $(PKGPATH).appName=$(APP) -X $(PKGPATH).gitCommit=$(REVISION) -X $(PKGPATH).appVersion=$(TAG) -X $(PKGPATH).buildDate=$(DATE)" $(SOURCE) 
	$(GOPATH)/bin/$(APP) server --config $(CONF) 
