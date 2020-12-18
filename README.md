# Utilities to make my (and your?) life easier

This is a collection of reusable scripts, functions and [aliases](https://en.wikipedia.org/wiki/Alias_(Mac_OS)) related to software development.

- [Bash & Zsh](#bash--zsh)
- [JavaScript & TypeScript](#javascript--typescript)
- [Git](#git)
- [Utilities & Miscellaneous](#utilities--miscellaneous)

## Bash & Zsh

### Open `.bash_profile` in Visual Studio Code

```shell
alias edit-bash-profile="code ~/.bash_profile"
```

### Apply changes made in `.bash_profile` without restarting your terminal

```shell
alias refresh-bash="source ~/.bash_profile"
```

### Open `.zshrc` in Visual Studio Code

```shell
alias edit-zsh='code ~/.zshrc'
```

### Apply changes made in `.zshrc` without restarting your terminal

```shell
alias refresh-zsh='source ~/.zshrc'
```

### View pretty-printed JSON response using `fx`

```shell
curl_json_pretty() {
    curl $1 | npx fx .
}
```

### Work with JSON response using `fx`

```shell
curl_json() {
    curl $1 | npx fx
}
```

### Execute a command multiple times

```shell
run_multiple_times() {
  echo "Executing" "the following command" $1 "times:" $2
  for i in $(seq 1 $1);
    do $2;
  done;
}
```

### Shortcut for home directory

```shell
alias home="cd ~"
```

### Say `please` and you shall receive

```shell
alias please="sudo"
```

### Rerun last command

```shell
alias rerun="!!"
```

### Use rainbow

```shell
run_with_rainbow() {
    $1 | npx lolcatjs
}
```

## JavaScript & TypeScript

### List globally installed NPM packages

```shell
alias npm-global-packages="npm list -g --depth 0"
```

### Fix auto-fixable issues in TSLint

```shell
alias tslint-fix="npx tslint --fix --project ./"
```

### Generate a `tsconfig.json` file

```shell
alias ts-init="npx tsc --init"
```

### Clear cache of Jest test runner

```shell
alias jest-clear-cache="npx jest --clearCache"
```

### Start Jest in watch mode

```shell
alias jest-watch="npx jest --watch"
```

### Check JavaScript bundles for ES5 compatibility

```shell
check_es_bundles() {
  echo "Checking bundles in" $1 "for ES5 compatibility."
  npx es-check es5 $1 --verbose
}
```

### Compile TypeScript

```shell
compile_typescript() {
  echo "Compiling TypeScript using the following configuration file:" $1
  npx tsc -p $1
}
```

### Find publicly known security vulnerabilities in a website's frontend JavaScript libraries using [Snyk](https://snyk.io)

```shell
run_snyk_check() {
  echo "Running Snyk check for website:" $1
  npx is-website-vulnerable $1
}
```

### Run a local HTTP server

```shell
run_http_server() {
  echo "Running HTTP server on port" $1 ". Serving the following directory:" $2
  npx http-server -p $1 -c-1 $2
}
```

### Start Cypress test runner

```shell
open_cypress() {
    npx cypress open $1
}
```

### Determine download stats for all the NPM packages by user

```shell
get_npm_download_stats() {
    npx https://gist.github.com/kentcdodds/8eea6d7365f46ddd2f2760bb44d164c0 $1
}
```

### Start server, test and terminate
```shell
start_server_and_test() {
    npx start-server-and-test $1 $2 $3
}
```

### Invoke Angular CLI / nx.dev CLI if you don't have them installed globally

```shell
alias ng="npx ng"
alias nx="npx nx"
```

## Git

### Stash single file

```shell
alias git-stash-single-file="git stash push "
```

### Print current branch name

```shell
alias git-branch-name='git rev-parse --abbrev-ref HEAD'
```

### Amend staged files

```shell
alias git-ammend='git commit --amend'
```

### Undo last commit while keeping the changes

```shell
alias git-undo-last-commit='git reset --soft HEAD~1'
```

### Revert all local changes

```shell
alias git-revert-changes='git fetch --prune && git reset --hard'
```

### Checkout previous branch

```shell
alias git-previous-branch='git checkout -'
```

## Utilities & Miscellaneous

### Kill process running on a specific port

```shell
kill_process_by_port() {
  lsof -i TCP:$1 | grep LISTEN | awk '{print $2}' | xargs kill -9
  echo "Port" $1 "found and killed."
}
```

### Convert a post on Medium.com to a Markdown document

```shell
medium_post_to_markdown() {
    cd ~/Desktop
    npx mediumexporter "$1" > medium_post.md
}
```

### Execute a JAR file

```shell
run_jar() {
    "Running the following JAR file: " $1
    java -jar $1
}
```
