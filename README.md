Some contents of this chapter have been copied from the [Using Slate in Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker) documentation on the [Slate Wiki](https://github.com/slatedocs/slate/wiki). 

This guide assumes you are using a Docker-supported Linux-capable system. You could for instance be running [Ubuntu](https://ubuntu.com/) in the [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) using [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/about) (WSL). In that case you'd be using the dropdown menu in the tab bar to change to your _Ubuntu_ terminal profile.


# Dependencies

**[Docker](https://www.docker.com/):** See [this page](https://www.docker.com/get-started) for installing Docker Desktop.

**Slate:**

1. Go to the directory where you wish to store _slate_ and the documentation files. E.g. `cd /mnt/e/`.
2. Clone the [Slate repository](https://github.com/slatedocs) to your hard drive with `git clone https://github.com/slatedocs/slate.git`.
   * You can also use `git clone https://github.com/Remi-Lo/slate.git` but it might be out of sync when pulling.
   * If you intend to create a custom version of Slate:
      * Fork the [slatedocs](https://github.com/slatedocs) repository on GitHub before cloning.
      * Use `git clone https://github.com/YOURGITHUBUSERNAME/slate.git` when cloning to your hard-drive.
3. Go to the _slate_ directory (`cd slate`).
4. Grab the slate image (`docker pull slatedocs/slate`) or build the docker image for the repository (`docker build . -t slatedocs/slate`). 
5. Go to the parent directory (`cd ..`).

Note: If you are using the pre-built images for Slate, you may wish to remove all files other than the `source` directory from your repository.


# Documentation source files

1. Go to where the _slate_ directory is stored (eg. `cd /mnt/e/`).
2. Visit the [api_docs](https://bitbucket.org/timegrip/api_docs/) repository on the Timegrip Bitbucket
3. Click Clone and copy the git clone command.
4. Run the command in the terminal:
   * E.g. `git clone https://YOURBITBUCKETUSERNAME@bitbucket.org/timegrip/api_docs.git`.



# Building

To use Docker to build your site, run the following command but modify `cd /mnt/e/` to be where the _slate_ directory is stored first (eg. `/mnt/c/containers/`):

```
cd /mnt/e/ & docker run --rm --name slate -v $(pwd)/slate/build:/srv/slate/build -v $(pwd)/api_docs/source:/srv/slate/source slatedocs/slate build
```

After this command completes, you should see the built artifacts for your site in the `$(pwd)/build` directory, which you can then statically serve for your website.

_Note_: You may omit the final `build` argument and get the same result. By default, if given no command, the Dockerfile will run `build`.


# Running

If you wish to run the development server for Slate to aid in working on the site, run:

```
docker run --rm --name slate -p 4567:4567 -v $(pwd)/api_docs/source:/srv/slate/source slatedocs/slate serve
```

and you will be able to access your site at http://localhost:4567 until you stop the running container process.


## Further reading

See the official Slate repository for:

* [Usage of Slate in Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker)
* [Advanced usage of Slate in Docker](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker#advanced-usage)
* [Next steps to creating documentation](https://github.com/slatedocs/slate/wiki/Using-Slate-in-Docker#what-now)
* [An introduction to Slate](https://github.com/slatedocs/slate#readme)
* And other Slate topics
