# oVirt Engine API Ruby SDK

## Introduction

This project contains the Ruby SDK for the oVirt Engine API.

## Important

Note that most of the code of this SDK is automatically generated. If you
just installed the gem then you will have everything already, but if you
downloaded the source then you will need to generate it, follow the
instructions in the `README.md` file of the parent directory.

## Usage

To use the SDK require the `ovirt/sdk/v4` file. That will give you
access to all the classes of th SDK, and in particular to the
Ovirt::SDK::V4::Connection class. This is the entry point of the SDK,
and gives you access to the root of the tree of services of the API:

```ruby
require 'ovirt/sdk/v4'

# Create a connection to the server:
connection = Ovirt::SDK::V4::Connection({
  :url => 'https://engine.example.com/ovirt-engine/api',
  :username => 'admin@internal',
  :password => '...',
  :ca_file => 'ca.pem',
})

# Get the reference to the system service:
system_service = connection.system

# Always remember to close the connection when finished:
connection.close
```

The `ca.pem` file is required when connecting to a server protected
with TLS. In an usual oVirt installation it will be in
`/etc/pki/ovirt-engine/ca.pem`.

Once you have the reference to the system service you can use it to
get references to other services, and call their methods. For example,
to retrieve the list of virtual machines of the system you can use the
`vms` method, which returns a reference to the service that manages
the virtual machines:

```ruby
# Get the reference to the "vms" service:
vms_service = system_service.vms
```

This service is an instance of Ovirt::SDK::V4::VmsService, and it has
a `list` method that returns an array of virtual machines, which are
instances of the Ovirt::SDK::V4::Vm class:

```ruby
# Retrieve the virtual machines:
vms = vms_service.list

# Print the names and identifiers of the virtual machines:
vms.each do |vm|
  puts "#{vm.name}: #{vm.id}"
end
```

In the future you will find more usuage examples in the `examples` directory.