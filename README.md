# Jamie LXC

The LXC driver for the Chef convergence integration test harness, [Jamie](https://github.com/jamie-ci/jamie).

## Installation

Add this line to your Chef cookbooks's Gemfile:

    gem 'jamie-lxc'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install jamie-lxc

## Usage

### Configuration

`.jamie.yml`

```
driver_plugin: lxc

platforms:
  - name: distribution
    driver_config:
      base_container: "distribution-release" # your base container name
      username: "foo" # defaults to "jamie"
      password: "bar" # defaults to "jamie"

suites:
  - name: default
    run_list:
      - "recipe[cookbook::recipe]"
```

### Example

```
$ jamie create
-----> Starting Jamie
-----> Creating <default-ubuntu>
       [lxc command] BEGIN (sudo lxc-clone -o ubuntu-1204 -n default-ubuntu-a5fb8a)
       Tweaking configuration
       Copying rootfs...
       Updating rootfs...
       'default-ubuntu-a5fb8a' created
       [lxc command] END (0m6.17s)
       [lxc command] BEGIN (sudo lxc-start -n default-ubuntu-a5fb8a -d)
       [lxc command] END (0m0.01s)
       [lxc command] BEGIN (sudo lxc-wait -n default-ubuntu-a5fb8a -s RUNNING)
       [lxc command] END (0m1.05s)
       Finished creating <default-ubuntu> (0m7.42s).
-----> Creating <default-centos>
       [lxc command] BEGIN (sudo lxc-clone -o centos-6 -n default-centos-58fced)
       Tweaking configuration
       Copying rootfs...
       Updating rootfs...
       'default-centos-58fced' created
       [lxc command] END (0m6.68s)
       [lxc command] BEGIN (sudo lxc-start -n default-centos-58fced -d)
       [lxc command] END (0m0.02s)
       [lxc command] BEGIN (sudo lxc-wait -n default-centos-58fced -s RUNNING)
       [lxc command] END (0m1.05s)
       Finished creating <default-centos> (0m13.92s).
-----> Jamie is finished. (0m21.45s)
$ jamie destroy
-----> Starting Jamie
-----> Destroying <default-ubuntu>
       [lxc command] BEGIN (sudo lxc-destroy -n default-ubuntu-a5fb8a -f)
       [lxc command] END (0m1.18s)
       Finished destroying <default-ubuntu> (0m1.21s).
-----> Destroying <default-centos>
       [lxc command] BEGIN (sudo lxc-destroy -n default-centos-58fced -f)
       [lxc command] END (0m1.14s)
       Finished destroying <default-centos> (0m1.17s).
-----> Jamie is finished. (0m2.45s)
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
