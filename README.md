# 🐋 Cloudflare React + Vite + Hono + Cloudflare Workers with Docker Compose

This is a development setup with docker compose for the [Vite React Template](https://github.com/cloudflare/templates/tree/main/vite-react-template).

> [!TIP]
> While this example shows the Vite React template, the principles on how to use Docker Compose can be applied for any other template as well.

## 🛠️ Prerequisites

* [Docker Compose](https://docs.docker.com/compose/install/)
* [Task (optional)](https://taskfile.dev/installation/)

## 📜 Usage

### First time

1. Copy `.env.dev.example` to `.env.dev`.

	```shell
	task init
	```

> [!NOTE]
> - The `.env.dev` file is used for development purposes, and can include variables/secrets like `CLOUDFLARE_API_TOKEN`, and will **not** be parsed for wrangler types.

2. Install dependencies before starting the container.

	```shell
	task npm:install
	```

3. Start the container.

	```shell
	task up
	```

4. Access the UI at [`http://localhost:8789`](http://localhost:8789).

🚀 **TLDR**

Initialize the project, install dependencies, and start the container.

```shell
task setup
```

### 🐚 Additional commands

#### NPM

##### Install

Install NPM dependencies.

```shell
task npm:install
```

##### Update

Update NPM dependencies.

```shell
task npm:update
```

#### Compose

##### Up

Start vite dev server.

```shell
task up
```

Build and start vite preview server.

```shell
task up:preview
```

##### Down

Stop and remove the container.

```shell
task down
```

##### Logs

View container logs.

```shell
task logs
```

#### Wrangler

##### Types

Generate wrangler types.

```shell
task wrangler:types
```

##### Deploy

Deploy to Cloudflare Workers.

```shell
task wrangler:deploy
```

> [!IMPORTANT]  
> This requires the `CLOUDFLARE_API_TOKEN` to be set in the `.env` file.

##### Secret

Upload secret.

```shell
task wrangler:secret s=<NAME_OF_SECRET>
# Example
task wrangler:secret s=API_KEY
```

> [!IMPORTANT]
> - This requires the `CLOUDFLARE_API_TOKEN` to be set in the `.env` file.
> - You will be prompted to enter the secret value.

#### Biome

##### Format

Run biome format with safe fixes.

```shell
task biome:format:fix
```

##### Lint

Run biome lint with safe fixes.

```shell
task biome:lint:fix
```

##### Check

Run biome check with safe fixes.

```shell
task biome:check:fix
```

## 🧑‍🏫 Good to know

- The current development setup uses [Vite](https://vite.dev/) with the [`@cloudflare/vite-plugin`](https://www.npmjs.com/package/@cloudflare/vite-plugin).
- The base image for the docker compose worker service is `node:24-slim`.
- There is a Github action that releases a new version of the worker when pushed to `main` (or manual workflow dispatch).
	- The action uses `cloudflare/wrangler-action@v3` but has the `wranglerVersion` explicitly set to match the version in the `package.json` (v4).
	- By default, the [`release.yml`](.github/workflows/release.yml) has `WRANGLER_QUIET` set to `true` and `SHOW_DEPLOYMENT_URL` set to `false`, which will hide the deployment URL from the logs.

## 🛠️ Contribute

### Requirements

* ☑️ [Pre-commit](https://pre-commit.com/#installation).
* 📋 [Task (optional)](https://taskfile.dev/installation/)

### Usage

Run `pre-commit install` or `task precommit:install` to install the pre-commit hooks.

## ❕ Licence

This repository comes with a [MIT license](./LICENSE).
