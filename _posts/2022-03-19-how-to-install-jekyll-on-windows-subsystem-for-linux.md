---
title: How to Install Jekyll on Windows Subsystem for Linux
categories:
  - Help File
tags:
  - Linux
  - Windows
---

If you try to install [Jekyll](https://jekyllrb.com/) on a base install of Windows Subsystem for Linux (WSL), you'll run into a few errors. This is because we need to be able to build Jekyll, but the required compilers, libraries, and utilities we need to do so are not installed by default. Luckily it is a simple fix that requires just a few terminal commands.

This guide uses Ubuntu 20.04, but it should work equally well on any Debian-flavor Linux variant.

Before we begin, make sure your system is up to date.

```sh
    sudo apt update
    sudo apt upgrade
```

First, we want to install the latest version of Ruby and the essential build tools.

```sh
    sudo apt install -y ruby-full build-essential zlib1g-dev
```

Next, we need to update a few environment variables. These tell the shell where to look for our Ruby Gems.

```sh
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
```

Third, we need to install the Ruby package called Bundler. Don't worry too much about what it does, just note that we need it for Jekyll to work properly.

```sh
    gem install bundler
```

Finally, we install Jekyll. This command may take a minute or two to finish.

```sh
    gem install jekyll
```

Now you are up and ready to go. You can use the standard Jekyll commands to create and view your website.

```sh
    jekyll new my-awesome-site
    cd my-awesome-site
    bundle exec jekyll serve --drafts --force_polling
    # => Now browse to http://localhost:4000
```

One final note. You may notice that the auto-regenerate feature of Jekyll does not work correctly under WSL. To fix this, we simply need to add the `--force_polling` option when we run the server. You'll see we added this option to the command above.

That's it! [Let me know](/about) if I got anything wrong, or send me some comments if you run into trouble.

----

# Q&A

### What does the `--drafts` option do?

There are two ways to manage drafts in Jekyll. One is to have a post in the `"_posts"` folder with a date greater than the current date, and the other is have a separate `"_drafts"` folder. Running the server with the `--drafts` option tells Jekyll to go ahead and show your drafts as if they are published, allowing you to see a preview before going live.
