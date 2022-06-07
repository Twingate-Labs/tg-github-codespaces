# Twingate + GitHub CodeSpaces
Example of Github Codespaces with Twingate

## What this is
[GitHub Codespaces](https://github.com/features/codespaces) is a service from GitHub that provides a way for developers to run a full development environment entirely within the cloud and accessible via a web-browser or via [VisualStudio Code](https://code.visualstudio.com).

This repository provides an example of how to configure a Twingate client running with either a [Service Account](https://docs.twingate.com/docs/services) (default) or as a regular user.
Codespaces users will then be able to access private resources such as internal databases or APIs that are protected behind Twingate directly from their web-browser or from within VS Code.

## Getting started

### Prerequisites
1. Ensure you have a GitHub repository that you'd like to open with CodeSpaces and ensure you have permissions to launch CodeSpaces.  You may need assistance from your organization's GitHub Administrator.
2. Ensure that there exists a `.devcontainer` directory in your repository
3. Copy the `Dockerfile` from `.devcontainer` in this repository to the same location in your repository.

#### Connect using a Twingate Service Account Key
1. Ensure you have a Service Account Key - this can be generated within the Twingate Admin Console (you may need to ask your Twingate Administrator to do this for you).
2. Copy the file `devcontainer.serviceaccount.json` to the `.devcontainer` directory in your respository and rename it to `devcontainer.json`.
3. Create a Codespaces [User Secret](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-encrypted-secrets-for-your-codespaces#adding-a-secret) named `TWINGATE_SERVICE_KEY`
4. Start your Codespaces instance and confirm that Twingate is connected by running `twingate status` - it should return `online`
   1. You can run `twingate resources` to obtain a list of resource
   2. In case of problems please run `sudo twingate report` and send the report file to support@twingate.com

#### Connect using a regular Twingate account (interactive login)
1. Copy the file `devcontainer.interactive.json` to the `.devcontainer` directory in your respository and rename it to `devcontainer.json`.
2. Start your Codespaces instance and connect it to your Twingate account using `sudo twingate setup`
3. Once your Twingate account is configured you can begin login using `twingate start`  (**note**: be sure to execute this _without_ `sudo`)
4. Run `/usr/bin/twingate-notifier console` (**note**: be sure to execute this _without_ `sudo`)
   1. You should follow the URL displayed and authenticate through your web-browser
   2. You can run `twingate resources` to obtain a list of resource
   3. In case of problems please run `sudo twingate report` and send the report file to support@twingate.com

## Feedback, improvements, comments
Please open an issue or submit a Pull Request in this repository with any feedback you may have.