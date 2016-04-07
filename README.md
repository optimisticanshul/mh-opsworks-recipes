# mh-opsworks-recipes [![Build Status](https://secure.travis-ci.org/harvard-dce/mh-opsworks-recipes.png?branch=master)](https://travis-ci.org/harvard-dce/mh-opsworks-recipes)

A custom cookbook in support of [mh-opsworks](https://github.com/harvard-dce/mh-opsworks).

## Supported Platforms

Ubuntu 14.04 LTS, and more specifically [amazon
opsworks](https://aws.amazon.com/opsworks/)

## Development

### Requirements

* ruby >= 2
* vagrant >= 1.7.0

### Development setup

First, satisfy the requirements above. Then:

        git clone https://github.com/harvard-dce/mh-opsworks-recipes/
        cd mh-opsworks-recipes
        bundle

You should now have [test-kitchen](http://kitchen.ci) and the vagrant tooling
for test-kitchen installed. You probably need to read up on test-kitchen if
you're not familiar with it.

### Process

* Create a branch off the develop branch
* Edit your cluster config to use this branch in your development cluster
* Write tests - currently we support
  [bats](https://github.com/sstephenson/bats) tests, but
  [serverspec](http://serverspec.org/) should work fine too once we get to it.
* Make your changes and push them to your recipe branch
* Run `./bin/run_foodcritic.sh` to lint your recipes. This uses
  [foodcritic](http://www.foodcritic.io) to lint your recipes for best
  practices. See `.foodcritic`  for config and information on tests we skip.
  We also run these tests via travis
  [here](https://travis-ci.org/harvard-dce/mh-opsworks-recipes)
* Run your kitchen tests

        kitchen test <your test suite>

* (optional, but do it relatively frequently) run the full kitchen tests

        kitchen test all

* Update your cluster's chef recipes and redeploy to run them. If your recipe
  isn't run during the opsworks deploy lifecycle, then run it manually to test.
* Work on your feature until it's ready to be merged into the develop branch.
* Be sure to update the "To be released" section of the CHANGELOG.md file with
  a description of your change, and whether or not it requires a manual recipe
  invocation. If your change runs as part of the deploy lifecycle, it will be run
  the next time the main app is deployed to a cluster and therefore does not
  require a manual chef recipe invocation.
* Rebase against develop and submit a pull request off of develop.

## QA'ing and releasing new chef recipes

* Update CHANGELOG.md to collapse all "To be released" changes under a new
  version, following [semver](http://semver.org).
* Rebase develop onto master (just to be sure).
* Cut an RC tag and link that into your staging cluster. Annotate the tag to
  reference the matterhorn tag this is meant to work with.
* QA. When QA passes,
* Merge the RC tag into master,
* Tag the release on master based on the RC tag
* Push the tag to the remote via `git push --tags`
* Make sure the release manager knows the correct tag to use in the cluster
  config.

## Contributors

* Dan Collis-Puro - [djcp](https://github.com/djcp)
* Jay Luker - [lbjay](https://github.com/lbjay)

## License

This project is under an Apache 2.0 license. Please see LICENSE.txt for details.

## Copyright

2015 President and Fellows of Harvard College
