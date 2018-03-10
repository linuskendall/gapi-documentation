# Cloud Machines

Use this section of the API to create, run, start, stop, reboot and change any available settings for your Cloud Machines (VMs).

## DescribeInstanceAttribute

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

i = ec2.get_instance_attribute('1111', 'instanceType')
```

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

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Attribute</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The attribute to describe. Can be instanceType, operatingSystem, hostname or you can fetch a graph using the following pattern: graph_(cpu|disk|network)_(hour|day|week|month|year), for example graph_cpu_month to get a monthly CPU graph.</td>
</tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The VM/instance ID to describe.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeInstanceStatus

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

i = ec2.get_all_instance_status(instance_ids=['1111'])
```

Describe the status for one or more instances.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>List of instances to describe. If omitted, describes all your instances/VMs.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeInstanceTypes

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

i = ec2.get_all_instance_types()
```

Describes one or more instance types.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceType</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>A list of instance types to describe. If omitted returns all instance types available.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_instances()
i = ec2.get_only_instances(['1111', '1112'])
```

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

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>List of instances to describe. If omitted, describes all your instances/VMs.</td>
</tr>
<tr>
<td>Filter</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5aa3cd24c6384').toggle();return false;">Members</a>)
<table id='Filter_5aa3cd24c6384' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Name</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Value</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td>Filters to apply</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeReservedInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_reserved_instances()
```

Describe reservation details for one or more instances.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ReservedInstancesId</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>List of instances to describe. If omitted, describes all your instances/VMs.</td>
</tr>
<tr>
<td>Filter</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5aa3cd24c63f4').toggle();return false;">Members</a>)
<table id='Filter_5aa3cd24c63f4' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Name</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Value</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td>Filters to apply</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeVmTypes

```python--boto2
# This is an API call not available in boto2.
```

Describes one or more instance types.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceType</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>A list of instance types to describe. If omitted returns all instance types available.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## GetPasswordData

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

password_data = ec2.get_password_data('1111')
```

Get encrypted administrator password for a Windows instance.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>List of instances to destroy.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## ModifyInstanceAttribute

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.modify_instance_attribute('1111', 'instanceType', 'cpu.lg')

ret = ec2.modify_instance_attribute('1111', 'password', 'this-is-ignored')

ret = ec2.modify_instance_attribute('1111', 'hostname', 'new-hostname')
```

Modifies one or more attributes of a given instance. Beware that some modifications are destructive.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Attribute</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The attribute to modify (optional: you can also just provide the modified instance value).</td>
</tr>
<tr>
<td>InstanceType_Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>New instance type. Beware that certain parameters cannot be downgraded such as disk. Also if you specify an instance type that is too small for the operating system used, this call will fail.</td>
</tr>
<tr>
<td>Password_Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>Provide any value in this field to re-generate a new random root password and set it on the instance.</td>
</tr>
<tr>
<td>OperatingSystem_Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>New operating system to use. Beware: This will fully reinstall the instance and will delete all data. Only supported within one family of OSes, for example Ubuntu to Ubuntu or Windows to Windows.</td>
</tr>
<tr>
<td>Hostname_Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>New hostname for the instance.</td>
</tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The ID of the instance to modify.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## RebootInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.reboot_instances(instance_ids=['1111'])
```

Reboot the provided list of instances.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to reboot.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## ResetInstanceAttribute

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.reset_instance_attribute('1111', 'operatingSystem')
```

Resets a given attribute on the instance to its current default value. Beware that some of these actions can be destructive.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Attribute</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>Name of the attribute to reset. Can be "instanceType", "operatingSystem", "networkConfig", "password" or "hostname". Beware: operatingSystem reset is destructive and will reinstall the OS.</td>
</tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The instance to reset the attribute for.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## RunInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

instance = ec2.run_instances('centos64_6.4', instance_type='bal.small')
```

Create one or more new instances with the given specifications.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ImageId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The operating system image to use for the instance.</td>
</tr>
<tr>
<td>InstanceType</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The instance type to use (cpu/memory specifiations). You can use the DescribeInstanceTypes to find available types. There are a number of instance types optimized for either memory, cpu or balanced types. Be aware that we do not necessarily offer the same types as AWS.</td>
</tr>
<tr>
<td>KeyName</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The SSH key name to use for the instance. Preview: This is currently only in preview mode and not fully supported.</td>
</tr>
<tr>
<td>NetworkInterface</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#NetworkInterface_5aa3cd24c6519').toggle();return false;">Members</a>)
<table id='NetworkInterface_5aa3cd24c6519' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>AssociatePublicIpAddress</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td>Used to specifiy the number of additional public IP addresses to associated with the instance. You can specify multiple NetworkInterfaces with AssociatePublicIpAddress set to true to generate multiple public IPs. If AssociatePublicIpAddress is set to false this will be ignored.</td>
</tr>
<tr>
<td>PrivateIpAddress</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>Provide any value here to allocate a private IP address to the instance.</td>
</tr>
<tr>
<td>Placement_AvailabilityZone</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td>ord1</td>
<td>The datacenter to locate the instance in.</td>
</tr>
<tr>
<td>MinCount</td>
<td><a href='#types'>int</a></td>
<td>N</td>
<td>1</td>
<td>Minimum number of instances to launch.</td>
</tr>
<tr>
<td>MaxCount</td>
<td><a href='#types'>int</a></td>
<td>N</td>
<td>1</td>
<td>Maximum number of instances to launch (ie. requested number).</td>
</tr>
<tr>
<td>BillingTerm</td>
<td><a href='#types'>int</a></td>
<td>N</td>
<td>1</td>
<td>The billing term to use in hours. Valid values are 1 (hourly), 730 (monthly) and 2190 (quarterly). Note: this is an extension to the AWS API and might not be supported by SDKs.</td>
</tr>
<tr>
<td>TagSpecification</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#TagSpecification_5aa3cd24c6584').toggle();return false;">Members</a>)
<table id='TagSpecification_5aa3cd24c6584' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ResourceType</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The type of resource to tag</td>
</tr>
<tr>
<td>Tags</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tags_5aa3cd24c65f4').toggle();return false;">Members</a>)
<table id='Tags_5aa3cd24c65f4' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Key</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td>Set of tags to apply to the newly created instance</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## StartInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

instance = ec2.start_instances(instance_ids=['1111'])
```

Start the provided list of instances. They need to be in "stop" or "pause" state to be started.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to start.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## StopInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

instance = ec2.stop_instances(instance_ids=['1111'])
```

Stop the provided list of instances. They need to be in "started" state to be stopped.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to stop.</td>
</tr>
<tr>
<td>Force</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## TerminateInstances

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

instance = ec2.terminate_instnaces(instance_ids=['1111'])
```

Destroy the provided list of instances. Warning: This will delete all data from the instances.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to destroy.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
# Networking

Use this section of the API to manage elastic and additional IP addresses. Elastic IP addresses can be associated and de-associated with VMs without removing them, while additional IP addresses are always directly bound to a VM.

## AllocateAddress

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ip = ec2.allocate_address(domain='ord1')
```

Allocates an elastic IP address to your account. The elastic IP will be availablein a VLAN that will be created in the provided availability zone.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Domain</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The availability zone/data center to which to allocate the address.The address will be available for routing within that data center</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## AssignPublicIpAddress

```python--boto2
# Not supported by the boto2 SDK
```

Assigns a new public/additional IP address to the Instance provided. This is an extension of the AWS API so likely not supported by AWS SDKs or tools.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The VM/instance to assign the public IP address to.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## AssociateAddress

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ip = ec2.allocate_address(domain='ord1')

ret = ec2.associate_address(instance_id='1111', public_ip=ip.public_ip)
```

Creates an association between a given cloud machine instance and an elastic IP. Ensures that the Cloud Machine is added to the VLAN the IP is associated to.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>InstanceId</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The instance/cloud machine to which to associate the address.</td>
</tr>
<tr>
<td>PublicIp</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The public IP to associate with the given instance</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeAddresses

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_addresses()

address = ec2.get_all_addresses(['32.44.22.11'])
```

Describes one or more addresses.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>PublicIp</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>A list of public IPs to describe. If not provided all address will be described.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DisassociateAddress

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.disassociate_address(public_ip='32.44.22.11')
```

Disassociates an address from the VM it is associated with. this does not release the elastic IP.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>PublicIp</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The public IP to disassociate from a given VM.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## ReleaseAddress

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.release_address(public_ip='32.44.22.11')
```

Releases an elastic IP address, removing it from your account.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>PublicIp</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The elastic IP to free/release.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## UnassignPublicIpAddress

```python--boto2
# Not supported by the boto2 SDK
```

Removes and releases a public/additional IP address. This is an extension of the AWS API so likely not supported by AWS SDKs or tools.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>PublicIp</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td>The public IP to remove from the VM it is assigned to.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
# Images & Regions

Use this section of the API to retrieve information about the available operating system images as well as our data centers.

## DescribeImageAttribute

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.get_image_attribute(image_id='ubuntu64_14.04.1', 
	attribute='description')
```

Describes attributes of an operating system image.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Attribute</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
<tr>
<td>ImageId</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeImages

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_images()

image = ec2.get_image('ubuntu64_14.04.1')



```

Describes available operating system images.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ImageId</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>The operating system image to describe. If none is provided, describe all images.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeAvailabilityZones

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_zones()

zone = ec2.get_all_zones(zones=['ord1'])

```

Describes one, several or all of the data centers returning information about its current status and whether you can launch new cloud machines in them.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ZoneName</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>The name of the datacenter to describe. If not supplied - describe all data centers.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
### Return Value

<table><tr><th>Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>availabilityZoneInfoSet</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#availabilityZoneInfoSet_5aa3cd24c6838').toggle();return false;">Members</a>)
<table id='availabilityZoneInfoSet_5aa3cd24c6838' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>regionName</td>
<td><a href='#types'>string</a></td><td>
The name of the region/data center (at this time identical to zoneName).</td>
</tr>
<tr>
<td>zoneName</td>
<td><a href='#types'>string</a></td><td>
The name of the zone/data center (at this time identical to regionName).</td>
</tr>
<tr>
<td>zoneState</td>
<td><a href='#types'>string</a></td><td>
"Active" if currently accepting requests for new Cloud Machines, otherwise "Inactive".</td>
</tr>
<tr>
<td>messageSet</td>
<td><a href='#types'>array</a></td><td>
Array with one member "message" providing any messages or updates about the data center.</td>
</tr>
</table>
</td><td>
A set of information related to the queried data centers.</td>
</tr>
</table>
## DescribeRegions

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_regions()

zone = ec2.get_all_regions(zones=['ord1'])
```

Describes the API end points available in different data centers/regions.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>RegionName</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>The name of the datacenter to describe. If not supplied - describe all data centers.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
### Return Value

<table><tr><th>Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>regionInfoSet</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#regionInfoSet_5aa3cd24c68d5').toggle();return false;">Members</a>)
<table id='regionInfoSet_5aa3cd24c68d5' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>regionEndpoint</td>
<td><a href='#types'>string</a></td><td>
The API endpoint that can be used for the region/data center.</td>
</tr>
<tr>
<td>regionName</td>
<td><a href='#types'>string</a></td><td>
The name of the region/data center.</td>
</tr>
</table>
</td><td>
A set describing the queried regions/API endpoints.</td>
</tr>
</table>
# SSH Keys

Use this section of the API to add, describe and delete SSH Keys to your account. This is currently a preview feature and is not yet supported when creating new Cloud Machines.

## CreateKeyPair

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

keypair = ec2.create_key_pair('ssh-key-name')
```

Generates a new keypair returning the private key. Only do this over a secure HTTPS connection as the private key returned must be kept secret.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>KeyName</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>What to name the key pair generated.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DeleteKeyPair

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

keypair = ec2.delete_key_pair('ssh-key-name')
```

Deletes a key from your account.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>KeyName</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The name of the key to delete.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeKeyPairs

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

all = ec2.get_all_key_pairs()

keypair = ec2.get_all_key_pairs(['ssh-key-name'])
```

Describes one or more of the keys that have been added to your account.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>KeyName</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td>The keys to describe. If omitted all keys will be returned.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## ImportKeyPair

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

keypair = ec2.import_key_pair('ssh-key-name',
		'ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA27Qd8PiFw+FYhPOJgDp9lo9bUP6NJEGtjyAK+o+oyd8HKEqORSVzM9vG81mHkapkr3VCBkZKgF6GF8Lfc2cUlC9g4XYJErjBeWmuWYo8Fq1ch1QTQUDkJfRaI1lNSuzS/8KvKVi4yO4ydOoCM7rG5yFiwtrPcxy8CeuwkA6DpyHtoIspOpzD5C6kcTyhf3PdPk/qMTB1h9oa0gpqmh8ns1yYI3Lxud8AYf63Awm9/V1WxwCMxHailKbE0glgw95PTJGUL6FVyc+awXg3xn48TjNT9dR82Dr4OPUgZq7fZHArcSyavoWzvjeQqcCN5qkcCAUZ1ZpSgWj/FOZIENlMDw== test@thegcloud.com')
```

Imports a public key which you have generated separately.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>KeyName</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>What to name the imported public key.</td>
</tr>
<tr>
<td>PublicKeyMaterial</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td>The public key to import.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
# Tags

Use this section of the API create, delete and describe tags used for Cloud Machines.

## CreateTags

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.create_tags(['1111'], { 'MyTag': 'value-is-ignored' })
```

Adds or Overwrites one or more tags for a CloudMachine resource.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ResourceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to tag.</td>
</tr>
<tr>
<td>Tag</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tag_5aa3cd24c6a25').toggle();return false;">Members</a>)
<table id='Tag_5aa3cd24c6a25' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Value</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Key</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>Y</td>
<td></td>
<td>One or more tags.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DeleteTags

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

ret = ec2.delete_tags(['1111'], { 'MyTag': 'value-is-ignored' })
```

Deletes specified tags from resources.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>ResourceId</td>
<td><a href='#types'>stringlist</a></td>
<td>Y</td>
<td></td>
<td>List of instances to delete tags from.</td>
</tr>
<tr>
<td>Tag</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tag_5aa3cd24c6abc').toggle();return false;">Members</a>)
<table id='Tag_5aa3cd24c6abc' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Key</td>
<td><a href='#types'>string</a></td>
<td>Y</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Value</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td>One or more tags.</td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
## DescribeTags

```python--boto2
import boto

ec2 = boto.connect_ec2_endpoint(
    'https://api.thegcloud.com', 
    'APIKEY', 
    'APIHASH')

tags = ec2.get_all_tags({"resource-id": ['1111']})
```

Describes one or more of tags assigned to CloudMachine.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Filter</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5aa3cd24c6b50').toggle();return false;">Members</a>)
<table id='Filter_5aa3cd24c6b50' style='display:none'>
<tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Name</td>
<td><a href='#types'>string</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>Value</td>
<td><a href='#types'>stringlist</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>
</td>
<td>N</td>
<td></td>
<td></td>
</tr>
<tr>
<td>DryRun</td>
<td><a href='#types'>boolean</a></td>
<td>N</td>
<td></td>
<td></td>
</tr>
</table>

