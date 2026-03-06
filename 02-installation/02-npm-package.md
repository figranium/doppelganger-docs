# Installation via NPM (Package)

This guide covers installing figranium as a standalone NPM package. This is ideal for quickly testing figranium without cloning the repository or using Docker.

## Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended, v18+).
- [NPM](https://docs.npmjs.com/) or Yarn installed.

## Global Installation (Recommended)

To install figranium globally:

```bash
npm install -g @doppelgangerdev/doppelganger
```

### Running the CLI

Once installed, you can start the application using:

```bash
doppelganger
```

This will launch the figranium server on the default port (11345).

### Access the Application

Open your browser and navigate to:

[http://localhost:11345](http://localhost:11345)

## Running with NPX (Temporary/One-Off)

If you don't want to install figranium globally, you can run it directly using `npx`:

```bash
npx @doppelgangerdev/doppelganger
```

This will execute the latest version of figranium without a global installation.

## Customizing Configuration

You can customize the environment variables by passing them before the command:

```bash
PORT=8080 SESSION_SECRET=mysecret doppelganger
```

Or with `npx`:

```bash
PORT=8080 SESSION_SECRET=mysecret npx @doppelgangerdev/doppelganger
```

## Running Scripts (Advanced)

The NPM package also exposes specific scripts for different modes:

- **Scraper Mode**: `doppelganger --scrape` (Runs the high-performance scraper).
- **Agent Mode**: `doppelganger --agent` (Runs the full automation agent).

Additionally, you can run a debugging session:

- **Headful Execution**: `doppelganger --headful` (Opens the interactive browser for debugging).

For more details on CLI usage, see [CLI Tool Documentation](../06-api/02-cli-tool.md).
