# Helpers to make my (and your?) life easier

This is a collection of reusable scripts, functions and [aliases](https://en.wikipedia.org/wiki/Alias_(Mac_OS)) related to software development.

## Bash

### Open `.bash_profile` in Visual Studio Code
```
alias edit-bash-profile="code ~/.bash_profile"
```

### Apply changes made in `.bash_profile` without restarting your terminal
```
alias refresh-bash="source ~/.bash_profile"
```

### Execute a command multiple times

```
run_multiple_times() {
  echo "Executing" "the following command" $1 "times:" $2
  for i in $(seq 1 $1);
    do $2;
  done;
}
```

### Shortcut for home directory

```
alias home="cd ~"
```

## JavaScript & TypeScript

### List globally installed NPM packages

```
alias npm-global-packages="npm list -g --depth 0"
```

### Fix auto-fixable issues in TSLint

```
alias tslint-fix=" npx tslint --fix --project ./"
```

### Generate a `tsconfig.json` file

```
alias tslint-fix=" npx tsc --init"
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

### Find publicly known security vulnerabilities in a website's frontend JavaScript libraries using [Snyk](https://snyk.io)

```
run_snyk_check() {
  echo "Running Snyk check for website:" $1
  npx is-website-vulnerable $1
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
alias git-branch-name='git rev-parse --abbrev-ref HEAD'
```

### Amend staged files

```
alias git-ammend='git commit --amend'
```

### Undo last commit while keeping the changes

```
alias git-undo-last-commit='git reset --soft HEAD~1'
```

### Revert all local changes

```
alias git-revert-changes='git fetch --prune && git reset --hard'
```

### Checkout previous branch

```
alias git-previous-branch='git checkout -'
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
