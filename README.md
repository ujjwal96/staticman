<img src="logo.png" width="300">

# Staticman [![coverage](https://img.shields.io/badge/coverage-83%25-yellow.svg?style=flat?style=flat-square)](https://github.com/eduardoboucas/staticman) [![Build Status](https://travis-ci.org/eduardoboucas/staticman.svg?branch=master)](https://travis-ci.org/eduardoboucas/staticman) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

> Static sites with superpowers

## Introduction

Staticman is a Node.js application that receives user-generated content and uploads it as data files to a GitHub repository. In practice, this allows you to have dynamic content (e.g. blog post comments) as part of a fully static website, as long as your site automatically deploys on every push to GitHub, as seen on [GitHub Pages](https://pages.github.com/), [Netlify](http://netlify.com/) and others.

It consists of a small web service that handles the `POST` requests from your forms, runs various forms of validation and manipulation defined by you and finally pushes them to your repository as data files. You can choose to enable moderation, which means files will be pushed to a separate branch and a pull request will be created for your approval, or disable it completely, meaning that files will be pushed to the main branch automatically.

You can download and run the Staticman API on your own infrastructure, or you can simply use the public instance of the Staticman API for free. If using the public instance, you can skip to *[Setting up repository](#setting-up-a-repository)*.

## Requirements

- Node.js 4.8.3+
- npm
- A [personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) for the GitHub account you want to run Staticman with
- An SSH key (click [here](https://help.github.com/articles/connecting-to-github-with-ssh/) to learn how to create one)

## Setting up the server

- Clone the repository and install the dependencies via npm.

  ```
  git clone git@github.com:eduardoboucas/staticman.git
  cd staticman
  npm install
  ```

- Create a development config file from the sample file.

  ```
  cp config.sample.json config.development.json
  ```

- Edit the newly-created config file with your GitHub access token, SSH private key and the port to run the server. Click [here](https://staticman.net/docs/api) for the list of available configuration parameters.

- Start the server.

  ```
  npm start
  ```

Each environment, determined by the `NODE_ENV` environment variable, requires its own configuration file. When you're ready to push your Staticman API live, create a `config.production.json` file before deploying.

Check [this guide](docs/docker.md) if you're using Docker.

## Setting up a repository

Staticman runs as a bot using a GitHub account, as opposed to accessing your account using the traditional OAuth flow. This means that you can give it access to just the repositories you're planning on using it on, instead of exposing all your repositories.

To add Staticman to a repository, you need to add the bot as a collaborator with write access to the repository and ask the bot to accept the invite by firing a `GET` request to this URL:

```
http://your-staticman-url/v2/connect/GITHUB-USERNAME/GITHUB-REPOSITORY
```

If you're using the public instance, the account you want to add is [staticmanapp](https://github.com/staticmanapp) and the URL is https://api.staticman.net/v2/connect/GITHUB-USERNAME/GITHUB-REPOSITORY.

## Site configuration

Staticman will look for a config file. For the deprecated `v1` endpoints, this is a  `_config.yml` with a `staticman` property inside; for `v2` endpoints, Staticman looks for a `staticman.yml` file at the root of the repository.

For a list of available configuration parameters, please refer to the [documentation page](https://staticman.net/docs/configuration).

## Development

Would you like to contribute to Staticman? That's great! Here's how:

1. Read the [contributing guidelines](CONTRIBUTING.md)
1. Pull the repository and start hacking
1. Make sure tests are passing by running `npm test`
1. Send a pull request and celebrate

## Sites using Staticman

- [Popcorn](http://popcorn.staticman.net) ([Source](https://github.com/eduardoboucas/popcorn))
- [eduardoboucas.com](https://eduardoboucas.com) ([Source](https://github.com/eduardoboucas/eduardoboucas.github.io))
- [Made Mistakes](https://mademistakes.com/) ([Source](https://github.com/mmistakes/made-mistakes-jekyll))
- [Minimal Mistakes theme](https://mmistakes.github.io/minimal-mistakes/) ([Source](https://github.com/mmistakes/minimal-mistakes))
- [/wg/ Startpages](http://startpages.cf/) ([Source](https://github.com/twentytwoo/startpages.cf))
- [movw-0x16.cf](http://movw-0x16.cf/) ([Source](https://github.com/twentytwoo/movw-0x16))
- [Open Source Design Job Board](http://opensourcedesign.net/jobs/) ([Source](https://github.com/opensourcedesign/jobs/))
- [zongren.me](https://zongren.me/) ([Source](https://gitlab.com/zongren/zongren.gitlab.io/)) 
- [DOTSLASHLINUX](http://www.dotslashlinux.com/) ([Source](https://github.com/firasuke/DOTSLASHLINUX/))
- [Spinningnumbers.org](http://spinningnumbers.org/) ([Source](https://github.com/willymcallister/spinningnumbers))
- [blog.justin.kelly.org.au](https://blog.justin.kelly.org.au/) ([Source](github.com/justinkelly/justinkelly.github.io))
- [chimad-phase-field](https://pages.nist.gov/chimad-phase-field/) ([Source](https://github.com/usnistgov/chimad-phase-field))
- [abhinavsarkar.net](https://abhinavsarkar.net) ([Source](https://github.com/abhin4v/abhin4v.github.io/))

Are you using Staticman? [Let us know!](https://github.com/eduardoboucas/staticman/edit/master/README.md)
