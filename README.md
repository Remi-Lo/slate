# Developing the Timegrip System Documentation and API Reference

Some contents of this chapter have been copied from the [Using Slate in Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker) documentation on the [Slate Wiki](https://github.com/slatedocs/slate/wiki). 

This guide assumes you follow the guide in the [Dependencies](#dependencies) below to install Docker Desktop on a supported Linux-capable system. Afterwards, you could for instance be running [Ubuntu](https://ubuntu.com/) in the [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) using [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/about) (WSL). In that case you'd be using the dropdown menu in the tabs to change to your Ubuntu terminal profile.

You'll need the _Timegrip System Documentation and API Reference_ repository, a Slate repository, the Slate image, a container you build yourself, and a running instance of said container when developing. Se the [Getting started](#getting-started), 


## Slate usage

Provided in the slate repo is a Dockerfile you can use to run slate using [Docker](https://www.docker.com/), as well as providing pre-built images on [Docker Hub](https://hub.docker.com/r/slatedocs/slate). Docker is similar to Vagrant in that it provides a reproducible, portable development environment using virtualization, however it does not provide a full VM, rather piggy backing off the host, allowing for a slimmer installation profile than Vagrant / full VMs. However, Docker does come with a number of its own terms, and for beginners, we recommend looking at
[this Glossary](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/docker-terminology)
to familiarize yourself with some of them.


## Dependencies

* [Docker](https://www.docker.com/), see [this page](https://www.docker.com/get-started) for installing Docker Desktop.


## Getting Started

### Timegrip Timegrip System Documentation and API Reference

Clone the [api_docs](https://bitbucket.org/timegrip/api_docs/) from the Timegrip Bitbucket to your harddrive.

The api_docs repository contains the source files you will be editing when documenting. This guide assumes the resulting api_docs and slate directories share the same parent directory after cloning.


### Slate

1. Fork the [slatedocs](https://github.com/slatedocs) repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
   * You can aslo use `git clone https://github.com/Remi-Lo/slate.git` if you don't intend to customize the Slate installation.
   * Use the official Slate repository to get the latest Slate version as well when pulling from it.
   * Otherwise use your _own forked repository_ if you want to sync the repository yourself and make it custom.
3. `cd slate`
4. Grab the slate image (`docker pull slatedocs/slate`) or build the docker image for the repository (`docker build . -t slatedocs/slate`).

#### Notes



If you are using the pre-built images for Slate, you may wish to remove all files other than the `source` directory from your repository.


## Building Slate

To use Docker to just build your site, run:

```
docker run --rm --name slate -v $(pwd)/build:/srv/slate/build -v $(pwd)/../api_docs/source:/srv/slate/source slatedocs/slate build
```

After this command completes, you should see the built artifacts for your site in the `$(pwd)/build` directory, which you can then statically serve for your website.

_Note_: You may omit the final `build` argument and get the same result. By default, if given no command, the Dockerfile will run `build`.


## Running Slate

If you wish to run the development server for Slate to aid in working on the site, run:

```
docker run --rm --name slate -p 4567:4567 -v $(pwd)/../api_docs/source:/srv/slate/source slatedocs/slate serve
```

and you will be able to access your site at http://localhost:4567 until you stop the running container process.


## Further reading

See the official Slate repository for:

* [Advanced usage of Slate in Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker#advanced-usage)
* [Next steps to creating documentation](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker#what-now)
* [An introduction to Slate](https://github.com/slatedocs/slate#readme)
* And other Slate topics
