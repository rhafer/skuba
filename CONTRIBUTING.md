# Contributing to skuba

The following is a set of guidelines for contributing to this project, hosted by [SUSE](https://github.com/suse/skuba).
If you have a suggestion to these guidelines feel free to propose changes in a pull request.


## Pull requests

Contributors:
* Adhere to the PR template. Fill out as many sections as possible with as much detail as possible.
* Adhere to the style guide as closely as possible, where a bot cannot do it for you.
* The PR is ready for review only when the CI is green. Do not ask for people to review your code if the CI is failing.
* If CI is not passing, or you need to make more improvements than expected, please add the wip label.
* Once the CI is green, feel free to assign specific reviewers to your PR to signal it is ready.
* Do NOT merge pull requests.  CI will automatically merge the PR once tests pass and approvals are received.

Maintainers:
* Devote time to regular code review and make your reviews impactful. Look at the big picture, don't get hung up on style alone.
* Veto only when there's is something really problematic, otherwise just comment. Otherwise you are forcing a new round of reviews including a new CI run.
* Add yourself to the [CODEOWNERS](.github/CODEOWNERS) file if you want to be assigned automatically as reviewer in a particular area.


## Styleguides

### git commit messages

This list is not comprehensive, meaning if you want to include more detail than required that is fine as long as you meet these guidelines first.

* Title
  * Always start with an upper-case letter
  * Do not put a dot (period) at the end
  * Use imperative verbs
  * Maximum characters: 50 (excluding the (bsc#123456) part)
  * Tracking issues from Bugzilla
    * Add `(bsc#123456)` as part of the title

* Body
  * Start sentences with upper-case letter and finish with dot (period).
  * Maximum characters per line is 72
  * Explain what this commit is doing
  * Explain why we have to do it
  * Do not explain how unless the change is sufficiently large and needs further explanation
    * Tracking issues from Github:
      * __Do not track references (ID/URLs) to in the commit message__ but on the web-ui (yes you are forced to open your browser)

## Go style

This will be checked automatically by our CI linter bot.

## Releasing

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
+ If you are releasing a new kubernetes version, or any other container, +
+ make sure the versions.go has been updated accordingly. See as an      +
+ example:                                                               +
+   https://github.com/SUSE/skuba/pull/573                               +
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


In order to create a new release, create a Pull Request with these changes:

  * Update the VERSION file:
    echo "x.y.z" > VERSION

  * Commit with the message "Bump version: x.y.z", being x.y.z the version. Please use semantic versioning.
    git commit -m "Bump version: x.y.z" -s

Ask for a reviewer. Once reviewed, checkout master branch:

    * git checkout master && git pull

And tag:

  * Tag with vx.y.z
    git tag -s vx.y.z -m "Tag x.y.z"

* Push
  git push --tags origin master
  
  Note: Assuming origin is github.com/SUSE/skuba 

* Checkout the tag
  git checkout vx.y.z

* Create the changelog:
  make suse-package 

* Add a new release at https://github.com/SUSE/skuba/releases with the contents from the file ci/packaging/suse/obs_files/skuba.changes.append

* Use the files in ci/packaging/suse/obs_files to update the skuba package
