# poliastro performance benchmarks

## About

These benchmarks track the performance of various features in poliastro
*over time*.

To view them, visit [this site](https://benchmarks.poliastro.space).

The benchmarks are run using [airspeed velocity](https://asv.readthedocs.io).

## For contributors

The `master` branch in this repository should not contain any results or
built website. Results should be added to the `results` branch, and
commits to the `results` branch trigger a build to the `gh-pages`
branch.

To do a dry run of the benchmarks, install the dependencies and do:

```
$ asv run --dry-run
```

[![image](https://travis-ci.org/poliastro/poliastro-benchmarks.svg)](https://travis-ci.org/poliastro/poliastro-benchmarks)
