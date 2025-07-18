# CDP Node.js Prototype Template

`Node.js` prototype template, using the [GOV.UK Prototype Kit](https://github.com/alphagov/govuk-prototype-kit).
Basically the `GOV.UK Prototype Kit` with `CDP` running capabilities.

- [Requirements](#requirements)
  - [Node.js](#nodejs)
- [Environment Variables](#environment-variables)
  - [Local](#local)
  - [CDP Environment's](#cdp-environments)
  - [Secrets](#secrets)
  - [GOV.UK Prototype Kit](#govuk-prototype-kit)
- [Creating a secret](#creating-a-secret)
- [Setting a password for a prototype](#setting-a-password-for-a-prototype)
- [Setting multiple passwords](#setting-multiple-passwords)
- [Update dependencies](#update-dependencies)
- [Docker](#docker)
  - [Development image](#development-image)
  - [Production image](#production-image)
  - [Debug docker](#debug-docker)
- [Npm scripts](#npm-scripts)
  - [Formatting](#formatting)
    - [Windows prettier issue](#windows-prettier-issue)
- [Licence](#licence)
  - [About the licence](#about-the-licence)

## Requirements

### Node.js

Please install [Node.js](http://nodejs.org/) `>= v22` and [npm](https://nodejs.org/) `>= v11`. You will find it
easier to use the Node Version Manager [nvm](https://github.com/creationix/nvm)

To use the correct version of Node.js for this application, via nvm:

```bash
cd cdp-node-prototype-template
nvm use
```

## Environment Variables

Environment variables and Secrets are used to configure the application in your prototype.

- Sensitive secrets and non-sensitive Environment variables can be set in a `.env` file for local development
- Sensitive secrets can be set in the CDP Portal Frontend when your prototype is being run on a CDP environment
- Non-sensitive environment variables can be set in the CDP App Config repository when your prototype is being run on a
  CDP environment

### Local

> [!CAUTION]
> Do not store passwords in the `.env` file. Or in GitHub. Sensitive information such as a password can be password to
> a prototype via the Secrets page in the CDP Portal Frontend. `.env` is for local development only

To use environment variables locally copy the [.env.template](./.env.template) file to `.env` and add any environment
variables or secrets your local environment needs.

### CDP Environment's

To add environment variables read - https://github.com/DEFRA/cdp-documentation/blob/main/how-to/config.md. This will
guide you to add non-sensitive environment variables to the https://github.com/DEFRA/cdp-app-config repository via a
pull request.

### Secrets

To add sensitive environment variables for your prototype. Add them via your prototypes secrets page on the Core
Delivery Platform Portal

### GOV.UK Prototype Kit

- For information on the `GOV.UK Prototype Kit` see https://prototype-kit.service.gov.uk/docs/
- To view the code in the `GOV.UK Prototype Kit` see https://github.com/alphagov/govuk-prototype-kit
- For tutorials on how to use the `GOV.UK Prototype Kit`
  see https://prototype-kit.service.gov.uk/docs/tutorials-and-guides
- For help with using the `GOV.UK Prototype Kit` on the Core Delivery Platform come and chat with us in `#cdp-support`

The following environment variables are available in the `GOV.UK Prototype Kit`. For more information see their docs or
the GitHub repository listed above.

```markdown
| Name                  | Value     | Description                                              |
| --------------------- | --------- | -------------------------------------------------------- |
| `PASSWORD`            | `string`  | Password for basic authentication                        |
| `PASSWORD_KEYS`       | `string`  | Comma-separated list of keys for password authentication |
```

## Creating a secret

1. Go to the CDP Portal Frontend
1. Navigate to your prototype on the services list page
1. Navigate to yhe `Secrets` tab
1. Add a secret on your chosen environment with a name and value of your choosing
1. Re-deploy your prototype for the changes to take effect

## Setting a password for a prototype

> [!CAUTION]
> Do not commit the `.env` file to GitHub, it is in the `.gitignore` file by default. Sensitive information such as a
> password can be passed to a prototype via the Secrets page of your prototype in the CDP Portal Frontend

Basic authentication is on by default in CDP environments, so you will need to set a password for your prototype. You
can do this via the secrets tab in the Portal Frontend. For information on how to do this, follow these steps:

1. Read https://prototype-kit.service.gov.uk/docs/publishing
1. Go to the CDP Portal Frontend
1. Navigate to your prototype on the services list page
1. Navigate to yhe `Secrets` tab
1. Add a secret with a name `PASSWORD` and a value of your choosing
1. Re-deploy your prototype for the changes to take effect

## Setting multiple passwords

The `GOV.UK Prototype Kit` has the ability to set up multiple passwords via secrets. For more information on how to do
this read the `If you want to create additional passwords` section on
https://prototype-kit.service.gov.uk/docs/publishing. To add a secret to an environment your prototype is running in
see [Creating a secret](#creating-a-secret)

## Update dependencies

To update dependencies use [npm-check-updates](https://github.com/raineorshine/npm-check-updates):

> The following script is a good start. Check out all the options on
> the [npm-check-updates](https://github.com/raineorshine/npm-check-updates)

```bash
ncu --interactive --format group
```

## Docker

### Development image

Build:

```bash
docker build --target development --no-cache --tag cdp-node-prototype-template:development .
```

Run:

```bash
docker run -e PORT=3000 -p 3000:3000 cdp-node-prototype-template:development
```

### Production image

Build:

```bash
docker build --no-cache --tag cdp-node-prototype-template .
```

Run:

> Update the password field

```bash
docker run -e PASSWORD=beepBoopBeep -e PORT=3000 -p 3000:3000 cdp-node-prototype-template
```

### Debug docker

To debug issues in docker and to have a look at the built docker container in the same way as when it runs on CDP. You
can run an interactive shell:

Build:

```bash
docker build --no-cache --tag cdp-node-prototype-template .
```

Run:

```bash
docker run -it --entrypoint /bin/ash cdp-node-prototype-template
```

## Npm scripts

All available Npm scripts can be seen in [package.json](./package.json)
To view them in your command line run:

```bash
npm run
```

### Formatting

#### Windows prettier issue

If you are having issues with formatting of line breaks on Windows update your global git config by running:

```bash
git config --global core.autocrlf false
```

## Licence

THIS INFORMATION IS LICENSED UNDER THE CONDITIONS OF THE OPEN GOVERNMENT LICENCE found at:

<http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3>

The following attribution statement MUST be cited in your products and applications when using this information.

> Contains public sector information licensed under the Open Government license v3

### About the licence

The Open Government Licence (OGL) was developed by the Controller of Her Majesty's Stationery Office (HMSO) to enable
information providers in the public sector to license the use and re-use of their information under a common open
licence.

It is designed to encourage use and re-use of information freely and flexibly, with only a few conditions.
