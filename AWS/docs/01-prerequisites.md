# Prerequisites

## AWS

This tutorial leverages [Amazon Web Services](https://aws.amazon.com//) to streamline provisioning of the compute infrastructure required to bootstrap a Kubernetes cluster from the ground up. This will cost you money; if that's a concern consider instead using the original [Google Cloud version](https://github.com/petabloc/kubernetes-the-hard-way/tree/main/GCP) of this tutorial, as Google offers $300 in free credits.

Estimated cost to run this tutorial: UPDATE LATER AFTER WE FINISH THE DOCS in this format: $0.XX per hour ($Y.ZZ per day).

> The compute resources required for this tutorial exceed the AWS free tier.

## AWS CLI

### Install the AWS CLI

Follow the AWS [documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) to install and configure the `aws` command line utility.

Verify the AWS CLI version is 2.7.19 or higher:

```
aws version
```

### Set a Default Compute Region and Zone

This tutorial assumes a default account and region have been configured in your AWS CLI configuration.

If you are using the `aws` command-line tool for the first time `configure` is the easiest way to do this:

```
aws configure
```

### Directory Structure
It is recommended you create a separate "working" directory.  This tutorial generates a lot of files and we don't want them accidentally getting mixed in with the repo.

## Running Commands in Parallel with tmux

[tmux](https://github.com/tmux/tmux/wiki) can be used to run commands on multiple compute instances at the same time. Labs in this tutorial may require running the same commands across multiple compute instances, in those cases consider using tmux and splitting a window into multiple panes with synchronize-panes enabled to speed up the provisioning process.

> The use of tmux is optional and not required to complete this tutorial.

![tmux screenshot](images/tmux-screenshot.png) // TODO fix screenshot

> Enable synchronize-panes by pressing `ctrl+b` followed by `shift+:`. Next type `set synchronize-panes on` at the prompt. To disable synchronization: `set synchronize-panes off`.

Next: [Installing the Client Tools](02-client-tools.md)
