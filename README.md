yum-pgdg Cookbook
============
[![Build Status](https://travis-ci.org/chef-cookbooks/yum-pgdg.svg?branch=master)](http://travis-ci.org/chef-cookbooks/yum-pgdg)
[![Cookbook Version](https://img.shields.io/cookbook/v/yum-pgdg.svg)](https://supermarket.chef.io/cookbooks/yum-pgdg)

The yum-pgdg cookbook takes over management of the default
repositoryids that ship with pgdg. It allows attribute
manipulation of `pgdg`.

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['pgdg']['repositoryid'] = 'pgdg-9.3'
default['yum']['pgdg']['baseurl'] = 'http://yum.pgrpms.org/9.3/fedora/fedora-$releasever-$basearch'
default['yum']['pgdg']['description'] = 'PostgreSQL 9.3'
default['yum']['pgdg']['enabled'] = true
default['yum']['pgdg']['gpgcheck'] = true
default['yum']['pgdg']['gpgkey'] = 'http://yum.postgresql.org/RPM-GPG-KEY-PGDG'
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'pgdg-9.3' do
    mirrorlist 'http://yum.pgrpms.org/9.3/fedora/fedora-$releasever-$basearch'
    description 'PostgreSQL 9.3'
    enabled true
    gpgcheck true
    gpgkey 'http://yum.postgresql.org/RPM-GPG-KEY-PGDG'
  end
```

Usage Example
-------------
To disable the pgdg repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :pgdg => {
      :enabled => {
        false
       }
     }
   }
 )
```

More Examples
-------------
Point the base and updates repositories at an internally hosted server.

```
node.default['yum']['pgdg']['enabled'] = true
node.default['yum']['pgdg']['mirrorlist'] = nil
node.default['yum']['pgdg']['baseurl'] = 'https://internal.example.com/pgdg/9.3/fedora-19-x86_64'
node.default['yum']['pgdg']['sslverify'] = false

include_recipe 'yum-pgdg'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@chef.io>)

```text
Copyright:: 2011-2015 Chef Software, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
