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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_instance_attribute(InstanceId='1111', Attribute='instanceType')
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

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeInstanceAttribute(array('InstanceId' => '1111', 'Attribute' => 'instanceType'));
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_instance_status(InstanceIds=['1111'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_instance_status({ instance_ids: ['1111'] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeInstanceStatus(array(
		'InstanceIds' => array('2632')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeInstanceStatus', 'InstanceId.1=1111');

```

> Sample DescribeInstanceStatus XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeInstanceStatusResponse>
  <instanceStatusSet>
    <item>
      <instanceId>2632</instanceId>
      <availabilityZone>ord1</availabilityZone>
      <instanceState>
        <code>0</code>
        <name>on</name>
      </instanceState>
      <systemStatus>
        <item>
          <status>ok</status>
          <details>
            <item>
              <name>reachability</name>
              <status>passed</status>
            </item>
          </details>
        </item>
      </systemStatus>
      <instanceStatus>
        <item>
          <status>ok</status>
          <details>
            <item>
              <name>reachability</name>
              <status>passed</status>
            </item>
          </details>
        </item>
      </instanceStatus>
      <eventsSet>
        <item>
          <code>instance-modify</code>
          <description>modify</description>
          <notAfter>2018-03-22T18:39:33+00:00</notAfter>
          <notBefore>2018-03-22T18:39:33+00:00</notBefore>
        </item>
      </eventsSet>
    </item>
  </instanceStatusSet>
  <RequestID>251415cd11fc9a2b5398af5d100cd049</RequestID>
</DescribeInstanceStatusResponse>
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

```python--boto3
# Not supported by this SDK
```

```ruby
# Not supported by this SDK
```

```php
# Not supported by this SDK
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeInstanceTypes', '');
```

> Sample DescribeInstanceTypes XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeInstanceTypesResponse>
  <instanceTypeSet>
    <item>
      <name>bal.lg</name>
      <cores>1</cores>
      <memory>2048</memory>
      <disk>40</disk>
    </item>
    <item>
      <name>bal.lg2</name>
      <cores>2</cores>
      <memory>4096</memory>
      <disk>40</disk>
    </item>
    <item>
      <name>bal.small</name>
      <cores>1</cores>
      <memory>512</memory>
      <disk>10</disk>
    </item>
    <item>
      <name>bal.xlg</name>
      <cores>2</cores>
      <memory>4096</memory>
      <disk>60</disk>
    </item>
    <item>
      <name>bal.xxlg</name>
      <cores>4</cores>
      <memory>8192</memory>
      <disk>80</disk>
    </item>
    <item>
      <name>client_1544-bal.small</name>
      <cores>1</cores>
      <memory>512</memory>
      <disk>10</disk>
    </item>
    <item>
      <name>cpu.lg</name>
      <cores>4</cores>
      <memory>3200</memory>
      <disk>60</disk>
    </item>
    <item>
      <name>cpu.med</name>
      <cores>3</cores>
      <memory>2176</memory>
      <disk>40</disk>
    </item>
    <item>
      <name>cpu.xxlg</name>
      <cores>8</cores>
      <memory>8192</memory>
      <disk>80</disk>
    </item>
    <item>
      <name>mem.lg</name>
      <cores>6</cores>
      <memory>11008</memory>
      <disk>80</disk>
    </item>
    <item>
      <name>mem.med</name>
      <cores>5</cores>
      <memory>10240</memory>
      <disk>60</disk>
    </item>
    <item>
      <name>mem.small</name>
      <cores>4</cores>
      <memory>8192</memory>
      <disk>30</disk>
    </item>
    <item>
      <name>mem.xlg</name>
      <cores>7</cores>
      <memory>14080</memory>
      <disk>80</disk>
    </item>
    <item>
      <name>mem.xxlg</name>
      <cores>8</cores>
      <memory>16384</memory>
      <disk>80</disk>
    </item>
    <item>
      <name>new.small</name>
      <cores>1</cores>
      <memory>512</memory>
      <disk>10</disk>
    </item>
    <item>
      <name>promo.bal.small</name>
      <cores>1</cores>
      <memory>1024</memory>
      <disk>30</disk>
    </item>
  </instanceTypeSet>
  <RequestID>c0d9f0db011b9019bac47898096a7735</RequestID>
</DescribeInstanceTypesResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

# Get all instances
resp = ec2.describe_instances()

# Describe single instance
resp = ec2.describe_instances(InstanceIds=['2632'])


```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
# Get all instances 
i = ec2.describe_instances()

# Describe a single instance
i = ec2.describe_instances({ instance_ids: ['1111'] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

// Describe all instances 
$ret = $ec2Client->describeInstances();

// Describe one instance
$ret = $ec2Client->describeInstances(array(
		'InstanceIds' => array('1111')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'

// Get all instances
print apiRequest('DescribeInstances');

// Get specific instance
print apiRequest('DescribeInstances', 'InstanceId.1=2632');
```

> Sample DescribeInstances XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeInstancesResponse>
  <reservationSet>
    <item>
      <ownerId>1479</ownerId>
      <instancesSet>
        <item>
          <imageId>centos64_6.4</imageId>
          <instanceId>2632</instanceId>
          <instanceType>custom_cpu_4vcpu_3200m_60gb</instanceType>
          <placement>
            <availabilityZone>ord1</availabilityZone>
          </placement>
          <launchTime>2018-03-20T18:17:59+00:00</launchTime>
          <privateDnsName>840bde.linus.kendal</privateDnsName>
          <privateIpAddress>10.60.235.153</privateIpAddress>
          <publicIpAddress>69.39.235.150</publicIpAddress>
          <state>
            <code>0</code>
            <name>on</name>
          </state>
          <subnetId>148</subnetId>
          <architecture>x86_64</architecture>
          <virtualizationType>hvm</virtualizationType>
          <rootDeviceName>/dev/sda1</rootDeviceName>
          <hypervisor>xenserver</hypervisor>
          <platform>Centos</platform>
          <tagSet>
            <item>
              <key>testtag</key>
            </item>
            <item>
              <key>rextag</key>
            </item>
            <item>
              <key>rex_t-a:g</key>
            </item>
            <item>
              <key>test</key>
            </item>
          </tagSet>
        </item>
      </instancesSet>
    </item>
  </reservationSet>
  <RequestID>b7de420a019667e5cec50028864aa459</RequestID>
</DescribeInstancesResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5af9b3d83cb8c').toggle();return false;">Members</a>)
<table id='Filter_5af9b3d83cb8c' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_reserved_instances()
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
 
i = ec2.describe_reserved_instances({})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeReservedInstances();
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeReservedInstances', '');
```

> Sample DescribeReservedInstances XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeReservedInstancesResponse>
  <reservedInstancesSet>
    <item>
      <reservedInstancesId>2759</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_2048m_40gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.08928571428571428</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-03-21T12:28:24+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2669</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_512m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.02896461038889516</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-03-20T18:17:58+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2668</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_512m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.02896461038889516</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-03-20T18:17:45+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2632</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_384m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.01553986438648480</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-03-20T18:17:59+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2627</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_512m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.00684900000000000</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-01-17T22:30:37+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2621</reservedInstancesId>
      <instanceType>custom_cpu_2vcpu_2048m_45gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.05988775565242224</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-01-16T18:48:40+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2620</reservedInstancesId>
      <instanceType>custom_cpu_2vcpu_512m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.02455757339034518</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-01-16T18:48:40+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges>
        <item>
          <amount>0.00138888889000000</amount>
          <frequency>Hourly</frequency>
          <desc>1 Additional IPs</desc>
        </item>
      </recurringCharges>
    </item>
    <item>
      <reservedInstancesId>2600</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_2048m_40gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.08669750343712217</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2018-01-15T20:33:52+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2599</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_2048m_40gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.01835599000000000</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>1970-01-01T00:00:00+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2587</reservedInstancesId>
      <instanceType>custom_mem_6vcpu_11008m_80gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.37845361580000000</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2017-11-01T13:10:48+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2583</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_384m_4gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.02339383963648480</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2017-11-01T12:46:54+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2525</reservedInstancesId>
      <instanceType>custom_bal_2vcpu_2304m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.10171102509280179</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2016-09-09T14:51:47+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2524</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_2048m_25gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.08669750343712217</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2016-09-09T14:30:44+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2522</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_1024m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.04862036677268064</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2016-07-29T19:37:28+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2513</reservedInstancesId>
      <instanceType>custom_cpu_6vcpu_6000m_10gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.25998123120000000</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2016-07-08T16:40:30+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges/>
    </item>
    <item>
      <reservedInstancesId>2432</reservedInstancesId>
      <instanceType>custom_bal_1vcpu_512m_20gb</instanceType>
      <availabilityZone>ord1</availabilityZone>
      <usagePrice>0.03094783505594508</usagePrice>
      <instanceCount>1</instanceCount>
      <productDescription>Linux/UNIX</productDescription>
      <start>2015-10-29T23:04:27+00:00</start>
      <state>on</state>
      <instanceTenancy>default</instanceTenancy>
      <currencyCode>USD</currencyCode>
      <offeringType>Medium Utilization</offeringType>
      <recurringCharges>
        <item>
          <amount>0.50000000000000000</amount>
          <frequency>Hourly</frequency>
          <desc>VM#2432 - VM Snapshots</desc>
        </item>
      </recurringCharges>
    </item>
  </reservedInstancesSet>
  <RequestID>fbb8dafa86e7ba6204236e8a95a52d95</RequestID>
</DescribeReservedInstancesResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5af9b3d83cc38').toggle();return false;">Members</a>)
<table id='Filter_5af9b3d83cc38' style='display:none'>
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

```python--boto3
# Not supported by this SDK
```

```ruby
# Not supported by this SDK
```

```php
# Not supported by this SDK
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeVmTypes');
```

> Sample DescribeVmTypes XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeVmTypesResponse xmlns="http://ec2.amazonaws.com/doc/2016-11-15/">
    <instanceTypeSet>
        <item>
            <name>gcl.1</name>
            <cores>1</cores>
            <memory>1024</memory>
            <disk>30</disk>
        </item>
        <item>
            <name>gcl.2</name>
            <cores>1</cores>
            <memory>2048</memory>
            <disk>60</disk>
        </item>
        <item>
            <name>gcl.4</name>
            <cores>2</cores>
            <memory>4096</memory>
            <disk>90</disk>
        </item>
        <item>
            <name>gcl.8</name>
            <cores>4</cores>
            <memory>8192</memory>
            <disk>120</disk>
        </item>
        <item>
            <name>gcl.core.2</name>
            <cores>2</cores>
            <memory>2048</memory>
            <disk>60</disk>
        </item>
        <item>
            <name>gcl.core.4</name>
            <cores>4</cores>
            <memory>4096</memory>
            <disk>90</disk>
        </item>
        <item>
            <name>gcl.core.8</name>
            <cores>8</cores>
            <memory>8192</memory>
            <disk>180</disk>
        </item>
        <item>
            <name>gcl.max.8</name>
            <cores>2</cores>
            <memory>8192</memory>
            <disk>180</disk>
        </item>
        <item>
            <name>gcl.max.16</name>
            <cores>4</cores>
            <memory>16384</memory>
            <disk>360</disk>
        </item>
    </instanceTypeSet>
    <RequestID>d4e0b3938bac43f61dd933567c1416dd</RequestID>
</DescribeVmTypesResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.get_password_data(InstanceId='1111')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
 
i = ec2.get_password_data({instance_id: "1111"})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->getPasswordData(array(
		'InstanceId' => '1111'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('GetPasswordData', '2632');
```

> Sample GetPasswordData XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<GetPasswordDataResponse>
  <instanceId>1111</instanceId>
  <passwordData>password</passwordData>
  <RequestID>623e7465548c231e1634e824ba6fe549</RequestID>
</GetPasswordDataResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.modify_instance_attribute(
	InstanceId='1111', 
	Attribute='instanceType',
	InstanceType='cpu.lg')

resp = ec2.modify_instance_attribute(
	InstanceId='1111', 
	Attribute='password',
	Value='ignored')

resp = ec2.modify_instance_attribute(
	InstanceId='1111', 
	Attribute='hostname',
	Value='new-hostname')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.modify_instance_attribute({
    attribute: "instanceType",
    instance_id: "1111",
    instance_type: "cpu.lg"})

i = ec2.modify_instance_attribute({
    attribute: "password",
    instance_id: "1111",
    value: "ignored"})

i = ec2.modify_instance_attribute({
    attribute: "hostname",
    instance_id: "1111",
    value: "new-hostname"})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->modifyInstanceAttribute(array(
		'InstanceId' => '1111',
		'Attribute' => 'instanceType',
		'InstanceType' => array('Value' => 'cpu.lg')));

$ret = $ec2Client->modifyInstanceAttribute(array(
		'InstanceId' => '1111',
		'Attribute' => 'password',
		'Value' => 'ignored'));

$ret = $ec2Client->modifyInstanceAttribute(array(
		'InstanceId' => '1111',
		'Attribute' => 'hostname',
		'Value' => 'new-hostname'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('ModifyInstanceAttribute', 'InstanceId=2632&Attribute=instanceType&InstanceType.Value=cpu.lg');
```

> Sample ModifyInstanceAttribute XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ModifyInstanceAttributeResponse>
  <return>true</return>
  <RequestID>957fd7ed4e49fea8376ba2a0b571fe36</RequestID>
</ModifyInstanceAttributeResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.reboot_instances(InstanceIds=['1111'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.reboot_instances({ instance_ids: ["1111"] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->rebootInstances(array('InstanceIds' => array('1111')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('RebootInstances', 'InstanceId.1=2632');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.reset_instance_attribute(
	InstanceId='1111', 
	Attribute='operatingSystem')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.reset_instance_attribute({
    attribute: "operatingSystem",
    instance_id: "1111"})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->resetInstanceAttribute(array(
		'InstanceId' => '1111',
		'Attribute' => 'operatingSystem'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('ResetInstanceAttribute', 'InstanceId=2632&Attribute=operatingSystempassword');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.run_instances(
	ImageId="centos64_6.4",
	InstanceType="bal.small",
	MinCount=1,
	MaxCount=1)
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.run_instances({ image_id: "centos64_6.4", instance_type: "bal.small" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->runInstances(array(
		'ImageId' => 'centos64_6.4',
		'InstanceType' => 'bal.small',
		'MinCount' => 1,
		'MaxCount' => 1));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('RunInstances', 'ImageId=centos64_6.4&InstanceType=bal.small');
```

> Sample RunInstances XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunInstancesResponse>
  <reservationId>0</reservationId>
  <ownerId>4444</ownerId>
  <instancesSet>
    <item>
      <imageId>centos64_6.4</imageId>
      <instanceId>2760</instanceId>
      <instanceType>custom_bal_1vcpu_512m_10gb</instanceType>
      <placement>
        <availabilityZone>ord1</availabilityZone>
      </placement>
      <launchTime>1970-01-01T00:00:00+00:00</launchTime>
      <privateDnsName>ord1-9cf49e</privateDnsName>
      <privateIpAddress>none</privateIpAddress>
      <publicIpAddress>69.39.235.179</publicIpAddress>
      <state>
        <code>4</code>
        <name>unknown</name>
      </state>
      <architecture>x86_64</architecture>
      <virtualizationType>hvm</virtualizationType>
      <rootDeviceName>/dev/sda1</rootDeviceName>
      <hypervisor>xenserver</hypervisor>
      <platform>Centos</platform>
      <tagSet/>
    </item>
  </instancesSet>
  <RequestID>7809f80abbd92cda0dbfa22e0daf1862</RequestID>
</RunInstancesResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#NetworkInterface_5af9b3d83cec2').toggle();return false;">Members</a>)
<table id='NetworkInterface_5af9b3d83cec2' style='display:none'>
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
<td>730</td>
<td>The billing term to use in hours. Valid values are 1 (hourly), 730 (monthly) and 2190 (quarterly). Note: this is an extension to the AWS API and might not be supported by SDKs.</td>
</tr>
<tr>
<td>TagSpecification</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#TagSpecification_5af9b3d83cf0e').toggle();return false;">Members</a>)
<table id='TagSpecification_5af9b3d83cf0e' style='display:none'>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tags_5af9b3d83cf52').toggle();return false;">Members</a>)
<table id='Tags_5af9b3d83cf52' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.start_instances(InstanceIds=['1111'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.start_instances({ instance_ids: ["1111"] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->startInstances(array('InstanceIds' => array('1111')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('StartInstances', 'InstanceId.1=2632');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.stop_instances(InstanceIds=['1111'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.stop_instances({ instance_ids: ["1111"] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->stopInstances(array('InstanceIds' => array('1111')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('StopInstances', 'InstanceId.1=2632');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.terminate_instances(InstanceIds=['1111'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.terminate_instances({ instance_ids: ["1111"] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->terminateInstances(array('InstanceIds' => array('1111')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('TerminateInstances', 'InstanceId.1=2632');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.allocate_address(Domain='ord1')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.allocate_address({ domain: "ord1" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->allocateAddress(array('Domain' => 'ord1'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('AllocateAddress', 'Domain=ord1');
```

> Sample AllocateAddress XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<AllocateAddressResponse>
	<publicIp>69.39.235.241</publicIp>
	<domain>ord1</domain>
	<RequestID>4882d9fd45cd1b67f9de4a078f41f7a7</RequestID>
</AllocateAddressResponse>
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

```python--boto3
# Not supported by this SDK
```

```ruby
# Not supported by this SDK
```

```php
# Not supported by this SDK
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.associate_address(InstanceId='1111', PublicIp='69.23.22.11')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.associate_address({ instance_id: "1111", public_ip: "69.33.235.235" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->associateAddress(array(
	'InstanceId' => '1111', 
	'PublicIp' => '69.39.39.39'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('AssociateAddress', 'InstanceId=2632&PublicIp=69.39.235.242');
```

> Sample AssociateAddress XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<AssociateAddressResponse>
	<return>true</return>
	<RequestID>332aa29ac2f273b2b507d54ba5039fc6</RequestID>
</AssociateAddressResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_addresses(PublicIps=['69.23.22.11'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_addresses({ public_ips: ["69.39.235.241"]})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeAddresses(array(
	'PublicIp' => '69.39.39.39'));
```

```php--raw
<?php
require('vendor/autoload.php');

$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeAddresses', 'PublicIp.1=69.39.235.241');
```

> Sample DescribeAddresses XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ReleaseAddressResponse>
	<return>true</return>
	<RequestID>2a8312d3b0214a808c15c15d9f558935</RequestID>
</ReleaseAddressResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.disassociate_address(PublicIp='69.23.22.11')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.disassociate_address({ public_ip: "69.33.235.235" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->associateAddress(array(
	'InstanceId' => '1111', 
	'PublicIp' => '69.39.39.39'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DisassociateAddress', 'PublicIp=69.39.235.242');
```

> Sample DisassociateAddress XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DisassociateAddressResponse>
	<return>true</return>
	<RequestID>f8bef95fe215cfa684218999b4960d5e</RequestID>
</DisassociateAddressResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.release_address(PublicIp='69.23.22.11')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.release_address({ public_ips: "69.39.235.241"})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->releaseAddress(array(
	'PublicIp' => '69.39.39.39'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('ReleaseAddress', 'PublicIp=69.39.235.241');
```

> Sample ReleaseAddress XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeAddressesResponse>
	<addressesSet>
		<item>
			<publicIp>69.39.235.241</publicIp>
			<domain>standard</domain>
		</item>
	</addressesSet>
	<RequestID>23d4749fb8ce14714bce8f6415d5a622</RequestID>
</DescribeAddressesResponse>
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

```python--boto3
# Not supported by this SDK
```

```ruby
# Not supported by this SDK
```

```php
# Not supported by this SDK
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_image_attribute(Attribute='description', ImageId='ubuntu64_14.04.1')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_image_attribute({attribute: "description", image_id: "ubuntu64_14.04.1"})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

// Describe all iamges
$ret = $ec2Client->describeImages();

// Describe single image
$ret = $ec2Client->describeImages(array(
		'ImageIds' => array('ubuntu64_14.04.1')));
```

```php--raw
<?php
require('vendor/autoload.php');

$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeImageAttribute', 'ImageId=ubuntu64_14.04.1&Attribute=description');
```

> Sample DescribeImageAttribute XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeImageAttributeResponse>
	<ImageId>ubuntu64_14.04.1</ImageId>
	<description>
		<value>Ubuntu 14.04.1 LTS AMD64</value>
	</description>
	<RequestID>d47a65af377300d4efbd1b79add5d7b4</RequestID>
</DescribeImageAttributeResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

# Describe all images
resp = ec2.describe_images()

# Describe single image
resp = ec2.describe_images(ImageIds=['ubuntu64_14.04.1'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
 
# Describe all images
i = ec2.describe_images({})

# Describe single image
i = ec2.describe_images({ image_ids: ["ubuntu64_14.04.1"]})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

// Describe all images
$ret = $ec2Client->describeImages();

// Describe one image 
$ret = $ec2Client->describeImages(array(
		'InstanceIds' => array('ubuntu64_14.04.1')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeImages', 'ImageId.1=ubuntu64_14.04.1');
```

> Sample DescribeImages XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeImagesResponse>
  <imagesSet>
    <item>
      <imageId>ubuntu64_14.04.1</imageId>
      <imageLocation>gigenet</imageLocation>
      <imageState>active</imageState>
      <imageOwnerId>gigenet</imageOwnerId>
      <isPublic>true</isPublic>
      <architecture>x86_64</architecture>
      <imageType>machine</imageType>
      <imageOwnerAlias>gigenet</imageOwnerAlias>
      <name>ubuntu64_14.04.1</name>
      <description>Ubuntu 14.04.1 LTS AMD64</description>
      <platform>Ubuntu</platform>
      <virtualizationType>hvm</virtualizationType>
      <hypervisor>xen</hypervisor>
    </item>
  </imagesSet>
  <RequestID>122b388ffdee67b98690051c8ac6cd0d</RequestID>
</DescribeImagesResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_availability_zones()
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_availability_zones({})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeAvailabilityZones();
```

```php--raw
<?php
require('vendor/autoload.php');

$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeAvailabilityZones');
```

> Sample DescribeAvailabilityZones XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeAvailabilityZonesResponse>
	<availabilityZoneInfo>
		<item>
			<regionName>ord1</regionName>
			<zoneName>ord1</zoneName>
			<zoneState>available</zoneState>
			<messageSet>
				<message>Location: Arlington Heights, IL Zone 2</message>
			</messageSet>
		</item>
		<item>
			<regionName>ord1</regionName>
			<zoneName>ord1</zoneName>
			<zoneState>unavailable</zoneState>
			<messageSet>
				<message>Location: Arlington Heights, IL [CMAN]</message>
			</messageSet>
		</item>
		<item>
			<regionName>lax1</regionName>
			<zoneName>lax1</zoneName>
			<zoneState>unavailable</zoneState>
			<messageSet>
				<message>Location: Los Angeles, CA</message>
			</messageSet>
		</item>
		<item>
			<regionName>ord1</regionName>
			<zoneName>ord1</zoneName>
			<zoneState>available</zoneState>
			<messageSet>
				<message>Location: Arlington Heights, IL</message>
			</messageSet>
		</item>
	</availabilityZoneInfo>
	<RequestID>01040b5a9c1c571eaa7eb1312be6736b</RequestID>
</DescribeAvailabilityZonesResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#availabilityZoneInfoSet_5af9b3d83d429').toggle();return false;">Members</a>)
<table id='availabilityZoneInfoSet_5af9b3d83d429' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_regions()
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_regions({})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeRegions();
```

```php--raw
<?php
require('vendor/autoload.php');

$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeRegions');
```

> Sample DescribeRegions XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeRegionsResponse>
	<regionInfo>
		<item>
			<regionEndpoint>api.thegcloud.com</regionEndpoint>
			<regionName>ord1</regionName>
		</item>
	</regionInfo>
	<RequestID>728f818461f481e7cc3a97671045f2a0</RequestID>
</DescribeRegionsResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#regionInfoSet_5af9b3d83d4d3').toggle();return false;">Members</a>)
<table id='regionInfoSet_5af9b3d83d4d3' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.create_key_pair(KeyName='test_key')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.create_key_pair({ key_name: "my-key-name" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->createKeyPair(array('KeyName' => 'test-key-pair'));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('CreateKeyPair', 'KeyName=test-key-pair');
```

> Sample CreateKeyPair XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CreateKeyPairResponse>
	<keyName>test-key-pair</keyName>
	<keyFingerprint>23:cf:b0:a4:29:b4:d3:40:0f:db:b3:49:e5:35:0c:bf:be:6b:9b:fb</keyFingerprint>
	<keyMaterial>-----BEGIN PRIVATE KEY-----
	MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQC0vT/F+wvCk6eX
	GlTKXzGfZ0MweDnINmQWCzq0LGKj1VhH5VnSLJkoJEHx6pJw71iLmLztW2//ngby
	G3RIElcXWHCXMl8S7kpCuttvpSHwt6V6u/bMYc3irvzbYfk3wDXzGLgX41f+nRxE
	qW7nkIevd4crOgSOgU1v21AVI3LMs57TSVmEQd9u3RUp9OtN/Z96MCyYEYggvCKr
	kqUV93ggB9j9joZc1I7XmHOHtn1ugjrMFSrXUmotQuNuM1Y8Hysm8GQk7N+iw9+a
	24JXhQDCJVbWNR4qDPbcR/K3QXWuEe27lKCiiR52lU+mYlDWL+0x5jRidmHJ+V6P
	v07Hco41AgMBAAECggEACDfiwnnb2wkjwbcsy9bwRrNHVtjgp73xZx8zmCW8hn6Y
	+QvwvaHRhQXBCeMEraX0fMSBMrnJqfHhlviwnOZYl3MqC3X65L15GvesKrNzi6KO
	H7qUSk7YMcqLLN6Tmnle+qLRHCT2R1mVg3nA1T65LL1epBSLSH+QqdlrFsr52Vzt
	3IvgFqM2CaS3Npezvij+8YQF+fU/LOnN+xVNuaLf5FNr/sVMTfeYps3YcTm49SWO
	483VyKyvKQ/sKCmPtzwZuQC9xgJl+qkt3SvMLEl/6ckKc0zy61SL6x+zploRe3PK
	ThORUjcPmfvQqq1ahNiZIJdjfH2Ajg6hU/NNYI2rAQKBgQDu2fg9HTVJvYP8M+sD
	6cEwpKD2RWK2mOLcAYvLQxFt585d556GUTqjJMhnjKjgvRcCoCLpizo2+xtExpHA
	y2sJzktP8R/Cbun2OJoF3VMY0zxlY2hV+KEH6xeRDkW6jWssKixvqpa2EGM35R4m
	Nu3X+nhk1Jq8HzaeMCeoRK8ZRQKBgQDBtzEZcAsm+O3QLBSzAC2P8zMqIDyjTKlD
	fsqlrxwzhfFKyjqlZEPKKSYEgDGBTN1MrA5Lu+drZnbkZznR2YZYkzFh9/7wyLZ5
	KRJLVPCZpfrKlu6cL2ff2drspsYjzWKRTN1rO0Ow0Gz37WuUnO25tdacBVqywzpi
	r5pJDrNYMQKBgGRVd+vkOyBQ1gK5pH2uUhMm9N6+4uqlapbUp26pK8cpWw0jYPo3
	YRRrPSwScFaH2ASoVEIa1EeIUDoh19RPHxWtbQGV3quEgA+IU1snT+LbyUEl8ww6
	NxrmbK3oeu4UvfJ9fNEjrc+pLqSqQHH5HQxfEPf6P03LJtxoiiArSgqpAoGAMwO2
	Z3eNSE8n+bmSHe2/Efi/Ean5rhujO8YpQebSq3Lrr4GAXkwAWj3p6CeGYgHHCckJ
	3sH2WN9cEhxpKq15ZtwkliNEPU7uVwwM6E/PKPeAC1giMHl/hoEN2WK2LXmKKq+u
	Y+3wjqDlAYnB2hpVtKGBigcS8p7dQl3yaKj5bBECgYAcXJaAi28R8QJly7V2ZXH1
	pnwe5F+kE5dqeZtR+1Y1PsCb81X3e2nJoZ3yMXuVKAsuQJ7dM8tps5s+A8+WT354
	LjJLfHnVezPfcdewu7fff9y3hP/DBpBndP/MZUzMab1B4sJfePBgkjXxstZ0Xpf6
	5XfwbDE+80wPf2KkMuTi/A==
	-----END PRIVATE KEY-----
	</keyMaterial>
	<RequestID>f997fa212094383d896215550230a08d</RequestID>
</CreateKeyPairResponse>

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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.delete_key_pair(KeyName='test_key')
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.delete_key_pair({ key_name: "my-key-name" })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->deleteKeyPair(array('KeyName' => ('test-key-pair')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DeleteKeyPair', 'KeyName=test-key-pair');
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_key_pairs(KeyNames=['test_key'])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_key_pairs({ key_names: [ "my-key-namea "] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeKeyPairs(array('KeyNames' => array('test-key-pair')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeKeyPairs', 'KeyName.1=test-key-pair');
```

> Sample DescribeKeyPairs XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeKeyPairsResponse>
	<keySet>
		<item>
			<keyName>test-key-pair</keyName>
			<keyFingerprint>50:30:71:b2:10:68:bb:7c:fa:0a:55:14:f7:f1:f0:91:47:a9:71:09</keyFingerprint>
		</item>
	</keySet>
	<RequestID>3be58fe350b32f09b9f8b834beee69bd</RequestID>
</DescribeKeyPairsResponse>

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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.import_key_pair(
	KeyName='test_key',  
	PublicKeyMaterial=base64.b64encode("ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA27Qd8PiFw+FYhPOJgDp9lo9bUP6NJEGtjyAK+o+oyd8HKEqORSVzM9vG81mHkapkr3VCBkZKgF6GF8Lfc2cUlC9g4XYJErjBeWmuWYo8Fq1ch1QTQUDkJfRaI1lNSuzS/8KvKVi4yO4ydOoCM7rG5yFiwtrPcxy8CeuwkA6DpyHtoIspOpzD5C6kcTyhf3PdPk/qMTB1h9oa0gpqmh8ns1yYI3Lxud8AYf63Awm9/V1WxwCMxHailKbE0glgw95PTJGUL6FVyc+awXg3xn48TjNT9dR82Dr4OPUgZq7fZHArcSyavoWzvjeQqcCN5qkcCAUZ1ZpSgWj/FOZIENlMDw== test@thegcloud.com'"))


```

```ruby
require 'aws-sdk'
require 'base64'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
 
i = i = ec2.import_key_pair({
    key_name: "test-key",
    public_key_material: Base64.encode64("ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA27Qd8PiFw+FYhPOJgDp9lo9bUP6NJEGtjyAK+o+oyd8HKEqORSVzM9vG81mHkapkr3VCBkZKgF6GF8Lfc2cUlC9g4XYJErjBeWmuWYo8Fq1ch1QTQUDkJfRaI1lNSuzS/8KvKVi4yO4ydOoCM7rG5yFiwtrPcxy8CeuwkA6DpyHtoIspOpzD5C6kcTyhf3PdPk/qMTB1h9oa0gpqmh8ns1yYI3Lxud8AYf63Awm9/V1WxwCMxHailKbE0glgw95PTJGUL6FVyc+awXg3xn48TjNT9dR82Dr4OPUgZq7fZHArcSyavoWzvjeQqcCN5qkcCAUZ1ZpSgWj/FOZIENlMDw== test@thegcloud.com'")})
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$
$ret = $ec2Client->importKeyPair(
	array(
		'KeyName' => 'test-key-pair',
		'PublicKeyMaterial' => base64_encode('ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA27Qd8PiFw+FYhPOJgDp9lo9bUP6NJEGtjyAK+o+oyd8HKEqORSVzM9vG81mHkapkr3VCBkZKgF6GF8Lfc2cUlC9g4XYJErjBeWmuWYo8Fq1ch1QTQUDkJfRaI1lNSuzS/8KvKVi4yO4ydOoCM7rG5yFiwtrPcxy8CeuwkA6DpyHtoIspOpzD5C6kcTyhf3PdPk/qMTB1h9oa0gpqmh8ns1yYI3Lxud8AYf63Awm9/V1WxwCMxHailKbE0glgw95PTJGUL6FVyc+awXg3xn48TjNT9dR82Dr4OPUgZq7fZHArcSyavoWzvjeQqcCN5qkcCAUZ1ZpSgWj/FOZIENlMDw== test@thegcloud.com')));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('ImportKeyPair', 'KeyName=testkey123&PublicKeyMaterial='.base64_encode('ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA27Qd8PiFw+FYhPOJgDp9lo9bUP6NJEGtjyAK+o+oyd8HKEqORSVzM9vG81mHkapkr3VCBkZKgF6GF8Lfc2cUlC9g4XYJErjBeWmuWYo8Fq1ch1QTQUDkJfRaI1lNSuzS/8KvKVi4yO4ydOoCM7rG5yFiwtrPcxy8CeuwkA6DpyHtoIspOpzD5C6kcTyhf3PdPk/qMTB1h9oa0gpqmh8ns1yYI3Lxud8AYf63Awm9/V1WxwCMxHailKbE0glgw95PTJGUL6FVyc+awXg3xn48TjNT9dR82Dr4OPUgZq7fZHArcSyavoWzvjeQqcCN5qkcCAUZ1ZpSgWj/FOZIENlMDw== test@thegcloud.com'));
```

> Sample ImportKeyPair XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ImportKeyPairResponse>
  <keyName>testkey123</keyName>
  <keyFingerprint>d4:1d:8c:d9:8f:00:b2:04:e9:80:09:98:ec:f8:42:7e</keyFingerprint>
  <RequestID>d57a6d9d2dce3cb6a6c60ee4b3a7a048</RequestID>
</ImportKeyPairResponse>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.create_tags(Resources=["1111"], Tags=[ { 'Key': 'test-tag-1', 'Value': 'ignored' } ])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.create_tags({ resources: ["1111"], tags: [{ key: "test-tag", value: "" }] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->createTags(array(
		'Resources' => array('2632'),
		'Tags' => array( array( 'Key' => 'test-tag-123', 'Value' => 'ignored' ))));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('CreateTags', 'ResourceId.1=2632&Tag.1.Key=test-tag&Tag.1.Value=');
```

> Sample CreateTags XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CreateTagsResponse>
	<return>true</return>
	<RequestID>87c3f0bfa83b198ab649eb96755f1a4f</RequestID>
</CreateTagsResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tag_5af9b3d83d725').toggle();return false;">Members</a>)
<table id='Tag_5af9b3d83d725' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.delete_tags(Resources=['1111'], Tags= [ {'Key': 'test-tag', 'Value': 'ignored'} ])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.delete_tags({ resources: ["1111"], tags: [{ key: "test-tag", value: "" }] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->deleteTags(array(
		'Resources' => array('2632'),
		'Tags' => array( array( 'Key' => 'test-tag-123', 'Value' => 'ignored' ))));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DeleteTags', 'ResourceId.1=2632&Tag.1.Key=test-tag&Tag.1.Value=');
```

> Sample DeleteTags XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DeleteTagsResponse>
	<return>true</return>
	<RequestID>460275b13ebc0992a3cb41c5fe11f1cd</RequestID>
</DeleteTagsResponse>
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
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Tag_5af9b3d83d7d2').toggle();return false;">Members</a>)
<table id='Tag_5af9b3d83d7d2' style='display:none'>
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

```python--boto3
import boto3

ec2 = boto3.client('ec2', 
	endpoint_url='https://api.thegcloud.com', 
	aws_access_key_id='APIKEY', 
	aws_secret_access_key='APIHASH', 
	region_name='ord1');

resp = ec2.describe_tags(Filters=[{ 'Name': 'resource-id', 'Values': ['1111'] }])
```

```ruby
require 'aws-sdk'

ec2 = Aws::EC2::Client.new(
  endpoint: 'https://api.thegcloud.com',
  region: 'ord1',
  access_key_id: 'APIKEY',
  secret_access_key: 'APIHASH'
)
  
i = ec2.describe_tags({ filters: [ { name: "resource-id", values: ["1111"] } ] })
```

```php
<?php

require('vendor/autoload.php');

use \Aws\Ec2\Ec2Client;


$ec2Client = Ec2Client::factory(array(
  'endpoint' => 'https://api.thegcloud.com',
  'region' => 'ord1',
  'credentials' => array(
    'key' => 'APIKEY',
    'secret' => 'APIHASH'
  )
));

$ret = $ec2Client->describeTags(array(
		'Filters' => array(
			array( 
				'Name' => 'resource-id', 
				'Values' => array('2632') )
		)));
```

```php--raw
<?php
require('vendor/autoload.php');


$access_key = 'APIKEY';
$secret_key = 'APIHASH';
$api_url = 'https://api.thegcloud.com';

// For documentation of the apiRequest method 
// see the documentation section 'Connecting to the API'
print apiRequest('DescribeTags', 'ResourceId.1=2632');
```

> Sample DescribeTags XML return:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DescribeTagsResponse>
	<tagSet>
		<item>
			<resourceId>1111</resourceId>
			<resourceType>instance</resourceType>
			<key>test-tag</key>
		</item>
	</tagSet>
	<RequestID>a13161cad1123f503e129a761d8e3249</RequestID>
</DescribeTagsResponse>
```

Describes one or more of tags assigned to CloudMachine.

### Parameters

<table><tr><th>Name</th><th>Type</th><th>Required?</th><th>Default</th><th>Description</th></tr>
<tr>
<td>Filter</td>
<td><a href='#types'>array</a>&nbsp;(<a href='#' onClick="$('#Filter_5af9b3d83d876').toggle();return false;">Members</a>)
<table id='Filter_5af9b3d83d876' style='display:none'>
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







