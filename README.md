# ![Fullstack Dev Scripts](logo.gif)

A collection of scripts/snippets/etc I use during full stack development.

_(I still use [tldr pages](https://tldr.sh/) as a cheat sheet for specific tooling examples. This repo is intended to contain scripts to achieve certain goals, and not as a generic reference for any particular toolset.)_

## npm/yarn package managment

### list all top level JS dependencies

```sh
jq -r '.dependencies , .devDependencies | to_entries | .[] | .key' package.json | tr '\n' ' '
```

#### With versions:

```sh
jq -r '.dependencies | to_entries[] | .key as $k | .value as $v | "\($k)@\($v)"' package.json | tr '\n' ' '
```

## find all linked packages

```sh
find node_modules -maxdepth 1 -type l -ls
```

## JavaScript 

#### CLI Script

```js
#!/usr/bin/env node

/**
 * @file Tool to do stuff
 *
 * Usage:
 *
 *   $ ./path/to/script <foo> <bar>
 */

async function main({ foo, bar }) {
    // do stuff
}

if (!process.env.NODE_ENV && require.main === module) {
    const [ , , foo, bar] = process.argv;
    
    main({ foo, bar }).catch(e => {
        console.error('\n======= Error caught in ./path/to/my/script =======');
        console.error(e);
        process.exit(1);
    });
}
```

## Bash

### killing all processes related to X

This is usually a super bad idea. Probably don't run this, unless you're feeling super lazy.

```sh
ps fux | grep my_service_here | tr -s ' ' | cut -d' ' -f2 | xargs kill
```

### change the value of a constant in a directory

```sh
find /path/to/directory -type f -name "*.yaml" | xargs -I{} sed -i -e 's/mem: 2800/mem: 4096/g' {}
```

### `tree` (with ignored directories)

```bash
tree -a -I 'node_modules|\.git'
```

### bash script

```bash
#!/bin/bash
set -euo pipefail

# https://stackoverflow.com/a/246128/4396258
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd )"
ROOT="${DIR}/.."

if [ "$#" -ne 1 ]
then
    echo '/path/to/script <foo>'
    exit 1;
fi

FOO="$1"
echo $FOO
```
## Docker

### run a hello world docker container (with cleanup)

```sh
docker run -it --rm ubuntu bash
```

### build & run a container

```sh
docker build -t myapp1 .
docker run -it --rm --name app-instance myapp1
```
