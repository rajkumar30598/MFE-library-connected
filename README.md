# MFE Library Consumer (MFE-library-connected)

An Angular 14 application that consumes the shared component library from **[MFE-library](https://github.com/rajkumar30598/MFE-library)** via a local package install.

![Angular](https://img.shields.io/badge/Angular-14-DD0031?logo=angular&logoColor=white)

## What it demonstrates

- Installing a locally built Angular library as an npm dependency with a relative path:
  ```json
  "angularlibrary": "../sample-library/dist/sample"
  ```
  npm links this into `node_modules/angularlibrary`.
- Importing the library's `SampleModule` into `AppModule` (`import { SampleModule } from 'angularlibrary'`)
- Rendering the library component `<lib-sample>` from `AppComponent`'s template
- `preserveSymlinks: true` in `angular.json` so the Angular build resolves the symlinked package correctly

## How the two repos connect

```
MFE-library                                  MFE-library-connected (this repo)
  projects/sample  --ng build sample-->  dist/sample
                                             ^
                                             |  package.json: "angularlibrary": "../sample-library/dist/sample"
                                             |
                                         AppModule -> SampleModule -> <lib-sample>
```

## Tech stack

| Package | Version |
| --- | --- |
| Angular | ^14.1.0 |
| RxJS | ~7.5.0 |
| TypeScript | ~4.7.2 |
| Karma + Jasmine (tests) | 6.4 / 4.x |

## Getting started

Both repositories need to sit side by side, with the library cloned into a folder named `sample-library` (that is the path the dependency points to).

```bash
mkdir mfe-demo && cd mfe-demo

# 1. Build the library
git clone https://github.com/rajkumar30598/MFE-library.git sample-library
cd sample-library
npm install
npx ng build sample
cd ..

# 2. Install and run the consumer app
git clone https://github.com/rajkumar30598/MFE-library-connected.git
cd MFE-library-connected
npm install          # links ../sample-library/dist/sample as "angularlibrary"
npm start            # ng serve -> http://localhost:4200
```

The page should render the library's `<lib-sample>` component ("sample works!").

To pick up library changes without reinstalling, run `npx ng build sample --watch` in the library folder while `npm start` runs here.

Other scripts:

```bash
npm run build        # production build to dist/sample-project
npm test             # unit tests with Karma
```
