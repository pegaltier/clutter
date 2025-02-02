
# Clutter is now MewsFeed

We are currently working towards the first major release of MewsFeed.

Collaborate on GitHub and join our Discord: https://discord.gg/D3BykUZumM

## Environment Setup

1. Install the holochain dev environment (only nix-shell is required): https://developer.holochain.org/quick-start/

3. Clone this repo and `cd` inside of it.
4. Enter the nix shell by running this in the root folder of the repository: 

```bash
nix-shell
npm install
```

This will install all the needed dependencies in your local environment, including `holochain`, `hc` and `npm`.

~~5. Install git submodule dependency (ui-common-library)~~ 

```bash
# not necessary with this Angular fork
git submodule init
git submodule update --remote --recursive
```

## Building the DNA

- Build the DNA (assumes you are still in the nix shell for correct rust/cargo versions from step above):

```bash
npm run build:happ
```

## Running the DNA tests

```bash
npm run test
```

## UI

To test out the UI:

``` bash
npm start
```

To run another agent, open another terminal, and execute again:

```bash
npm start
```

Each new agent that you create this way will get assigned its own port and get connected to the other agents.

## Package

To package the web happ:

``` bash
npm run package
```

You'll have the `clutter.webhapp` in `workdir`. This is what you should distribute so that the Holochain Launcher can install it.

You will also have its subcomponent `clutter.happ` in the same folder`.

## Documentation

We are using this tooling:

- [NPM Workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces/): npm v7's built-in monorepo capabilities.
- [hc](https://github.com/holochain/holochain/tree/develop/crates/hc): Holochain CLI to easily manage Holochain development instances.
- [@holochain/tryorama](https://www.npmjs.com/package/@holochain/tryorama): test framework.
- [@holochain/conductor-api](https://www.npmjs.com/package/@holochain/conductor-api): client library to connect to Holochain from the UI.


## Refactored with Nx/Angular/Ionic

- https://github.com/artbrock/clutter
- https://devdactic.com/twitter-ui-with-ionic
- https://github.com/mcknasty/twitter-angular-clone.github.io
- https://nx.dev/recipes/environment-variables/use-environment-variables-in-angular

### Preview

- Angular Webapp

![Preview of Clutter web](./docs/clutter-web-preview.jpg)

- Ionic Mobileapp

![Preview of Clutter mobile](./docs/clutter-mobile-preview.jpg)

### Nx

```bash
npx nx@latest init
npm install --save-dev @nrwl/angular
npx nx generate @nrwl/angular:application clutter-web --no-interactive
npm install --save-dev --exact @nxtend/ionic-angular --legacy-peer-deps
npm install --save-dev --exact @nxtend/capacitor --legacy-peer-deps
npx nx generate @nxtend/ionic-angular:application clutter-mobile --capacitor false
npx nx generate @nrwl/angular:library clutter/data-access-dna
npx nx generate @nrwl/angular:library shared/util-holochain
npx nx generate @nrwl/angular:library shared/util-common
```

### WSL

```bash
# start wsl session & start deamon as root: https://nixos.org/manual/nix/stable/installation/multi-user.html
wsl
sudo su -
nix-daemon
# start another wsl session and enjoy your nix commands
wsl
nix develop --extra-experimental-features nix-command --extra-experimental-features flakes
```