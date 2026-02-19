# DAML SDK

## Installation

One of the best resources you'll use as you learn DAML and Canton is the https://docs.daml.com/ website.

To properly install the Daml SDK, refer to the installation guide at:

https://docs.daml.com/getting-started/installation.html

If you have questions about the installation process, use the DAML Discuss forum at:

https://discuss.daml.com/

## Guide (Installing SDK)

1. **Install DAML SDK**
   a. Get shell version: `echo $SHELL`
   b. Install DAML SDK: `curl -sSL https://get.daml.com/ | sh`
   c. Run:
   ```
   echo "export PATH=$HOME/.daml/bin:$PATH" >> ~/.zshrc
   echo "fpath=(~/.daml/zsh $fpath)" >> ~/.zshrc
   source ~/.zshrc
   ```
   d. Test DAML SDK: `daml version`
2. **Get JDK 11 or higher**
   a. Get shell version: `echo $SHELL`
   b. Verify JDK version: `java -version` (should be 11 or higher)
   c. Set JAVA_HOME environment variable (if not set):
   ```
   echo 'export JAVA_HOME="$(/usr/libexec/java_home)"' >> ~/.zprofile
   echo 'export PATH="$HOME/.daml/bin:$PATH"' >> ~/.zprofile
   ```
   d. Test config: `echo $JAVA_HOME` in a new shell
