# Twingate + GitHub Codespaces
Example of Github Codespaces with Twingate

## What this is
[GitHub Codespaces](https://github.com/features/codespaces) is a service from GitHub that provides a way for developers to run a full development environment entirely within the cloud and accessible via a web-browser or via [VisualStudio Code](https://code.visualstudio.com).

This repository provides an example of how to configure a [Twingate](https://twingate.com) client running with either a [Service Account](https://docs.twingate.com/docs/services) (default) or as a regular user.
Codespaces users will then be able to access private resources such as internal databases or APIs that are protected behind Twingate directly from their web-browser or from within VS Code.

_Note_: For connecting your GitHub workflows to private resources please also see the [Connect to Twingate](https://github.com/marketplace/actions/connect-to-twingate) GitHub Action.

## Getting started

### Prerequisites
1. Ensure you have a GitHub repository that you'd like to open with Codespaces and ensure you have permissions to launch Codespaces.  You may need assistance from your organization's GitHub Administrator.
2. Ensure that there exists a `.devcontainer` directory in your repository
3. Copy the `Dockerfile` from `.devcontainer` in this repository to the same location in your repository.

#### Connect using a Twingate Service Account Key
1. Ensure you have a Service Account Key - this can be generated within the Twingate Admin Console (you may need to ask your Twingate Administrator to do this for you).
2. Copy the file `devcontainer.serviceaccount.json` to the `.devcontainer` directory in your respository and rename it to `devcontainer.json`.
3. Create a Codespaces [User Secret](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-encrypted-secrets-for-your-codespaces#adding-a-secret) named `TWINGATE_SERVICE_KEY` set to your Twingate Service Account Key.
4. Start your codespace and confirm that Twingate is connected by running `twingate status` - it should return `online`
   1. Run `twingate resources` to obtain a list of resources
   2. In case of problems please run `sudo twingate report` and send the report file to support@twingate.com.

#### Connect using a regular Twingate account (interactive login)
1. Copy the file `devcontainer.interactive.json` to the `.devcontainer` directory in your respository and rename it to `devcontainer.json`.
3. Create a Codespaces [Secret](https://docs.github.com/en/codespaces/managing-codespaces-for-your-organization/managing-encrypted-secrets-for-your-repository-and-organization-for-codespaces) named `TWINGATE_ACCOUNT` set to your Twingate Account Name. For example, if your Twingate account is `acme.twingate.com` then set the value to `acme`.
3. Run `twingate status`  (**note**: be sure to execute these commands _without_ `sudo`)
   1. If status is `authenticating` you should follow the URL displayed to authenticate
   2. If status is `not running` then execute `twingate start` and then `/usr/bin/twingate-notifier console` and follow the URL displayed to authenticate
   3. Once `online`, run `twingate resources` to obtain a list of resources
   4. In case of problems please run `sudo twingate report` and send the report file to support@twingate.com.

## Feedback, improvements, comments
Please open an issue or submit a Pull Request in this repository with any feedback you may have.
