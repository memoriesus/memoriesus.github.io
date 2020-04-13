---
post: page
title: install Bazel on macOS
tags: [Bazel]
comment: true 
---

# Step 1: Install Homebrew on MacOS
`/usr/bin/ruby -e "$(curl -fsSL \
https://raw.githubusercontent.com/Homebrew/install/master/install)"`

# Step2 : Install Bazel homebrew package
`brew tap bazelbuild/tap`
`brew installl bazelbuild/tap/bazel`
All set, you must confirm Bazel is installed successfully via the command as below:
`bazel --version`
Once installed, you can upgrade to the latest version of Bazel
`brew upgrade bazelbuild/tap/bazel`
**Noted:If your system has the Bazel package from homebrew core installed your need to uninstall it by type**
 **brew uninstall bazel**




