## What was the problem?

Consumers of PatternFly were investing time creating multiple very similar solutions built from Patternfly Components

**actual examples go here**

## What is the extension seed?
The extension seed is an application scaffold like create-react-app, but instead of making a generic React app it creates a generic extension of the PatternFly library.

_Extensions_ in this context are typically all-in-one solutions for problems which are composed from multiple components from the PatternFly library.

Applications created using the extension seed come with out of the box support for TypeScript, linting, unit testing, accessibility testing, and CI/CD via GitHub Actions which matches the standards set by the upstream PatternFly libraries.

The extension seed also uses the same documentation framework as the PatternFly website, so that documentation you create for your extension can be easily integrated into the PatternFly website.

## Why should you use it?

## How do you use it?

### Initial scaffolding:

1. create an empty repo for your new extension on GitHub
    > **editors note**:  maybe add a screenshot of the new repo button being clicked or something?
1. clone that repo to your local machine
    ```bash
        git clone git@github.com:org/repo-name.git
    ```
1. enter the directory created by cloning
    ```bash
        cd repo-name
    ```
1. run the scaffolding app using npx, this will ask you a series of questions and create the foundation for your extension based on your input
    ```bash
        npx tmplr patternfly/patternfly-extension-seed
    ```
1. enter your information when prompted
   - npm scope should start with an @ symbol, i.e. @patternfly
   - extension name should be in sentence case but without any punctuation, i.e. Patternfly extension seed
   - What will your extension do? Need to have an example for this as well
   - repo URL should be the plain URL of the repo not URL used to clone, i.e. https://github.com/patternfly/patternfly-extension-seed
1. install the dependencies
    ```bash
        yarn install
    ```

### What goes where?

Below is an overview of the structure of an extension made using the extension seed:

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

As soon your push completes, GitHub will start running the CI/CD pipeline using GitHub Actions.

> **_NOTE:_** The extension seed is capable of automatically releasing your extension on NPM once it has passed your CI checks, but to prevent accidental release you will have to change the value of `dryRun` from `true ` to `false` in `packages/module/release.config.js` to enable this behavior.

The default pipeline for PRs will:
- Ensure that your components can build and compile
- Check that the package meets our linting requirements
- Run all of your unit tests and make sure that they pass
- Run accessibility tests 
- Ensure that your documentation can be pulled into the PatternFly site without error
    
The release pipeline (which runs whenever `main` is pushed to) will also attempt to automatically release your package to NPM.
     
If everything passes CI congratulations! You just published your first PatternFly extension package!

### Ok now how do I actually get my extension on the PatternFly site?

This process actually… isn’t very easy right now. But I will write a generator that makes it simple, then document that generator here or link to that documentation here.

## How does the extension seed solve the problem?

The seed makes it as easy as possible to contribute these solutions upstream in a way that is highly visible to other consumers
