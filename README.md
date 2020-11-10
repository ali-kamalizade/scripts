# Things to make my (and your?) life easier

This is a collection of reusable scripts, functions and [aliases](https://en.wikipedia.org/wiki/Alias_(Mac_OS)) related to development.

## Bash

### Open `.bash_profile` in Visual Studio Code
```
alias edit-bash-profile="code ~/.bash_profile"
```

### Apply changes made in `.bash_profile` without restarting your terminal
```
alias refresh-bash="source ~/.bash_profile"
```

### Shortcut for home directory

```
alias home="cd ~"
```

## JavaScript

### List globally installed NPM packages

```
alias npm-global-packages="npm list -g --depth 0"
```

### Fix auto-fixable issues in TSLint

```
alias tslint-fix=" npx tslint --fix --project ./"
```

### Clear cache of Jest test runner

```
alias jest-clear-cache="npx jest --clearCache"
```

### Check JavaScript bundles for ES5 compatibility

```
check_es_bundles() {
  echo "Checking bundles in" $1 "for ES5 compatibility."
  npx es-check es5 $1 --verbose
}
```

### Compile TypeScript

```
compile_typescript() {
  echo "Compiling TypeScript using the following configuration file:" $1
  npx tsc -p $1
}
```

### Run a local HTTP server

```
run_http_server() {
  echo "Running HTTP server on port" $1 ". Serving the following directory:" $2
  npx http-server -p $1 -c-1 $2
}
```

## Git

### Stash single file

```
alias git-stash-single-file="git stash push "
```

### Print current branch name

```
git rev-parse --abbrev-ref HEAD
```

## Utilities / Miscellaneous

### Kill process running on a specific port

```
kill_process_by_port() {
  lsof -i TCP:$1 | grep LISTEN | awk '{print $2}' | xargs kill -9
  echo "Port" $1 "found and killed."
}
```

### Convert a post on Medium.com to Markdown

```
medium_post_to_markdown() {
    cd ~/Desktop
    npx mediumexporter "$1" > medium_post.md
}
```
