Part Management
============

Part Management is a web-based system for tracking parts through the design and manufacture cycle. It assigns
part numbers with which CAD files can be saved to version control and stores information about parts'
current manufacturing status.

Part Managemenet is written in Ruby using the [Sinatra](http://sinatrarb.com) framework and uses MySQL as the
backing datastore. Development and production are run on Linux (Arch, Ubuntu), and is not designed to work on Windows.

## Development

Prerequisites:

* Ruby 1.9 (1.9.3-p286 is what we use in development and production)
* [Bundler](http://gembundler.com)
* MySQL

To run Cheesy Parts locally:

1. Create an empty MySQL database and a user account with full permissions on it.
1. Populate `config.json` with the parameters for the development and production environments. Set
`enable_wordpress_auth` to false and `members_url` to blank; they are used for a single sign-on (SSO)
mechanism specific to Team 254.
1. Run `bundle install`. This will download and install the gems that Cheesy Parts depends on.
1. Run `bundle exec rake db:migrate`. This will run the database migrations to create the necessary tables in
MySQL.
1. Run `ruby parts_server_control.rb <command>` to control the running of the Cheesy Parts server, where
`<command>` can be one of `start`|`stop`|`run`|`restart`.

The database migration will create an admin account (username "deleteme@team254.com", password "chezypofs")
that you can use to first get into the system and create other accounts. It is highly recommended that you
delete this account after having created your own admin account.

## Deployment

Cheesy Parts deploys by checking out from Git on the production server. If you don't plan on making any
changes, you can simply put a copy of the code on your server and edit the config in place. If you do plan on
making periodic changes to the code, you can follow this procedure:

1. Fork cheesy-parts on Github, make your initial code/config changes, and commit them.
1. On the production server, clone your fork and start it up the first time.
1. Fill in your server-specific information in the `deploy` script.
1. Make any incremental changes in your development machine, test them locally, commit and push them, then run
the `deploy` script.

The deploy script uses SSH to log into the production server, discard any local changes in the checked-out
version of Cheesy Parts, pull from the origin, and restart the server.

## Contributing

If you're on the VexU team or otherwise want to contribute back to our fork, great! Create an issue or shoot an email to [blward@wpi.edu](mailto:blward@wpi.edu), or open a pull request if you have some Ruby-fu. 

Otherwise, you can contribute to the original project back at [Team254/cheesy-parts](https://github.com/Team254/cheesy-parts).
