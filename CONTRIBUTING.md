# Contributing to Ripple

## Development Guide

### Prerequisites

Please have the *latest* stable versions of the following on your machine

- node
- npm

### Local environment setup

We are using [Storybook](https://storybook.js.org/) as development environment
for UI components. It allows you to browse a component library, view the
different states of each component, and interactively develop and test components.

Without Docker and Bay, you can start the server as below. But we recommend you
to use [Docker](#work-in-docker) which provide docker container enviorment.

``` bash
# install dependencies
npm install

# Start the storybook server
npm start
```

#### Lint code

``` bash
# Boolean check if code conforms to linting rules - uses sass-lint, eslint & markdownlint
npm run lint
```

#### Test

``` bash
# We uses Jest for unit test and snapshots test
npm test
```

Before commit changes, run test first. If new Ripple components changed, we
should update snapshots by `npm test -- -u`. Then add it in commit.

#### Documentation

``` bash
# Generate README.md for all modules in `./packages/` directory
npm run docs
```

#### Updating ripple depdendencies

``` bash
# Update all ripple dependencies (./package.json & ./packages/**/package.json)
npm run package-dependencies
```

This script requires:

- Each ripple component package to have a `package.json` file with `name`
- The root directory to have a `lerna.json` file with `version`

#### Create new packages

``` bash
# Generate a new package in the `./packages/**/` directory
npm run new-package "[Name]" "[Description]" "[Atoms / Molecules / Organisms]"
```

Example: Creating a new package 'My Package' in the Organism folder:

``` bash
npm run new-package "My Package" "A demonstration package." "Organisms"
```

After creating a new package:

- Generate the readme using `npm run docs`.
- Update `package.json` by using `npm run package-dependencies`.

A `demoData.js` entry will need to be manually included.

### Work in Docker

We recomend you work in our Docker enviorment.

1. Install Docker
   - Install [Homebrew](https://brew.sh/)

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

   - Install docker `brew cask install docker`
   (You can also install it manually if you prefer - [https://www.docker.com/docker-mac](https://www.docker.com/docker-mac))
2. Start docker and you should be able to run `docker ps`
3. Checkout project repo and confirm the path is in docker's file sharing
    config - [https://docs.docker.com/docker-for-mac/#file-sharing](https://docs.docker.com/docker-for-mac/#file-sharing)
4. Make sure that `node`, `npm` & `pygmy` are installed
   - Install pygmy `gem install pygmy` (you might need sudo for this depending
     on your ruby configuration)
   - If you haven't installed `node` yet. Recommand to install `node` & `npm`
     by [`nvm`](https://github.com/creationix/nvm)
5. Make sure you don't have anything running on port 80 on the host machine
   (like a web server) then go to the project root run `pygmy up`
6. Run `npm run bay:start`
7. Once build has completed, you can run `npm run bay:logs -- --follow` to view
   the real-time logs.
8. If you want to ssh into the container, use `docker-compose exec ripple sh`

_If any steps fail you're safe to rerun from any point, starting again from the
beginning will just reconfirm the changes._

Local URL -- [http://ripple.docker.amazee.io/](http://ripple.docker.amazee.io/)

#### Available workflow commands

- `npm run bay:start` - build and start local development environment.
- `npm run bay:stop` - stop all Bay containers.
- `npm run bay:rebuild-full` - rebuild and start local development environment.
- `npm run bay:destroy` - stop and remove all Bay containers.
- `npm run bay:logs` - get logs from all running Bay containers.
- `npm run bay:cli` - run a command in `node` container.
   Example: `npm run bay:cli -- ls -al`.
- `npm run bay:pull` - pull latest Bay containers.
- `npm run bay:test` - Run tests.

#### Logs

Using the npm run helper script you can get logs from any running container.

`npm run bay:logs`

To continue streaming logs, use `--follow`.
`npm run bay:logs -- --follow`

You can also filter the output to show only logs from a particular service.
For example `npm run bay:logs -- ripple` will show the log output from the node container.
The full list of services can be found in the `docker-compose.yml`

#### SSHing into Ripple container

`docker-compose exec ripple sh`

## Directory Structure

### The `.storybook` Directory

Storybook configuration directory

### The `docs` Directory

Documents

### The `src` Directory

This directory contains custom components for storybook site use.

### The `packages` Directory

This directory contains Ripple components packages.

### The `static` Directory

**Assets for Ripple component should not be added in here.**

This directory contains static files for our storybook site. For example, images
used for demo purpose.

Then you can use the image in any `story.js` by path like `'/logo.svg'`.

### The `storybook-static` Directory

Auto generated by `build-storybook` for static app deployment.
