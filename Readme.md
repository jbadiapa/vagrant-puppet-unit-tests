This environment is ready to run puppet unit test.
It's very helpfull to develop them.

[localhost]$ vagrant ssh
[vagrant@puppet ~]$ cd puppet-tripleo
[vagrant@puppet puppet-tripleo]$ bundle exec rake spec

To enable the debug on console drop the following lines 
 Puppet::Util::Log.level = :debug
 Puppet::Util::Log.newdestination(:console)
into puppet-tripleo/spec/spec_helper.rb
