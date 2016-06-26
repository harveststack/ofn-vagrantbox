# ofn-vagrantbox

Just based on a [railsbox](http://railsbox.io) template and got me a good deal of the way there.

Put the directory with the Open Food Network codebase at the top level of this directory and name it 'openfoodnetwork'.

Run the following commands to start/stop/etc the server.

`
vagrant up                      # To start VM
vagrant provision               # To re-run ansible playbook
vagrant halt                    # To stop VM
vagrant destroy                 # To destroy VM completely
`

If you edit your hosts file on the HOST machine `sudo vim /private/etc/hosts` adding the following:

`
## For ofn dev
192.168.20.50   ofn.dev
## ./For ofn dev
`

Then run `dscacheutil -flushcache` and you should be able to access the OFN site at http://ofn.dev

=AFTER YOU FIRST=
Follow the instructions at [OFN Wiki](https://github.com/openfoodfoundation/openfoodnetwork), starting from about the part that says "Create the development and test databases, using the settings specified in config/database.yml, and populate them with a schema and seed data:"
