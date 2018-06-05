projekct maintainers. If you're not sure if it's a bug or not,
start by asking in the [discussion forum](https://discourse.goprojek.io).
When reporting the issue, please provide the version of projek in use (`projek
version`) and your operating system.

## Code Contribution

projek has become a fully featured static site generator, so any new functionality must:

* be useful to many.
* fit naturally into _what projek does best._
* strive not to break existing sites.
* close or update an open [projek issue](https://github.com/goprojekio/projek/issues)

If it is of some complexity, the contributor is expected to maintain and support the new future (answer questions on the forum, fix any bugs etc.).

It is recommended to open up a discussion on the [projek Forum](https://discourse.goprojek.io/) to get feedback on your idea before you begin. If you are submitting a complex feature, create a small design proposal on the [projek issue tracker](https://github.com/goprojekio/projek/issues) before you start.


**Bug fixes are, of course, always welcome.**



## Submitting Patches

The projek projek welcomes all contributors and contributions regardless of skill or experience level. If you are interested in helping with the projek, we will help you with your contribution.

### Code Contribution Guidelines

Because we want to create the best possible product for our users and the best contribution experience for our developers, we have a set of guidelines which ensure that all contributions are acceptable. The guidelines are not intended as a filter or barrier to participation. If you are unfamiliar with the contribution process, the projek team will help you and teach you how to bring your contribution in accordance with the guidelines.

To make the contribution process as seamless as possible, we ask for the following:

* Go ahead and fork the projek and make your changes.  We encourage pull requests to allow for review and discussion of code changes.
* When you’re ready to create a pull request, be sure to:
    * Sign the [CLA](https://cla-assistant.io/goprojekio/projek).
    * Have test cases for the new code. If you have questions about how to do this, please ask in your pull request.
    * Run `go fmt`.
    * Add documentation if you are adding new features or changing functionality.  The docs site lives in `/docs`.
    * Squash your commits into a single commit. `git rebase -i`. It’s okay to force update your pull request with `git push -f`.
    * Ensure that `mage check` succeeds. [Travis CI](https://travis-ci.org/goprojekio/projek) (Linux and macOS) and [AppVeyor](https://ci.appveyor.com/projek/goprojekio/projek/branch/master) (Windows) will fail the build if `mage check` fails.
    * Follow the **Git Commit Message Guidelines** below.

### Git Commit Message Guidelines

This [blog article](http://chris.beams.io/posts/git-commit/) is a good resource for learning how to write good commit messages,
the most important part being that each commit message should have a title/subject in imperative mood starting with a capital letter and no trailing period:
*"Return error on wrong use of the Paginator"*, **NOT** *"returning some error."*

Also, if your commit references one or more GitHub issues, always end your commit message body with *See #1234* or *Fixes #1234*.
Replace *1234* with the GitHub issue ID. The last example will close the issue when the commit is merged into *master*.

Sometimes it makes sense to prefix the commit message with the package name (or docs folder) all lowercased ending with a colon.
That is fine, but the rest of the rules above apply.
So it is "tpl: Add emojify template func", not "tpl: add emojify template func.", and "docs: Document emoji", not "doc: document emoji."

Please use a short and descriptive branch name, e.g. **NOT** "patch-1". It's very common but creates a naming conflict each time when a submission is pulled for a review.

An example:

```text
tpl: Add custom index function

Add a custom index template function that deviates from the stdlib simply by not
returning an "index out of range" error if an array, slice or string index is
out of range.  Instead, we just return nil values.  This should help make the
new default function more useful for projek users.

Fixes #1949
```

###  Fetching the Sources From GitHub

Due to the way Go handles package imports, the best approach for working on a
projek fork is to use Git Remotes.  Here's a simple walk-through for getting
started:

1. Get the projek source:

    ```bash
    go get -u -v -d github.com/goprojekio/projek
    ```

1. Install Mage:

    ```bash
    go get github.com/magefile/mage
    ```

1. Change to the projek source directory and fetch the dependencies:

    ```bash
    cd $HOME/go/src/github.com/goprojekio/projek
    mage vendor
    ```

    Note that projek uses [Go Dep](https://github.com/golang/dep) to vendor dependencies, rather than a simple `go get`. We don't commit the vendored packages themselves to the projek git repository. The call to `mage vendor` takes care of all this for you.

1. Create a new branch for your changes (the branch name is arbitrary):

    ```bash
    git checkout -b iss1234
    ```

1. After making your changes, commit them to your new branch:

    ```bash
    git commit -a -v
    ```

1. Fork projek in GitHub.

1. Add your fork as a new remote (the remote name, "fork" in this example, is arbitrary):

    ```bash
    git remote add fork git://github.com/USERNAME/projek.git
    ```

1. Push the changes to your new remote:

    ```bash
    git push --set-upstream fork iss1234
    ```

1. You're now ready to submit a PR based upon the new branch in your forked repository.

### Building projek with Your Changes

projek uses [mage](https://github.com/magefile/mage) to sync vendor dependencies, build projek, run the test suite and other things. You must run mage from the projek directory.

```bash
cd $HOME/go/src/github.com/goprojekio/projek
```

To build projek: 

```bash
mage projek
```

To install projek in `$HOME/go/bin`:

```bash
mage install
```

To run the tests:

```bash
mage projekRace
mage -v check
```

To list all available commands along with descriptions:

```bash
mage -l
```

### Updating the projek Sources

If you want to stay in sync with the projek repository, you can easily pull down
the source changes, but you'll need to keep the vendored packages up-to-date as
well.

```bash
git pull
mage vendor
```
