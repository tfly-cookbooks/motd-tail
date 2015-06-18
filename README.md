Description
===========

Updates motd.tail with Chef Roles

Requirements
============

Needs to be used on a system that utilizes /etc/motd.tail, e.g. Ubuntu.

Attributes
==========

* `node['motd-tail']['additional_text']` - Additional text to add to the end
  of the motd.tail (e.g. unauthorized access banner).

Usage
=====

```json
"run_list": [
    "recipe[motd-tail]"
]
```

default
----

Updates motd.tail with useful node data

Examples
--------

For example,

    % ssh myserver.int.example.org
    ***
    Chef-Client - myserver.int.example.org
    ubuntu
    samba_server
    netatalk_server
    munin_server
    rsyslog_server
    ***

    Additional text here when `node['motd-tail']['additional_text']` present.


Set additional_text in a role:

    "default_attributes": {
      "motd-tail": {
        "additional_text": {
           "ROLE_MESSAGE": "All servers with this role will have this message."
        }
      }
    },


Set additional_text directly on a node:

    "default_attributes": {
      "motd-tail": {
        "additional_text": {
           "ANOTHER_MESSAGE": "The node with this set will have this message."
        }
      }
    },


With both of these set motd-tail will look like this:

    % ssh myserver.int.example.org
    ***
    Chef-Client - myserver.int.example.org
    ubuntu
    samba_server
    netatalk_server
    munin_server
    rsyslog_server
    ***
    
    ROLE_MESSAGE": All servers with this role will have this message.
    ANOTHER_MESSAGE: The node with this set will have this message.

Testing
=====

This cookbook is using [ChefSpec](https://github.com/acrmp/chefspec) for testing.

    % cd $repo
    % bundle
    % librarian-chef install
    % ln -s ../ cookbooks/motd-tail
    % rspec cookbooks/motd-tail

License and Author
==================

Author:: Nathan Haneysmith <nathan@chef.io>

Copyright:: 2009-2012, Chef Software, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
