[# nodejs
nodejs
](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04


To get this version, you can use the apt package manager. Refresh your local package index first:

sudo apt update
Then install Node.js:

sudo apt install nodejs
Check that the install was successful by querying node for its version number:

node -v
Output
v10.19.0
If the package in the repositories suits your needs, this is all you need to do to get set up with Node.js. In most cases, you’ll also want to also install npm, the Node.js package manager. You can do this by installing the npm package with apt:

sudo apt install npm
This allows you to install modules and packages to use with Node.js.

At this point, you have successfully installed Node.js and npm using apt and the default Ubuntu software repositories. The next section will show how to use an alternate repository to install different versions of Node.js.

Option 2 — Installing Node.js with Apt Using a NodeSource PPA
To install a different version of Node.js, you can use a PPA (personal package archive) maintained by NodeSource. These PPAs have more versions of Node.js available than the official Ubuntu repositories. Node.js v16 and v18 are available as of the time of writing.

First, install the PPA to get access to its packages. From your home directory, use curl to retrieve the installation script for your preferred version, making sure to replace 16.x with your preferred version string (if different):

cd ~
curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh
Refer to the NodeSource documentation for more information on the available versions.

Inspect the contents of the downloaded script with nano or your preferred text editor:

nano /tmp/nodesource_setup.sh
When you are satisfied that the script is safe to run, exit your editor. Then run the script with sudo:

sudo bash /tmp/nodesource_setup.sh
The PPA will be added to your configuration and your local package cache will be updated automatically. You can now install the Node.js package in the same way you did in the previous section:

sudo apt install nodejs
Verify that you’ve installed the new version by running node with the -v version flag:

node -v
Output
v16.19.0
The NodeSource nodejs package contains both the node binary and npm, so you don’t need to install npm separately.

At this point, you have successfully installed Node.js and npm using apt and the NodeSource PPA. The next section will show how to use the Node Version Manager to install and manage multiple versions of Node.js.

Option 3 — Installing Node Using the Node Version Manager
Another way of installing Node.js that is particularly flexible is to use nvm, the Node Version Manager. This piece of software allows you to install and maintain many different independent versions of Node.js, and their associated Node packages, at the same time.

To install NVM on your Ubuntu 20.04 machine, visit the project’s GitHub page. Copy the curl command from the README file that displays on the main page. This will get you the most recent version of the installation script.

Before piping the command through to bash, it is always a good idea to audit the script to make sure it isn’t doing anything you don’t agree with. You can do that by removing the | bash segment at the end of the curl command:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh
Review the script and make sure you are comfortable with the changes it is making. When you are satisfied, run the command again with | bash appended at the end. The URL you use will change depending on the latest version of nvm, but as of right now, the script can be downloaded and executed with the following:

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
This will install the nvm script to your user account. To use it, you must first source your .bashrc file:

source ~/.bashrc
Now, you can ask NVM which versions of Node are available:

nvm list-remote
Output
. . .
        v18.0.0
        v18.1.0
        v18.2.0
        v18.3.0
        v18.4.0
        v18.5.0
        v18.6.0
        v18.7.0
        v18.8.0
        v18.9.0
        v18.9.1
       v18.10.0
       v18.11.0
       v18.12.0   (LTS: Hydrogen)
       v18.12.1   (LTS: Hydrogen)
       v18.13.0   (Latest LTS: Hydrogen)
        v19.0.0
        v19.0.1
        v19.1.0
        v19.2.0
        v19.3.0
        v19.4.0
It’s a very long list. You can install a version of Node by writing in any of the release versions listed. For instance, to get version v14.10.0, you can run:

nvm install v14.10.0
You can view the different versions you have installed by listing them:

nvm list
Output
->     v14.10.0
       v14.21.2
default -> v14.10.0
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v14.21.2) (default)
stable -> 14.21 (-> v14.21.2) (default)
. . .
This shows the currently active version on the first line (-> v14.10.0), followed by some named aliases and the versions that those aliases point to.

Note: if you also have a version of Node.js installed through apt, you may receive a system entry here. You can always activate the system-installed version of Node using nvm use system.

Additionally, there are aliases for the various long-term support (or LTS) releases of Node:

Output
lts/* -> lts/hydrogen (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.2
lts/gallium -> v16.19.0 (-> N/A)
lts/hydrogen -> v18.13.0 (-> N/A)
You can install a release based on these aliases as well. For instance, to install the latest long-term support version, hydrogen, run the following:

nvm install lts/hydrogen
Output
Downloading and installing node v18.13.0...
. . .
Now using node v18.13.0 (npm v8.19.3)
You can switch between installed versions with nvm use:

nvm use v14.10.0
Output
Now using node v14.10.0 (npm v6.14.8)
```

You can verify that the install was successful using the same technique from the other sections:

```command
node -v
Output
v14.10.0
The correct version of Node is installed on your machine as expected. A compatible version of npm is also available.

Removing Node.js
You can uninstall Node.js using apt or nvm, depending on how it was installed. To remove the version from the system repositories, use apt remove:

sudo apt remove nodejs
By default, apt remove retains any local configuration files that were created since installation. If you don’t want to save the configuration files for later use, use apt purge:

sudo apt purge nodejs
To uninstall a version of Node.js that you installed using nvm, first determine whether it is the current active version:

nvm current
If the version you are targeting is not the current active version, you can run:

nvm uninstall node_version
Output
Uninstalled node node_version
This command will uninstall the selected version of Node.js.

If the version you would like to remove is the current active version, you first need to deactivate nvm to enable your changes:

nvm deactivate)
