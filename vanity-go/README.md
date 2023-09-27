# VanityGO : Vanity import paths for Go package

[![Release 🎉](https://github.com/42Atomys/vanity-go/actions/workflows/release.yaml/badge.svg)](https://github.com/42Atomys/vanity-go/actions/workflows/release.yaml)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/42atomys/vanity-go?label=last%20release)
![GitHub contributors](https://img.shields.io/github/contributors/42Atomys/vanity-go?color=blueviolet)
![GitHub Repo stars](https://img.shields.io/github/stars/42atomys/vanity-go?color=blueviolet)
[![Docker Pull](https://img.shields.io/docker/pulls/atomys/vanity-go)](https://hub.docker.com/r/atomys/vanity-go)
[![Docker Pull](https://img.shields.io/docker/image-size/atomys/vanity-go)](https://hub.docker.com/r/atomys/vanity-go)

Simple go application that allows you to share your code with a custom domain name instead of github or gitlab links or other git protocols.

Say goodbye to `github.com/42Atomys/vanity-go` imports. Say hello to `atomys.codes/vanity-go` imports 🎉


When choosing a domain, keep in mind that it will be the name of your package for the foreseeable future, so choose a name that you’ll still like tomorrow.
People tend to choose domains with `.io`, `.codes` and `.dev` TLDs for their pacakges/software projects these days.

## Motivation

At the beginning to clarify my code especially with gitlab and subfolders (ex: `gitlab.com/subgroup-a/subgroup-b/subgroup-n/project`) importing files was not sexy. And a problem occurred when the folder architecture changed!

Error 404 in all directions, in all repositories. I created a classic `index.html` file but having to connect to a server to do vim (sorry emacs) is very annoying.

With [webhooked](https://github.com/42Atomys/webhooked) project, I told myself that I didn't want to redo everything, so I put this repo online

## Usage

### Step 1 : Configuration file
```yaml
# API Version also used to protect against API or Schema changes
# Actually, the available API versions are: 1
apiVersion: 1
# List of your proxies
# You can add as many proxies as you want with logic:
# 1 proxy per final domain
proxies:
- # namespace is the domain name used for following entries
  # This can be a subdomain, a domain or a full domain name
  # subdomain.example.org, example.org or example.org/subdomain
  namespace: atomys.codes
  # All entries of this namespace will be proxied to the following address
  # Key are the name and the entrypoint/path of your proxied packages
  # Value is the current URL of your package. The Destination URL must
  # end with a valid protocol.
  # Allowed protocol are: "bzr", "fossil", "git", "hg", "svn".
  entries:
    # Root redirection can be catch with "-" or "/" as key
    # Will responds to the following URL: atomys.codes
    -: https://github.com/42Atomys/vanity-go.git
    # Redirect go-get import to atomys.codes/vanity-go
    vanity-go: https://github.com/42Atomys/vanity-go.git
    # Redirect go-get import to atomys.codes/webhooked
    webhooked: https://github.com/42Atomys/webhooked.git
    # Redirect go-get import to atomys.codes/dns-updater
    dns-updater: https://github.com/42Atomys/dns-updater.git
    # Redirect go-get import to atomys.codes/subpath/gw2api-go
    sdk/gw2api-go: https://gitlab.com/Atomys/gw2api-go.git
```

### Step 2: Launch it 🚀

> **TIPS**: When you create your routing, configure it to only take into account the query params `go-get=1` to follow the GoLang directive (https://pkg.go.dev/cmd/go#hdr-Remote_import_paths)

### With Kubernetes

If you want to use kubernetes, for production or personnal use, refere to example/kubernetes:

https://github.com/42Atomys/vanity-go/tree/main/examples/kubernetes


### With Docker image

You can use the docker image [atomys/vanity-go](https://hub.docker.com/r/atomys/vanity-go) in a very simplistic way

```sh
# Basic launch instruction using the default configuration path
docker run -it --rm -p 8080:8080 -v ${PWD}/myconfig.yaml:/config/vanity.yaml atomys/vanity-go:latest
# Use custom configuration file
docker run -it --rm -p 8080:8080 -v ${PWD}/myconfig.yaml:/myconfig.yaml atomys/vanity-go:latest serve --config /myconfig.yaml
```

### With pre-builded binary

```sh
./vanity-go serve --config config.yaml -p 8080
```

## To-Do

TO-Do is moving on Project Section: https://github.com/42Atomys/vanity-go/projects?type=beta

# Contribution

All pull requests and issues on GitHub will welcome.

All contributions are welcome :)

## Thanks
