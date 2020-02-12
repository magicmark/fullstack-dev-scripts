![Fullstack Dev Scripts](logo.gif)

A collection of scripts/snippets/cheat sheets to use during full stack development.

---

## npm/yarn package managment

### list all top level JS dependencies

```sh
jq -r '.dependencies , .devDependencies | to_entries | .[] | .key' package.json | tr '\n' ' '
```

#### With versions:

```sh
jq -r '.dependencies | to_entries[] | .key as $k | .value as $v | "\($k)@\($v)"' package.json | tr '\n' ' '
```

## find all yarn linked packages

```sh
find node_modules -maxdepth 1 -type l -ls
```

## Bash

### killing all processes related to X

This is usually a super bad idea. Probably don't run this, unless you're feeling super lazy.

```sh
ps fux | grep my_service_here | tr -s ' ' | cut -d' ' -f2 | xargs kill
```

### change the value of a constant in a directory

```sh
find /path/to/directory type f -name "*.yaml" | xargs -I{} sed -i -e 's/mem: 2800/mem: 4096/g' {}
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
docker run -t -i --rm ubuntu bash
```
