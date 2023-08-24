# Accelerate frontend development with the PatternFly Extension Seed

## What is the PatternFly Extension Seed?
The PatternFly Extension Seed is an application scaffold like create-react-app, but instead of making a generic React app it creates a generic extension for the [PatternFly library](https://www.patternfly.org/).

_Extensions_ in this context are interface systems composed using multiple components from the PatternFly library. Compared to PatternFly components these systems are generally more holistic, less flexible, and designed to address a specific problem.

Applications created using the PatternFly Extension Seed come with out of the box support for TypeScript, linting, unit testing, accessibility testing, and CI/CD via GitHub Actions which matches the standards set by the upstream PatternFly libraries.

The PatternFly Extension Seed also uses the same documentation framework as the PatternFly website, so that documentation you create for your extension can be easily integrated into the PatternFly website.

## Why should you use it?

The PatternFly library is primarily an upstream source of component level implementations which are used across a wide range of projects.

While this flexibility is required for PatternFly to have the broad applicability needed by teams using it to build modern UI's, it's meant that the consumers of our library must spend significant amounts of time wiring our components together to create actual interfaces. Often times, many project teams end up spending time creating systems that are extremely similar to systems already made by other projects.

When teams contribute their larger "batteries included" interface systems upstream to the PatternFly Extensions ecosystem, we're able to better leverage the power of an open source development model to accelerate development.

### Why we've used it

On the PatternFly team we used the PatternFly Extension Seed to quickly extract five packages from our main React monorepo and stand them up in their own repos. It also enabled us to launch one new extension and begin development of two more.

These efforts had largely been considered for quite a while previously, but were never prioritized as the work needed to stand them up and integrate them with our documentation site was deemed too time consuming.

Once we developed the PatternFly Extension Seed we were able to accomplish what would've likely taken months worth of dev time and accomplish it in a matter of days.

## How do you use it?

### Prerequisites
1. Git installed
2. Node installed (>=v18)
3. NPM installed
4. Yarn installed

### Initial scaffolding:

1. Create an empty repo for your new extension on GitHub (or your preferred alternative):
    ![](https://hackmd.io/_uploads/ByLp1NSan.png)

1. Clone that repo to your local machine:
    ```bash
        git clone git@github.com:org/repo-name.git
    ```
1. Enter the directory created by cloning:
    ```bash
        cd repo-name
    ```
1. Run the scaffolding app using npx, this will ask you a series of questions and create the foundation for your extension based on your input:
    ```bash
        npx tmplr patternfly/patternfly-extension-seed
    ```
1. Enter your information when prompted:
   - NPM scope should start with an @ symbol, i.e. ``@patternfly`
   - extension name should be in sentence case but without any punctuation, i.e. `Patternfly extension seed`
   - extension description should also be sentence case, i.e. `Enable accellerated development of extensions to the PatternFly eceosystem`
   - repo URL should be the plain URL of the repo not URL used to clone, i.e. `https://github.com/patternfly/patternfly-extension-seed`
1. Install the dependencies:
    ```bash
        yarn install
    ```

### What goes where?

Below is an overview of the structure of an extension made using the PatternFly Extension Seed:

```bash
.
├── LICENSE
├── README.md
├── babel.config.js
├── fed-mini-modules.js
├── jest.config.js
├── package.json
├── packages
│   └── module
│       ├── generate-fed-package-json.js
│       ├── package.json
│       ├── patternfly-a11y.config.js
│       ├── patternfly-docs
│       │   ├── content
│       │   │   ├── design-guidelines
│       │   │   │   └── design-guidelines.md
│       │   │   └── examples
│       │   │       ├── Basic.tsx
│       │   │       └── basic.md
│       │   ├── generated
│       │   │   ├── design-guidelines.js
│       │   │   ├── index.js
│       │   │   └── react.js
│       │   ├── pages
│       │   │   └── index.js
│       │   ├── patternfly-docs.config.js
│       │   ├── patternfly-docs.css.js
│       │   ├── patternfly-docs.routes.js
│       │   └── patternfly-docs.source.js
│       ├── release.config.js
│       ├── src
│       │   ├── ExtendedButton
│       │   │   ├── ExtendedButton.tsx
│       │   │   ├── __tests__
│       │   │   │   ├── ExtendedButton.test.tsx
│       │   │   │   └── __snapshots__
│       │   │   │       └── ExtendedButton.test.tsx.snap
│       │   │   └── index.ts
│       │   └── index.ts
│       └── tsconfig.json
├── renovate.json
├── styleMock.js
└── yarn.lock
```

 Any components you want to ship in your extension, along with their tests, should go in directories under `packages/module/src`, `ExtendedButton` shows an example of this structure
 
Documentation files for your extension should be placed in `packages/module/patternfly-docs/content`

Each documentation page should be a separate markdown file.

When creating the markdown files for your extension you can reference [our documentation](https://www.google.com) for the metadata of the files.

### Then what?

Once you’re happy enough with your extension to share it with the world just commit and push to your remote!

As soon as your push completes, GitHub will start running the CI/CD pipeline using GitHub Actions.

> **_NOTE:_** The PatternFly Extension Seed is capable of automatically releasing your extension on NPM once it has passed your CI checks, but to prevent accidental release you will have to change the value of `dryRun` from `true ` to `false` in `packages/module/release.config.js` to enable this behavior.

The default pipeline for PRs will:
- Ensure that your components can build and compile.
- Check that the package meets our linting requirements.
- Run all of your unit tests and make sure that they pass.
- Run accessibility tests .
- Ensure that your documentation can be pulled into the PatternFly site without error.
    
The release pipeline (which runs whenever `main` is pushed to) will also attempt to automatically release your package to NPM.
     
If everything passes CI congratulations! You just published your first PatternFly extension package!

### How do you actually get your extension on the PatternFly site?

If you've developed something that you think would be a great addition to the PatternFly Extensions ecosystem, or have an idea for an extension, please create [a discussion post on the PatternFly GitHub](https://github.com/orgs/patternfly/discussions). If we agree that it's a great fit we'll help guide you through the process of landing our extension's documentation on our site!
