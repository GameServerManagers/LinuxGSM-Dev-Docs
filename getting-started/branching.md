# Branching and Pull Requests

LinuxGSM has now moved from a rolling release to scheduled releases. This is due to the size of the project and the requirement to better manage features and bug fixes.

## GitFlow

LinuxGSM uses the GitFlow method \(mostly\) of releases. Relying on `master`, `develop`, `feature` and `hotfix` branches.

![GitFlow branching model](../.gitbook/assets/git-model-2x.png)

For further reading on the GitFlow model read the following article.

{% embed url="http://nvie.com/posts/a-successful-git-branching-model/" %}

## LinuxGSM Feature Flowchart

The below flow chart highlights the basic method for getting a feature released.

![](../.gitbook/assets/e241csr.jpg)

## Branches

The `master` branch will be the stable release branch. The `develop` branch is for developing stable code. All code is to be developed in a `feature` branch or `hotfix` for urgent fixes. 

### Master

The `master` branch is where the stable release is kept. Only code that has gone via the `develop` can be merged here and goes through a release process. It is very important that code there has been tested and is stable as it is used in production.

### Develop

The `develop` branch brings together all the `feature` branches ready to be tested to become the next stable release. Developers should use `develop` as the base when creating a branch. 

### Feature

A feature branch is a development branch that is used while code is being actively worked on by developers. A feature branch should normally relate to an existing issue in GitHub. The feature branch should refer to the issue number and a word or two describing the issue, allowing other developers to know what issue branch related to and helps with housekeeping.

```text
feature\1234-glibc-migrate
```

Once a feature is ready to be merged in to `develop` a pull request is to be raised to allow the feature to be reviewed.

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

It is also a good idea to start using [Git Kracken](https://www.gitkraken.com/) as the git client. It is a little more complex that GitHub Desktop but will give you a much better understanding of the development process.

## Pull Requests

Once the code you have worked on is ready to be submitted to the LinuxGSM project a [pull request](branching.md) will need to be raised. Pull requests have a list of things that need to be completed to get it merged into the project. Follow these steps as much as possible to ensure that your code can be merged quicker. When the pull request is raised various unit tests will be done on the code to ensure it follows the correct standards. When naming a pull request ensure that it is following [Conventional Commits](https://www.conventionalcommits.org/) standards; as this is what is used for generating the [changelog](https://github.com/GameServerManagers/LinuxGSM/releases) for the next release. 

A best practice for writing a commit message is to say in your head the following, followed by the change you are making.

> If I commit this change it will......._add slack support to alerts_

```bash
feat(alerts): add slack support to alerts
```

```bash
fix(csgoserver): remove SteamCMD auth requirement 32-bit workaround 
```

Once the Pull Request is created it is now time to wait.   
  
The Pull Request will need to be reviewed by LinuxGSM developers who regularly work on the project. They will accept, reject or recommend changes to the Pull Request. This can take time or your pull request will be held until a time that is appropriate to merge into the project so please be patient. One of the developers may leave a review to make changes or make changes themselves to make the commit ready. Once this review process is completed congratulations your commit will be merged ready for the next release.

Once merged in to the develop branch where it will be tested with other new features and code. When the code is at a point to release it will be merged in to the master branch which will make it live. 

Pull Requests \(PR\) let others review changes a developer has been making in a branch. Once a PR is opened, a branch can be reviewed with other developers giving feedback and also add follow-up commits \(LinuxGSM core devs only\) before changes are merged into the base branch.

LinuxGSM uses Pull Requests to allow developers to submit code that is ready or nearly ready to be merged into the `develop` branch. To make the process easier a checklist template has been created to guide the submission.

Various unit tests are carried out to check that the PR does not break LinuxGSM and follows standards. Feedback is given by the tests once they are completed.

If the PR is not quite ready for merge but is ready for review and feedback ensure the subject of the PR conains `[WIP]`\(Work in Progress\).

