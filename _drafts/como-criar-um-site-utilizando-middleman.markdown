---
layout: post
title:  "Middleman - criando um novo site estático"
categories: [middleman]
---
Middleman is distributed using the RubyGems package manager. This means you will need both the Ruby language runtime installed and RubyGems to begin using Middleman.

Mac OS X comes prepackaged with both Ruby and Rubygems, however, some of the Middleman's dependencies need to be compiled during installation and on OS X that requires Xcode. Xcode can be installed via the Mac App Store. Alternately, if you have a free Apple Developer account, you can just install Command Line Tools for Xcode from their downloads page.

Once you have Ruby and RubyGems up and running, execute the following from the command line:

{% highlight shell %}
$ gem install middleman
{% endhighlight %}

This will install Middleman, its dependencies and the command-line tools for using Middleman.

The installation process will add one new command to your environment, with 3 useful features:

{% highlight shell %}
$ middleman init
$ middleman server
$ middleman build
{% endhighlight %}


To get started we will need to create a project folder for Middleman to work out of. You can do this using an existing folder or have Middleman create one for you using the middleman init command.

Simply point the command at the folder for your new site and Middleman will build a skeleton project in that folder (or create the folder for you).

$ middleman init my_new_project

The Skeleton

Every new project creates a basic web development skeleton for you. This automates the construction of a standard hierarchy of folders and files that you can use in all of your projects.

A brand-new project will contain a source folder and a config.rb file. The source folder is where you will build your website. The skeleton project contains folders for javascript, CSS and images, but you can change these to match your own personal preferences.

The config.rb file contains settings for Middleman and commented documentation on how to enable complex features such as compile-time compression and "blog mode".
Gemfile

Middleman will respect a Bundler Gemfile for specifying and controlling your gem dependencies. When creating a new project, Middleman will generate a Gemfile for you which specifies the same version of Middleman you are using. This will lock Middleman to this specific release series (the 3.0.x series, for example). You can also use your Gemfile to use cutting-edge versions of Middleman from GitHub using the :git option. All plugins and extra libraries you use in your project should be listed in your Gemfile, and Middleman will automatically require all of them when it starts.
config.ru

A config.ru file describes how the site should be loaded by a Rack-enabled webserver. This file is provided as a convenience for users wishing to host their Middleman site in development mode on a Rack-based host such as Heroku. Remember that Middleman is built to generate static sites, though.

To include a boilerplate config.ru file in your project, add the --rack flag to the init command:

$ middleman init my_new_project --rack

If you've already initialized a project and just want the config.ru for linking with pow or other development server its contents are simply:

require 'middleman/rack'
run Middleman.server
