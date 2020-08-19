# Contributing

Thanks for your interest in contributing to Inertia.js!

## Local development

To make local Inertia.js development easier, the project has been setup as a monorepo using [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/). To set it up, start by cloning the repository on your system.

```sh
git clone https://github.com/inertiajs/inertia.git inertia
cd inertia
```

Next, install the dependencies. Note, Yarn will automatically install all the package dependencies at the project root and will setup the necessary symlinks.

```sh
yarn install
```

It's often helpful to develop Inertia.js within a real application, such as [Ping CRM](https://github.com/inertiajs/pingcrm). To do this, you'll need to use the `yarn link` feature to tell your application to use the local versions of the Inertia.js dependencies. To do this, first run `yarn link` within each Inertia.js package that you want to develop.

```sh
cd packages/inertia
yarn link
cd ../inertia-vue
yarn link
```

Finally, within your application, run `yarn link` again, but this time specifying which local packages you want to use:

```sh
cd pingcrm
yarn install
yarn link @inertiajs/inertia
yarn link @inertiajs/inertia-vue
```

If you're developing one of the packages that requires a build step (`inertia`, `inertia-react` or `inertia-vue`), you'll want to setup a watcher to automatically run the build step anytime the package files change.

```sh
cd inertia
yarn watch
```

If you're developing the `inertia-react` or `inertia-svelte` packages, you'll likely run into issues caused by the fact that there are two instances of the framework installed. This happens because there is one copy in the monorepo and another in your application. You can get around this issue by creating a (local only) Webpack alias. For example:

```js
mix.webpackConfig({
  resolve: {
    alias: {
      react: path.resolve('node_modules', 'react'),
      svelte: path.resolve('node_modules', 'svelte'),
    }
  }
})
````