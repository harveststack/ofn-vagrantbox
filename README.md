# ofn-vagrantbox

Just based on a [railsbox](http://railsbox.io) template and got me a good deal of the way there.

Put the directory with the Open Food Network codebase at the top level of this directory and name it 'openfoodnetwork'.

From _within_ the `development` dirrectory, run the following commands to start/stop/etc the server.

```
vagrant up                      # To start VM
vagrant provision               # To re-run ansible playbook
vagrant halt                    # To stop VM
vagrant destroy                 # To destroy VM completely
```

If you edit your hosts file on the HOST machine `sudo vim /private/etc/hosts` adding the following:

```
## For ofn dev
192.168.20.50   ofn.dev
## ./For ofn dev
```

Then run `dscacheutil -flushcache` and you should be able to access the OFN site at http://ofn.dev

=AFTER YOU FIRST=
Follow the instructions at [OFN Wiki](https://github.com/openfoodfoundation/openfoodnetwork), starting from about the part that says "Create the development and test databases, using the settings specified in config/database.yml, and populate them with a schema and seed data:"

Get into the new Virtualbox server with command `vagrant ssh`. You will be user `vagrant` and the OFN codebase that is on your local computer will be synced with the directory "openfodnetwork" in the `vagrant` users home directory on the VM. So that's where you'll go to do stuff with `rails`, `bundle` and `rake` commands, etc. 

Don't forget to make a note of the admin_email: and admin_pass: (we're using 'f00dies') when the rake task creates the Spree admin user.

If there's errors in the rake task you may need to delete and recreate the postgres databases: 'open_food_network_dev' and 'open_food_network_test'. This is done by:

1. Become postgres user: `sudo -u -i postgres`
2. Use postgres: `psql`
3. Drop a database like this: `drop database open_food_network_dev`.
4. If you cannot drop with an error that there are users connected, use this code:

```SELECT pg_terminate_backend(pg_stat_activity.pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = 'open_food_network_dev'
  AND pid <> pg_backend_pid();```

(Do the same for both databases.)

Now quit psql like `\q` and go back to user, `vagrant` with `logout`. Try the rake command again.

Good luck!

Oh yea - also you probably want to run the server like this:

`bundle exec rails server -b 0.0.0.0`.
