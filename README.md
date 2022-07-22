# Redwood

> **NOTICE:** RedwoodJS is very close to a stable version 1.0. In the last two years,
> the project has matured significantly and is already used in production by a number
> of startups. We intend to have a 1.0 release candidate before the end of 2021 and
> to release a truly production-ready 1.0 in early 2022.

## Getting Started
- [Tutorial](https://redwoodjs.com/tutorial/welcome-to-redwood): getting started and complete overview guide.
- [Docs](https://redwoodjs.com/docs/introduction): using the Redwood Router, handling assets and files, list of command-line tools, and more.
- [Redwood Community](https://community.redwoodjs.com): get help, share tips and tricks, and collaborate on everything about RedwoodJS.

### Setup

We use Yarn as our package manager. To get the dependencies installed, just do this in the root directory:

```terminal
yarn install
```

### Fire it up

```terminal
yarn redwood dev
```

Your browser should open automatically to `http://localhost:8910` to see the web app. Lambda functions run on `http://localhost:8911` and are also proxied to `http://localhost:8910/.redwood/functions/*`.

## Using VSCode Dev Containers

If you are using VSCode Dev Containers or Github Codespaces you will need to update the `schema.prisma` file to connect to the postgres database container for development and testing. Your `datasource db` should look like the following:

```js
datasource db {
  provider = "postgresql" // Switched to Postgres for local development
  url      = env("DATABASE_URL")
}

...
// The rest of the file
```

Next, update your .env file. Since we changed to using Postgres, change `DATABASE_URL` and `TEST_DATABASE_URL` to point to the postgres database containers and use the credentials that are set in the docker-compose.yml. Another important bit is to set the `RWJS_DEV_API_URL` variable so routing happens properly from within our container to the GQL server.

```ini
# THIS FILE SHOULD NOT BE CHECKED INTO YOUR VERSION CONTROL SYSTEM
#
# Environment variables set here will override those in .env.defaults.
# Any environment variables you need in production you will need to setup with
# your hosting provider. For example in Netlify you can add environment
# variables in Settings > Build & Deploy > environment

DATABASE_URL=postgres://postgres:postgres@localhost:5432/development_db
TEST_DATABASE_URL=postgres://postgres:postgres@localhost:5432/test_db

# Sets an app-specific secret used to sign and verify your own app's webhooks.
# For example if you schedule a cron job with a signed payload that later will
# then invoke your api-side webhook function you will use this secret to sign and the verify.
# Important: Please change this default to a strong password or other secret
# WEBHOOK_SECRET=THIS_IS_NOT_SECRET_PLEASE_CHANGE
# Set API base URL to be localhost, not 0.0.0.0
RWJS_DEV_API_URL=http://localhost
```
