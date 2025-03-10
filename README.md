# Source for nixos.org

[![GitHub Workflow Status of master branch](https://img.shields.io/github/workflow/status/nixos/nixos-homepage/Build%20&%20Deploy%20to%20Netlify?style=flat)](https://github.com/NixOS/nixos-homepage/actions?query=workflow%3A%22Build+%26+Deploy+to+Netlify%22) [![Number of open GitHub issues](https://img.shields.io/github/issues/nixos/nixos-homepage?style=flat&color=red)](https://github.com/nixos/nixos-homepage/issues) [![Number of open GitHub pull requests](https://img.shields.io/github/issues-pr/nixos/nixos-homepage?style=flat&color=blue)](https://github.com/nixos/nixos-homepage/pulls) [![Month of last commit](https://img.shields.io/github/last-commit/NixOS/nixos-homepage?style=flat)](https://github.com/NixOS/nixos-homepage/commits/master) [![Number of all contributors](https://img.shields.io/badge/all_contributors-10-orange.svg?style=flat)](https://github.com/nixos/nixos-homepage#how-to-help)

Code and content for the [nixos.org](https://nixos.org) website.


# Help us!

There are many ways how you can help:

- if you are familiar with CSS look at the [issues tagged with `design` tag](https://github.com/NixOS/nixos-homepage/issues?q=is%3Aissue+is%3Aopen+label%3Adesign).
- if you are an native English speaker or just a person that is very good with words, please look at the [issues tagged with `content` tag](https://github.com/NixOS/nixos-homepage/issues?q=is%3Aissue+is%3Aopen+label%3Acontent)
- if you are developer and just eager to fix stuff please look at the [issues tagged with `bug` tag](https://github.com/NixOS/nixos-homepage/issues?q=is%3Aissue+is%3Aopen+label%3Abug)

If you feel lost where and how to contribute, ask the [marketing team](https://nixos.org/community/teams/marketing.html) on the [`#marketing` room on Matrix](https://matrix.to/#/#marketing:nixos.org).


# How to help?

To run local development instance follow this steps:

    $ git clone git@github.com:NixOS/nixos-homepage.git
    $ cd nixos-homepage
    $ nix-shell

      To start developing run:
          serve

      and open browser on:
          https://localhost:8000

      It will rebuild the website on each change.

    [nix-shell]$ serve

Open your browser at: http://localhost:8000/

In order for the browser to automatically refresh, install the [Livereload extension](http://livereload.com/extensions/) for your browser.

Before creating a pull request make sure that `nix-build` runs successfully.


## Binary cache (Optional)

It can take some time to enter the development environment. To speed up and avoid building from source, you can use a binary cache. The same cache is used to speed up our GitHub Actions.

### On NixOS

Add the following to your `configuration.nix`:

```
nix.binaryCaches = [ "https://nixos-homepage.cachix.org" ];
nix.binaryCachePublicKeys = [ "nixos-homepage.cachix.org-1:NHKBt7NjLcWfgkX4OR72q7LVldKJe/JOsfIWFDAn/tE=" ];
```

### On non-NixOS

Add the following to the `/etc/nix/nix.conf` or `~/.config/nix/nix.conf`:

```
substituters = ... https://nixos-homepage.cachix.org
trusted-public-keys = ... nixos-homepage.cachix.org-1:NHKBt7NjLcWfgkX4OR72q7LVldKJe/JOsfIWFDAn/tE=
```

## Development under MacOS (via Docker)

The website cannot be served natively but with the help of [docker](https://www.docker.com/products/docker-desktop).
(You may need to increase the maximum "Disk image size" in Docker's Resources Preferences.)

1. Pull in the latest nixos container image from [dockerhub](https://hub.docker.com/r/nixos/nix)

    `$ docker pull nixos/nix`

2. Start and enter a container:

    `$ docker run -p 8000:8000 -it --name nixos-homepage nixos/nix`

3. Having entr, fd and vim at place is helpful for automatic rebuilds of the site and enabling a binary cache.

    `nix-shell -p entr fd vim`

3. Enable usage of binary cache to speed up the remaining process as been described in [On non-NixOs](https://github.com/NixOS/nixos-homepage#on-non-nixos)

4. Following with the same steps as on Linux/NixOS:

    ```
    $ git clone https://github.com/NixOS/nixos-homepage.git
    $ cd nixos-homepage
    $ nix-shell
    [nix-shell]$ make
    ```

5. Add the `--bind 0.0.0.0` argument to bind the web server with the container's external interface too:

    `[nix-shell]$ python -m http.server --bind 0.0.0.0`

6. Visit http://127.0.0.1:8000 in your browser. To continuously rebuild on any changes:

    `[nix-shell]$ fd | entr make`

## License

The content of the website is licensed under the [Creative Commons Attribution Share Alike 4.0 International](LICENSES/CC-BY-SA-4.0.txt) license.

The software (including sample code) is licensed under the [MIT](LICENSES/MIT.txt) license.

Some files might have a different license. See the files content for details.
