Maintenance scripts
===================

A couple scripts to quickly fetch & update all repositories in this organization. `pull` script is written to work with all repositories in the same organization as this repository.

![demo running status and pull](https://repository-images.githubusercontent.com/272589316/ebb9e480-af59-11ea-8aee-ad0a44455a8b)

_NOTE: These scripts have only been tested on macOS_


Use it
======

First, set up a token for pulling repositories:

* Go to https://github.com/settings/tokens
* Click "Generate new token"
* Give it a good "Note", like "why does GitHub v4 require a token just to view public repositories omg"
* Don't check any boxes; it's just pulling public repos
* Scroll down and hit "Generate token"
* In your `~/.bashrc` or equivalent, export an environment variable called
  `GITHUB_TOKEN` with the value of your new token

      GITHUB_TOKEN=the_value_github_gave_you

Now install some dependencies & clone this repo into a sensible location:

* Install prerequisites: `brew install jq`
* Must have [ssh key added to GitHub](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)
* Set up a new directory where you want to clone _only_ the repositories in this org
* Clone this repository into that new directory
* Optionally: add `./bin` to your PATH

If you've done the last step, you can change into that local folder and:

* run `pull` to fetch the latest `main` for all repositories
* run `status` to quickly find out if all projects have `master` checked out
  with a clean working tree. You can pass options that you would normally pass
  to `git status`, such as `-s` for short output.
* run `run some command` to run "some command" in each repository
* use `dirty` to do things like quickly commit a bunch of changes. Example:

      for x in $(dirty); do (cd $x && git add --all && git commit -m "cool" && git push); done

If you don't complete the last step, you will have to type `./bin/pull` and
`./bin/status` instead.
