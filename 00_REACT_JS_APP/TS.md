# Node Sass version 6.0.1 is incompatible with ^4.0.0 || ^5.0.0.

https://stackoverflow.com/questions/64625050/error-node-sass-version-5-0-0-is-incompatible-with-4-0-0

```sh

# TL;DR

npm uninstall node-sass
npm install node-sass@4.14.1
# Or, if using yarn (default in newer CRA versions)

yarn remove node-sass
yarn add node-sass@4.14.1

```