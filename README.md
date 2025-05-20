# Terraform Setup in AWS CloudShell

This repository provides a quick guide to installing and running [Terraform](https://www.terraform.io/) inside **AWS CloudShell** — a browser-based shell provided by AWS for managing cloud resources.

## Why Use Terraform in AWS CloudShell?

AWS CloudShell provides:
- Secure and pre-authenticated access to your AWS environment.
- Persistent $HOME directory for storing configuration files and binaries.
- No local setup required — use Terraform from any browser.

However, Terraform does **not come pre-installed** in AWS CloudShell. 

This guide enables you to set it up manually.

---

## Installation Script

1. Run the following scripts in **AWS CloudShell** to install Terraform:

To fully install and use tfenv, you typically need to add the ~/bin directory to your system's PATH environment variable. This allows you to run tfenv commands from any directory in your terminal.

Here are the complete steps, incorporating the commands you provided:

Clone tfenv:

```
git clone https://github.com/tfutils/tfenv.git ~/.tfenv

```
Create a local bin directory (if it doesn't exist):

```
mkdir ~/bin
```
or
```
mkdir -p ~/bin
```
(Using -p ensures the directory is created only if it doesn't exist, preventing errors.)

Create symbolic links:

```
ln -s ~/.tfenv/bin/* ~/bin/

```
Install a Terraform latest version

```

tfenv install latest

```
Verify tfenv installation:

```

tfenv --version

```

This should output the tfenv version.

You can use tfenv to install specific Terraform versions. For example, to install the latest stable version:

```
tfenv install latest
```

Or a specific version:
```
tfenv install 1.6.5
```
You can then switch between installed versions using:

```
tfenv use 1.6.5
```
And verify the Terraform version:

```Bash

terraform --version
```
By following these steps, you'll have tfenv fully set up and ready to manage your Terraform installations.
Feedback & Contributions

Feel free to submit issues or pull requests if you’d like to improve this setup or add enhancements.

