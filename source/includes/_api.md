
# Cloud Machines

Use this section of the API to create, run, start, stop, reboot and change any available settings for your Cloud Machines (VMs).

## DescribeInstanceAttribute

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_instance_attribute({ instance_id: '1111', attribute: 'instanceType' })
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeInstanceAttribute', '&InstanceId=2632&Attribute=instanceType');
```

> Sample DescribeInstanceAttribute XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeInstanceAttributeResponse>
  <instanceId>1111</instanceId>
  <instanceType>
    <value>custom_bal_1vcpu_384m_10gb</value>
  </instanceType>
  <RequestID>21cd8ec650fdfc7819465beae5bc48c8</RequestID>
</DescribeInstanceAttributeResponse>
```

Fetches a single property for an instance.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Attribute | [string](#parameter-types) | Y |  | The attribute to describe. Can be instanceType, operatingSystem, hostname or you can fetch a graph using the following pattern: graph_(cpu|disk|network)_(hour|day|week|month|year), for example graph_cpu_month to get a monthly CPU graph.
InstanceId | [string](#parameter-types) | Y |  | The VM/instance ID to describe.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeInstanceStatus

Describe the status for one or more instances.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | N |  | List of instances to describe. If omitted, describes all your instances/VMs.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeInstanceTypes

Describes one or more instance types.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceType | [stringlist](#parameter-types) | N |  | A list of instance types to describe. If omitted returns all instance types available.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeInstances

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_instances({ instance_ids: ['1111'] })
```

Describe the full properties for one or more instances.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | N |  | List of instances to describe. If omitted, describes all your instances/VMs.
Filter | [array](#parameter-types) | N |  | Filters to apply
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeReservedInstances

Describe reservation details for one or more instances.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ReservedInstancesId | [stringlist](#parameter-types) | N |  | List of instances to describe. If omitted, describes all your instances/VMs.
Filter | [array](#parameter-types) | N |  | Filters to apply
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeVmTypes

Describes one or more instance types.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceType | [stringlist](#parameter-types) | N |  | A list of instance types to describe. If omitted returns all instance types available.
DryRun | [boolean](#parameter-types) | N |  | 

## GetPasswordData

Get encrypted administrator password for a Windows instance.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [string](#parameter-types) | Y |  | List of instances to destroy.
DryRun | [boolean](#parameter-types) | N |  | 

## ModifyInstanceAttribute

Modifies one or more attributes of a given instance. Beware that some modifications are destructive.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Attribute | [string](#parameter-types) | N |  | The attribute to modify (optional: you can also just provide the modified instance value).
InstanceType_Value | [string](#parameter-types) | N |  | New instance type. Beware that certain parameters cannot be downgraded such as disk. Also if you specify an instance type that is too small for the operating system used, this call will fail.
Password_Value | [string](#parameter-types) | N |  | Provide any value in this field to re-generate a new random root password and set it on the instance.
OperatingSystem_Value | [string](#parameter-types) | N |  | New operating system to use. Beware: This will fully reinstall the instance and will delete all data. Only supported within one family of OSes, for example Ubuntu to Ubuntu or Windows to Windows.
Hostname_Value | [string](#parameter-types) | N |  | New hostname for the instance.
InstanceId | [string](#parameter-types) | Y |  | The ID of the instance to modify.
DryRun | [boolean](#parameter-types) | N |  | 

## RebootInstances

Reboot the provided list of instances.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | Y |  | List of instances to reboot.
DryRun | [boolean](#parameter-types) | N |  | 

## ResetInstanceAttribute

Resets a given attribute on the instance to its current default value. Beware that some of these actions can be destructive.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Attribute | [string](#parameter-types) | Y |  | Name of the attribute to reset. Can be "instanceType", "operatingSystem", "networkConfig", "password" or "hostname". Beware: operatingSystem reset is destructive and will reinstall the OS.
InstanceId | [string](#parameter-types) | Y |  | The instance to reset the attribute for.
DryRun | [boolean](#parameter-types) | N |  | 

## RunInstances

Create one or more new instances with the given specifications.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ImageId | [string](#parameter-types) | Y |  | The operating system image to use for the instance.
InstanceType | [string](#parameter-types) | Y |  | The instance type to use (cpu/memory specifiations). You can use the DescribeInstanceTypes to find available types. There are a number of instance types optimized for either memory, cpu or balanced types. Be aware that we do not necessarily offer the same types as AWS.
KeyName | [string](#parameter-types) | N |  | The SSH key name to use for the instance. Preview: This is currently only in preview mode and not fully supported.
NetworkInterface | [array](#parameter-types) | N |  | Used to specifiy the number of additional public IP addresses to associated with the instance. You can specify multiple NetworkInterfaces with AssociatePublicIpAddress set to true to generate multiple public IPs. If AssociatePublicIpAddress is set to false this will be ignored.
PrivateIpAddress | [string](#parameter-types) | N |  | Provide any value here to allocate a private IP address to the instance.
Placement_AvailabilityZone | [string](#parameter-types) | N | ord1 | The datacenter to locate the instance in.
MinCount | [int](#parameter-types) | N | 1 | Minimum number of instances to launch.
MaxCount | [int](#parameter-types) | N | 1 | Maximum number of instances to launch (ie. requested number).
BillingTerm | [int](#parameter-types) | N | 1 | The billing term to use in hours. Valid values are 1 (hourly), 730 (monthly) and 2190 (quarterly). Note: this is an extension to the AWS API and might not be supported by SDKs.
TagSpecification | [array](#parameter-types) | N |  | Set of tags to apply to the newly created instance
DryRun | [boolean](#parameter-types) | N |  | 

## StartInstances

Start the provided list of instances. They need to be in "stop" or "pause" state to be started.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | Y |  | List of instances to start.
DryRun | [boolean](#parameter-types) | N |  | 

## StopInstances

Stop the provided list of instances. They need to be in "started" state to be stopped.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | Y |  | List of instances to stop.
Force | [boolean](#parameter-types) | N |  | 
DryRun | [boolean](#parameter-types) | N |  | 

## TerminateInstances

Destroy the provided list of instances. Warning: This will delete all data from the instances.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [stringlist](#parameter-types) | Y |  | List of instances to destroy.
DryRun | [boolean](#parameter-types) | N |  | 

# Networking

Use this section of the API to manage elastic and additional IP addresses. Elastic IP addresses can be associated and de-associated with VMs without removing them, while additional IP addresses are always directly bound to a VM.

## AllocateAddress

Allocates an elastic IP address to your account. The elastic IP will be availablein a VLAN that will be created in the provided availability zone.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Domain | [string](#parameter-types) | N |  | The availability zone/data center to which to allocate the address.The address will be available for routing within that data center
DryRun | [boolean](#parameter-types) | N |  | 

## AssignPublicIpAddress

Assigns a new public/additional IP address to the Instance provided. This is an extension of the AWS API so likely not supported by AWS SDKs or tools.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [string](#parameter-types) | N |  | The VM/instance to assign the public IP address to.
DryRun | [boolean](#parameter-types) | N |  | 

## AssociateAddress

Creates an association between a given cloud machine instance and an elastic IP. Ensures that the Cloud Machine is added to the VLAN the IP is associated to.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
InstanceId | [string](#parameter-types) | N |  | The instance/cloud machine to which to associate the address.
PublicIp | [string](#parameter-types) | N |  | The public IP to associate with the given instance
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeAddresses

Describes one or more addresses.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
PublicIp | [stringlist](#parameter-types) | N |  | A list of public IPs to describe. If not provided all address will be described.
DryRun | [boolean](#parameter-types) | N |  | 

## DisassociateAddress

Disassociates an address from the VM it is associated with. this does not release the elastic IP.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
PublicIp | [string](#parameter-types) | N |  | The public IP to disassociate from a given VM.
DryRun | [boolean](#parameter-types) | N |  | 

## ReleaseAddress

Releases an elastic IP address, removing it from your account.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
PublicIp | [string](#parameter-types) | N |  | The elastic IP to free/release.
DryRun | [boolean](#parameter-types) | N |  | 

## UnassignPublicIpAddress

Removes and releases a public/additional IP address. This is an extension of the AWS API so likely not supported by AWS SDKs or tools.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
PublicIp | [string](#parameter-types) | N |  | The public IP to remove from the VM it is assigned to.
DryRun | [boolean](#parameter-types) | N |  | 

# Images & Regions

Use this section of the API to retrieve information about the available operating system images as well as our data centers.

## DescribeImageAttribute

Describes attributes of an operating system image.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Attribute | [string](#parameter-types) | Y |  | 
ImageId | [string](#parameter-types) | Y |  | 
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeImages

Describes available operating system images.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ImageId | [stringlist](#parameter-types) | N |  | The operating system image to describe. If none is provided, describe all images.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeAvailabilityZones

Describes one, several or all of the data centers returning information about its current status and whether you can launch new cloud machines in them.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ZoneName | [stringlist](#parameter-types) | N |  | The name of the datacenter to describe. If not supplied - describe all data centers.
DryRun | [boolean](#parameter-types) | N |  | 

### Return Value

Name | Type | Required? | Default | Description
## DescribeRegions

Describes the API end points available in different data centers/regions.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
RegionName | [stringlist](#parameter-types) | N |  | The name of the datacenter to describe. If not supplied - describe all data centers.
DryRun | [boolean](#parameter-types) | N |  | 

### Return Value

Name | Type | Required? | Default | Description
# SSH Keys

Use this section of the API to add, describe and delete SSH Keys to your account. This is currently a preview feature and is not yet supported when creating new Cloud Machines.

## CreateKeyPair

Generates a new keypair returning the private key. Only do this over a secure HTTPS connection as the private key returned must be kept secret.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
KeyName | [string](#parameter-types) | Y |  | What to name the key pair generated.
DryRun | [boolean](#parameter-types) | N |  | 

## DeleteKeyPair

Deletes a key from your account.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
KeyName | [string](#parameter-types) | Y |  | The name of the key to delete.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeKeyPairs

Describes one or more of the keys that have been added to your account.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
KeyName | [stringlist](#parameter-types) | N |  | The keys to describe. If omitted all keys will be returned.
DryRun | [boolean](#parameter-types) | N |  | 

## ImportKeyPair

Imports a public key which you have generated separately.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
KeyName | [string](#parameter-types) | Y |  | What to name the imported public key.
PublicKeyMaterial | [string](#parameter-types) | Y |  | The public key to import.
DryRun | [boolean](#parameter-types) | N |  | 

# Tags

Use this section of the API create, delete and describe tags used for Cloud Machines.

## CreateTags

Adds or Overwrites one or more tags for a CloudMachine resource.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ResourceId | [stringlist](#parameter-types) | Y |  | List of instances to tag.
Tag | [array](#parameter-types) | Y |  | One or more tags.
DryRun | [boolean](#parameter-types) | N |  | 

## DeleteTags

Deletes specified tags from resources.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
ResourceId | [stringlist](#parameter-types) | Y |  | List of instances to delete tags from.
Tag | [array](#parameter-types) | N |  | One or more tags.
DryRun | [boolean](#parameter-types) | N |  | 

## DescribeTags

Describes one or more of tags assigned to CloudMachine.

### Parameters

Name | Type | Required? | Default | Description
---- | ---- | --------- | ------- | -----------
Filter | [array](#parameter-types) | N |  | 
DryRun | [boolean](#parameter-types) | N |  | 


