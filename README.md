# Dot Files for West Arete

These are the common dot files that we share across our home directories.

As of yet, there is no fancy installation script; just manually put these in
place, or blend them with what you have now. 

They're named here without the leading dot, so that the repository is easy to
work with. You'll need to rename them e.g. from `gemrc` to `~/.gemrc` when you
install them.

Rakefile Semantics
==================

This rakefile is what is used to do all sorts of deploy related things. The available options are:

* `rake` - usage information (aliased to `rake default`) 
* `rake default` - usage information
* `rake deploy[projectname,environment]` - deploy site to (beta | staging | production)
* `rake destroy[projectname,environment]` - destroy a site's server
* `rake list` - list all chef-ed servers and roles
* `rake verifyChef` - verify that chef is correctly installed and operational

example: `rake deploy[redi,beta]` or `rake destroy[prometheus,staging]`

Notes on the arguments: 

* rake is a really particular tool. DO NOT PUT SPACES AFTER COMMAS. bad: `rake deploy[redi, staging]` -> good: `rake deploy[redi,staging]`
* `projectname` - this is the actual github project name [ex: centre-foundation.org or redi or admin.thepilgrimage.org ]
* `environment` - this is one of {beta, staging, production}

Rakefile Setup
==============

The rake file is quite robust, but there are some specifics about locations and naming that are important. Here is an idea of the proper usage, what to expect and just enough about how things work to guarantee you'll have a good time.

1. There is an expectation that you have a "westarete" directory that will contain chef (and possibly other projects). It doesn't need to be named anything specifically, but it must exist and be where you install chef. (^)
2. You must have chef installed. See the chef-repo for how to do that. Do this in your "westarete" directory.
3. You must clone this repo also into your "westarete" directory.
* `git clone git@github.com:westarete/dotfiles.git your/westarete/directory/path/dotfiles`
* `cd your/westarete/directory/path/dotfiles/`
* `git checkout anatraj`

(^) Optional: You can save yourself one line of questioning and typing in the rake task by setting an environment variable for the path to your "westarete" directory. To do this for just one session inside the terminal, 
`export WESTARETE=path/to/westarete/directory/`
To do this permanently, you must add the prior command to your `/etc/profile` text file. It doesn't matter where in the file (top or bottom). You will need to restart your terminal to see the effects. To test if it worked, `echo $WESTARETE` should print the path.

Rakefile usage
==============

There is no need to use the `verifyChef` rake task. It is automatically called by every other task as a dependency.

Deploy a project (new or already existing):
Checks for a server and will create if none is found. If it doesn't exist it will ask you interactively what roles you would like to provide for the server. You must enter some roles or recipes when it asks.
* for a rails app: `role[railsapp]` with postgre: `role[railsapp], recipe[postgre]`
* a php site: `role[phpsite]`
* a static page: `role[webserver]`
Once you've entered the roles you want (or not if the server already exists), the hard work is done! It will deploy the site properly the capistrano way. It will say "done" when it is all deployed.
Example: `rake deploy[redi,beta]` with roles `role[railsapp], recipe[postgre]` or `rake deploy[pasubway.com,beta]` with roles `role[webserver]`


Destroy a server for a project:
Will ask you if you are sure, then destroy the server and its dns records. Very simple, maybe too simple?
Example: `rake destroy[redi,beta]`, `rake destroy[secureport,staging]`

List all servers:
Will list all the servers that have been deployed using this rake tool, or via chef. It will also display their IPs and their role lists.
Example: `rake list`