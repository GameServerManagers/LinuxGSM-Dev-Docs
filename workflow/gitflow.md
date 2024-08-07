# Gitflow

## GitFlow

LinuxGSM uses the GitFlow method (mostly) for releases. Relying on `master`, `develop`, `feature` and `hotfix` branches.

![GitFlow branching model](../.gitbook/assets/git-model-2x.png)

For further reading on the GitFlow model read the following article.

{% embed url="http://nvie.com/posts/a-successful-git-branching-model/" %}

{% embed url="https://www.youtube.com/watch?v=hG_P6IRAjNQ" %}

## Branches

The `master` branch will be the stable release branch. The `develop` branch is for developing stable code. All code is to be developed in a `feature` branch or `hotfix` for urgent fixes.

### Master

The `master` branch is where the stable, production release is kept. Only code that has gone via the `develop` can be merged here and goes through a release process. It is very important that the code there has been tested and is stable as it is used in production.

### Develop

The `develop` branch brings together all the `feature` branches ready to be tested to become the next stable release. Developers should use `develop` as the base when creating a branch.

### Feature

A feature branch is a development branch that is used while code is being actively worked on by developers. A feature branch should normally relate to an existing issue in GitHub. The feature branch should refer to the issue number and a word or two describing the issue, allowing other developers to know what issue branch is related to and helps with housekeeping.

```text
feature\1234-glibc-migrate
```

Once a feature is ready to be merged into `develop` a pull request is to be raised to allow the feature to be reviewed.

{% hint style="info" %}
The branch naming convention is less of an issue for developers who have forked the project and submitted a pull request. However, it is recommended that the standard is used.
{% endhint %}

### Hotfix

The `hotfix` branch is identical to the `feature` branch but instead is used for urgent fixes that need to be applied to master.

```text
hotfix\1234-glibc-migrate
```

### Release

When code from the `develop` branch is ready for release it is split off into a `release` branch.

The `release` branch will not have any more features added to it. It is then tested and any bugs fixed it will be released into `master` and tagged as a version number. The release will also be merged back into the `develop` branch.
