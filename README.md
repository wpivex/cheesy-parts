Cheesy Parts
============

Cheesy Parts is a web-based system for tracking parts through the design and manufacture cycle. It assigns
part numbers with which CAD files can be saved to version control and stores information about parts'
current manufacturing status.

Cheesy Parts is written in Ruby using the [Sinatra](http://sinatrarb.com) framework and uses MySQL as the
backing datastore. Development and production are run on UNIX (OS X and Ubuntu), so there are no guarantees
it'll work on Windows, sorry.

## Team 199 Specific Features

Our fork differs from 254's in a few ways:

1. Users can edit their own account settings, including passwords, names, and one of several stylesheets.
1. Workflow, status options, and other attributes are generally optimized for our team's resources.
1. Secure file upload is added so that members with edit privileges may upload drawings, documentation, and toolpath files. Each part and assembly carries revision letters that are automatically managed by the program. Lite version control is offered, with the ability to restore previous revisions if user is an administrator.
1. Slack and Trello integeration is offered, since our team uses both tools for communication and task tracking.
1. Additional dashboards and reports are offered for use.

## Development

Prerequisites:

* Ruby 2.3 and developmment packages
* [Bundler](http://gembundler.com)
* MySQL and development packages
* g++

To run Cheesy Parts locally:

1. Create an empty MySQL database and a user account with full permissions on it.
1. Populate `config.json` with the parameters for the development and production environments. Set
`enable_wordpress_auth` to false and `members_url` to blank; they are used for a single sign-on (SSO)
mechanism specific to Team 254. Make sure to add your Slack and Trello API tokens.
1. Run `bundle install`. This will download and install the gems that Cheesy Parts depends on.
1. Run `bundle exec rake db:migrate`. This will run the database migrations to create the necessary tables in
MySQL.
1. Run `ruby parts_server_control.rb <command>` to control the running of the Cheesy Parts server, where
`<command>` can be one of `start`|`stop`|`run`|`restart`.

The database migration will create an admin account (username "deleteme@team254.com", password "chezypofs")
that you can use to first get into the system and create other accounts. It is highly recommended that you
delete this account after having created your own admin account.

## Contributing

If you have a suggestion for a new feature in Cheesy Parts, create an issue on GitHub or shoot an e-mail to
[pat@patfairbank.com](mailto:pat@patfairbank.com). Or if you have some Ruby-fu and are feeling adventurous,
fork Team 254 and send a pull request. If you are interested in modifying or using our fork, don't hesitate to reach out.
