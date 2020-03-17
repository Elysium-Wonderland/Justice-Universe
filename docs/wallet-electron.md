# Build Guide

> Step 1 ~ 3 are only required in the first time

### Step 1: Install Node.js

Please refer to the [Official Guide](https://nodejs.org/en/download/)

### Step 2: Install vue-cli

```shell
npm install -g vue-cli
```

### Step 3: Git clone wallet source code from github

```shell
git clone https://github.com/Elysium-Wonderland/just-wallet-electron.git
```

### Step 4: Install dependency

cd to the directory and run:

```shell
npm install
```

### Step 5: Update the justd RPC url

Open the config file: src/renderer/config/application.json

Change the rpcUrl to the proper justd RPC url

### Step 6: Build app for Windows/Mac

Build exe for Windows:

```shell
npm run win
```

Build dmg for Mac:

```shell
npm run mac
```

> dmg file cannot be built in windows system.

The exe/dmg files are generated in build/ directory.
