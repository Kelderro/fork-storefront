# Releasing Storefront

This document outlines the process for releasing new versions of the Storefront theme.

## Steps

The release process has three main phases:

- Building and testing a release candidate (RC) - steps 1-3 below.
- Fixing any issues that arise during RC testing.
- Building and releasing the final release - steps 1 & 4-6.

Depending on the release, releasing and testing an RC may not be necessary (i.e. skip step 2); for larger releases, multiple RCs may be worthwhile (i.e. repeat steps 1-3).

### 1 – Prepare code & build zip file

- Confirm all work intended for release (fixes, features) is completed and merged to release branch.
- Ensure your local checkout is in release branch and up to date!
- Update version numbers and release date:
  - `readme.txt`
  - `style.scss`
  - `package.json` and `package-lock.json`
- Confirm/update metadata in `readme.txt`, e.g. “tested up to” version.
- Draft changelog and add to `readme.txt`.
- Clean install of dependencies: `npm ci`.
- Run a production build: `npm run deploy`. Note this does not deploy anywhere, you can run multiple times safely 🙂
- Ensure all changes above are committed and pushed (you should not have uncommitted changes):
  - Version numbers, dates, metadata
  - Changelog
  - Translation (`.pot`) file. Note this file is generated by production build.

__*Outcome*: A `storefront.zip` file that you can test with.__ 

### 2 – Publish RC build (optional)

- Publish release on [GitHub](https://github.com/woocommerce/storefront/releases).
  - Upload release zip.
  - Use this format for tag: `version/1.2.3-rc.1`.
  - Paste changelog into “release details” field.

__*Outcome*: A `storefront.zip` file is available to the community and other stakeholders for testing and feedback.__

### 3 – Test & QA

Note: all new code should have been fully tested during development. This test pass is to confirm that there are no major regressions or bugs, aka [“happy path”](https://en.wikipedia.org/wiki/Happy_path) or [smoke testing](http://softwaretestingfundamentals.com/smoke-testing/).

- __Recommended__: Test in a clean environment, similar to a typical hosting environment. Avoid testing in your development environment.
- __Recommended__: Test with a snapshot of data from a real store, with customers, products and reviews.
- Test core WordPress and Woo flows.
- Test core Storefront features.
- Test compatibility with Storefront child themes and plugins.
- Spot-check to confirm recent fixes (this release, previous release) are working correctly and haven’t regressed.
- If there are blocking issues or major regressions, the process stops here! (So they can be fixed.)

__*Outcome*: You (release lead) are confident that the product is ready for release, and a safe & worthwhile upgrade for merchants.__

### 4 – Launch release

Now we get to release!

- If necessary, build final `storefront.zip` with correct (non-RC) version number (repeat step 1).
- Publish release on [GitHub](https://github.com/woocommerce/storefront/releases).
  - Upload release zip.
  - Use this format for tag: `version/1.2.3`.
  - Paste changelog into “release details” field.
- Upload to [WordPress.org](https://wordpress.org/themes/upload/). (You'll need access to the `Automattic` user account.)
- Publish any documentation updates.
- Post an announcement on the [dev blog](https://woocommerce.wordpress.com/category/storefront/).

__*Outcome*: Merchants are using the new Storefront, your new features are live, stores are working better, customers are happier!__

### 5 – Post-release checks

- Confirm WordPress.org version is correct, sites can auto-update.
- Update [demo site](https://themes.woocommerce.com/storefront/):
  - Clone/update [demo.woothemes.com](https://github.com/automattic/demo.woothemes.com) repository master branch.
  - Update storefront – i.e. unzip and replace `themes/storefront`.
  - Commit & push.
  - Site should automatically build & deploy.
- Confirm demo site is running correct version and nothing is broken.