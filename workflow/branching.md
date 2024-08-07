# Pull Requests

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

Pull Requests (PR) let others review changes a developer has been making in a branch. Once a PR is opened, a branch can be reviewed with other developers giving feedback and also add follow-up commits (LinuxGSM core devs only) before changes are merged into the base branch.

LinuxGSM uses Pull Requests to allow developers to submit code that is ready or nearly ready to be merged into the `develop` branch. To make the process easier a checklist template has been created to guide the submission.

Various unit tests are carried out to check that the PR does not break LinuxGSM and follows standards. Feedback is given by the tests once they are completed.

If the PR is not quite ready for merge but is ready for review and feedback ensure the subject of the PR conains `[WIP]`(Work in Progress).
