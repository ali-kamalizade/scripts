# Utilities to make my (and your?) life easier

This is a collection of reusable scripts, functions and [aliases](https://en.wikipedia.org/wiki/Alias_(Mac_OS)) related to software development.

- [Bash & Zsh](#bash--zsh)
- [JavaScript](#javascript)
- [TypeScript](#typescript)
- [Jest](#jest)
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

### Highlight syntax of a file

```shell
highlight_syntax() {
    npx cli-highlight $1
}
```

## JavaScript

### List globally installed NPM packages

```shell
alias npm-global-packages="npm list -g --depth 0"
```

### Run security audit for Node projects (omit `--production` to consider `devDependencies` as well)

```shell
alias npm-audit-prod="npm audit --production"
```

### Find unused NPM dependencies using [depcheck](https://github.com/depcheck/depcheck)

```shell
alias npm-depcheck="$ npx depcheck"
```

### Check JavaScript bundles for ES5 compatibility using [es-check](https://github.com/yowainwright/es-check)

```shell
check_es_bundles() {
  echo "Checking bundles in" $1 "for ES5 compatibility."
  npx es-check es5 $1 --verbose
}
```

### Find publicly known security vulnerabilities in a GitHub project using [Snyk](https://snyk.io) (provide URL)

```shell
run_snyk_github_project_check() {
  echo "Running Snyk check for GitHub project:" $1
  npx snyk test $1
}
```

### Find publicly known security vulnerabilities in a website's frontend JavaScript libraries using [Snyk](https://snyk.io)

```shell
run_snyk_website_check() {
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

### Update Angular to latest version

```shell
ng_update_to_latest() {
    ng update @angular/cli --allow-dirty
    ng update @angular/core --allow-dirty
    ng update @angular/cdk --allow-dirty 
}
```

### Run accessibility tests on a provided page

```shell
test_website_a11y() {
    npx pa11y $1
}
```

### Format files using [Prettier](https://github.com/prettier/prettier) (must be installed in the current directory)

```shell
alias browserslist="prettier --write ."
```

### List browsers which are supported by your project (needs a [browerslist](https://github.com/browserslist/browserslist) file)

```shell
alias browserslist="npx browserslist"
```

### Set the provided Node version as default using [nvm](https://github.com/nvm-sh/nvm)

```shell
nvm_set_default_version() {
    echo "Set the following version as default:" $1
    nvm alias default $1
}
```

## Jest

### Clear cache of Jest test runner

```shell
alias jest-clear-cache="npx jest --clearCache"
```

### Debug issues when using Jest test runner (e.g. when Jest is stuck and not logging the root issue)

```shell
alias jest-debug='npx jest --detectOpenHandles'
```

### Start Jest in watch mode

```shell
alias jest-watch="npx jest --watch"
```

### Open Jest coverage report (run tests with `--coverage`)

```shell
open_jest_coverage_report() {
    open ./coverage/lcov-report/index.html
}

```

## TypeScript

### Fix auto-fixable issues in TSLint

```shell
alias tslint-fix="npx tslint --fix --project ./"
```

### Generate a `tsconfig.json` file

```shell
alias ts-init="npx tsc --init"
```

### Execute TypeScript code using `ts-node`

```shell
alias ts-node="npx ts-node"
```

### Compile TypeScript

```shell
compile_typescript() {
  echo "Compiling TypeScript using the following configuration file:" $1
  npx tsc -p $1
}
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

### Remove committed file from Git version control but keep it locally

```shell
git_remove() {
    "Removing the following file from version control (it's still available locally: " $1
    git rm --cached $1
}
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

### Show contributors sorted by commits

```shell
alias git-contributors='git shortlog -sn --all'
```

### Push with force to repository but do not overwrite changes on the remote branch which you don't have locally yet ([see here](https://stackoverflow.com/a/52823955/4743909))

```shell
alias git-safe-force-push='git push --force-with-lease'
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

### Fix `xcrun: error: invalid active developer path, missing xcrun` error (this can occur after a Mac OS update)

```shell
alias fix-macos-xcrun='xcode-select --install'
```
