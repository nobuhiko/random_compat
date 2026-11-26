# random_compat 1.4.3 without the OpenSSL fallback, for EC-CUBE 3.0.x

[![tests](https://github.com/umiushi-lab/random_compat/actions/workflows/tests.yml/badge.svg?branch=eccube3%2F1.4)](https://github.com/umiushi-lab/random_compat/actions/workflows/tests.yml) [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/umiushi-lab/random_compat/badge)](https://scorecard.dev/viewer/?uri=github.com/umiushi-lab/random_compat)

EC-CUBE 3.0.18 ships `paragonie/random_compat` 1.4.3. This fork keeps 1.4.3 and removes the insecure fallback. It only matters on PHP 5; PHP 7 and later use the native `random_bytes()`.

## Fixed

| Advisory | What |
|---|---|
| PKSA-cncr-q695-v65g | `openssl_random_pseudo_bytes()` was used as a source of random bytes (fixed upstream in 2.0) |

## Install

Requires Composer 2. In the shop's project root:

```
composer require umiushi-lab/random_compat:^1.4.3
```

The package `replace`s `paragonie/random_compat` 1.4.3, so Composer removes the original and every other package keeps working against the same version.
EC-CUBE 3.0.18's own `composer.json` lists `mikey179/vfsStream` in `require-dev`; Composer 2 only accepts it in lowercase (`mikey179/vfsstream`), so fix that line first.

## What this is, and is not

- The base is exactly the version EC-CUBE 3.0.18 ships. Nothing is upgraded; only security fixes are added, each as its own commit on the `eccube3/1.4` branch.
- Each fix whose weakness could be reproduced on the base version was checked with a script that uses the weakness before the fix and fails to use it after, on PHP 5.6, 7.1 and 7.3. A few could not be reproduced there (Windows-only code, and cases the old code happened not to reach); those are ported as hardening. PHP 5.3 to 5.5 were not run (the changes avoid syntax newer than 5.3).
- This is not an official release of the upstream project and is not supported by its maintainers. Upstream: https://github.com/paragonie/random_compat
- EC-CUBE 3 と、その部品の古い系列には、もう公式の修正が出ません。3.0.18 が使っているバージョンのまま、上流の修正だけを移したものです。保守: うみうしラボ
