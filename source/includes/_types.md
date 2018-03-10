# Types

Below you can find description and example of the types of parameters that you can provide to the API calls.

Data&nbsp;type | Description | Example
--------- | ----------- | -------
string  | URL encoded string | SSHKeyName=Macbook+Key
stringlist |  List of string values | InstanceId.0=1223&InstanceId.1=1333
int | Numbered value | MyInt=132
array | A list of named values, each member of the array can have multiple named values. |  ArrayValue.0.Key=first+ip&<br/>ArrayValue.0.IpAddress=192.168.3.3&<br/>ArrayValue.1.Key=second+ip&<br/>ArrayValue.1.IpAddress=192.168.3.10
boolean | A true/false boolean value | DryRun=True
