---
title: How to set up git version control with Studio apps
description: A guide to using version control with your Studio Apps.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

As you are developing your Studio application, version control will help you collaborate with other users and keep track of changes to maintain a robust version history. Studio applications can be linked to remote git repositories using most of the popular options, such as GitHub and GitLab. This guide shows you how to connect to a remote Github repository, and push and pull changes when collaborating with others.

## Connecting to Github

Connect your Studio application to Github by following these instructions:

1. Connect to Git by opening the Studio app you want to connect to Git and select the **Connect Git** button on the left side of the bottom bar.
2. Select **Github** as the service provider (or your preferred provider). Version Control works with any Git hosting service that supports the SSH protocol and deploy keys. HTTPS Git connections are not currently supported in Studio.
3. Create a new Git repository or open an existing empty repository. The connection may fail if the repository is not empty.
4. After setting up an empty repository, navigate to the repository's landing page, select the **Code** button, and copy the **SSH** URL.
5. Paste the URL in the **Generate SSH Key** section in Studio.
6. Select the **Generate SSH Keys** button to display the unique `ECDSA 256` and `RSA 4096` keys. Choose the appropriate key based on your specific security requirements and system constraints.
7. Copy one of the keys, then navigate to your **Repository settings**. Proceed to **Deploy keys**, select on **Add deploy keys**, paste the copied key, and provide a meaningful title for future reference.
8. Check the **Allow write access** option and then add the key.
9. In Studio, select the **Connect Git** button.

!!! info "Permissions required"

     You will need to have **Create** permission for application resources on the workspace to be able to connect or disconnect an app to Github.

## Resolve merge conflicts in Git

You may have to deal with merge conflicts in two cases:

* When merging two separate branches.
* When updating changes to a local or remote branch.

### Branch merge conflicts

Merge conflicts occur when changes from different branches overlap, leading to conflicts that need manual resolution.

To resolve these conflicts:

1. Raise a pull request (PR) for your source branch, targeting the destination branch where you intend to merge the changes. For example: If you're working on the `feature` branch and want to merge changes into `staging`, but are facing conflicts, you can raise a pull request for your `feature` branch on your Git provider, targeting the `staging` branch for merging.
2. Once the PR is created, scroll down to the bottom of the PR page: 
    * If the Resolve conflicts button is available, you can resolve conflicts directly from the pull request interface by selecting the conflicting files and making the necessary changes.
   * If the Resolve conflicts button is disabled, you need to clone the Git repository to your local machine and resolve the conflicts using the command-line interface. If you don't want to resolve conflicts locally, you can use tools like [GitHub.dev](https://github.com/github/dev), [GitLab Web IDE](https://docs.gitlab.com/ee/user/project/web_ide/) to resolve conflicts directly from your browser.
3. After resolving all conflicts in all files and ensuring that the changes are correctly edited, select on **Commit merge**, and Merge the pull request.
4. Update your Studio app by pulling the changes.

!!! info "Resolving merge conflicts with different remote providers"

     For more information, see how to resolve a merge conflict on [GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github), [GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/conflicts.html#methods-of-resolving-conflicts), [Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/resolve-merge-conflicts/).

## Remote branch pull conflicts

These conflicts arise when changes in your local branch cannot be directly merged with changes in the remote branch. For example, if you're working on the `feature` branch and someone else pushes changes to the remote counterpart of the same branch, you may encounter conflicts if both have edited the same files. 

To resolve these conflicts:

1. Create a new branch from the conflicted branch and raise a Pull Request. For example, create a new branch from your local `feature` branch, name it `feature-fix`, and then raise a pull request from this new branch against the original `feature` branch.
2. Once the PR is created, scroll down to the bottom of the PR page:

    * If the Resolve conflicts button is available, you can resolve conflicts directly from the pull request interface by selecting the conflicting files and making the necessary changes.
    * If the Resolve conflicts button is disabled, you need to clone the Git repository to your local machine and resolve the conflicts using the command-line interface. If you don't want to resolve conflicts locally, you can use tools like [GitHub.dev](https://github.com/github/dev), [GitLab Web IDE](https://docs.gitlab.com/ee/user/project/web_ide/) to resolve conflicts directly from your browser.
3. After resolving all conflicts in all files and ensuring that the changes are correctly edited, select on **Commit merge**, and Merge the pull request.
4. In Studio, select **Discard and Pull** from the commit modal to update the app.

For more on mrgee conflicts, see [Avoid merge conflicts](#avoid-merge-conflicts).

## Revert changes

When you want to fix a mistake or undo an unwanted change you can use `git revert`. You can revert changes from Git user interfaces provided by some platforms, but it is recommended to perform reverts from the local system using Git commands.

To revert changes: 

1. Open your application's Git repository and clone it to your local system.
2. Switch to the branch where you want to revert the change
3. To identify the commits, in the terminal by issuing the command: `git log`. This displays a list of commits in reverse chronological order, starting with the most recent commit. Each commit entry includes information such as the commit hash, author name, date, and commit message.
4. To revert a commit, use the `git revert` command followed by the commit hash. For example: `git revert 2f50d7dd1dc4874b7ca6054099b54`. If you want to revert multiple commits: `git revert 2f50d7dd1dc4874b7ca6054099b54^..af0e737a28e0d5c816912a336`. Make sure to revert changes in chronological order, starting with the newest commit first.
5.  If there are conflicts during the revert process, resolve them manually by editing the conflicting files and then continue with the revert process.
6. After resolving any conflicts, commit and push the changes to your remote Git repository.
7. Once your changes have been reverted, you can pull them in the Studio app to deploy the changes.

## Git best practices

### Use a branching strategy

Implement a well-defined branching strategy to enhance collaboration and maintain code quality in Git:

- [x] Select a branching model that aligns with your team's workflow and project requirements. Popular models like [GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow), and [Trunk-Based Development](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development) offer different approaches suited for various scenarios. 
- [x] Create different feature branches from the `Staging` branch and merge them into `Staging` regularly through pull requests.
- [x] Create a `Staging` branch for testing features. Once a milestone is done, merge the `Staging` branch into the `master` branch via a pull request.
- [x] Reserve the `master` branch for production-ready code. Only merge thoroughly tested and reviewed changes into this branch to ensure stability.
- [x] To prevent accidental commits, make the `master` [branch protected](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) in Github settings.
- [x] Keep branches and pull requests short-lived to streamline the development process and minimize conflicts.

### Avoid merge conflicts

While working with Git, you may face merge conflicts. To avoid these conflicts, follow these best practices:

- [x] Break down changes into small, self-contained updates that address a single concern. Each commit should represent a single logical change or fix. 
- [x] Multiple developers should avoid making changes to the same UI elements on the same page, even if they are working on different branches
- [x] Pull changes frequently to incorporate updates from the remote repository into your local branch. 
- [x] Merge changes from the `master` branch regularly into the `feature` branch to keep it updated with the latest developments. You can do this by clicking on the **Merge icon** at the bottom left and merging changes from the `master` branch to the `feature` branch.
- [x] Divide work among developers so each person is responsible for different parts of the app to avoid overlap and conflicts.
- [x] Communicate with your teammates before making any changes to ensure coordination.
