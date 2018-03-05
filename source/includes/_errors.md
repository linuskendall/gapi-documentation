# Errors

> Sample XML error response from the API:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Response>
	<Errors>
		<Error>
			<Code>MalformedQueryString</Code>
			<Message>You have provided a malformed query string</Message>
		</Error>
	</Errors>
	<RequestID>35d1289884eb27ee28057a28d69b72ed</RequestID>
</Response>
```

The HTTP error code returned from the API response will be one of:
 
 * 400 - A client or sender error occurred, meaning an error in the parameters or the conditions of the API call.
 * 401 - An authentication error occurred.
 * 500 - A server error, meaning that the server experienced an unexpected error or fault.

4xx errors are as a result of the input you have provided to the API, while a 500 error means there has been an error in our backend - if it re-occurs please contact customer service.

Type | Exception Name | Meaning
---- | -------------- | -------
Auth | AuthFailure | Your API authentication details are incorrect.
Auth | SignatureDoesNotMatch | The signature you have calculated for the request is not valid.
Sender | IncompleteSignature | The signature provided lacked fields.
Sender | MissingAuthenticationToken | No or incomplete authentication token provied.
Client | MissingAction | You did not specify an API action.
Client | InvalidAction | The action you requested is not supported by our API.
Client | RequestExpired | The request expired, please try again.
Client | MalformedQueryString | The query string provided with the request was invalid.
Client | ValidationError | Could not validate your input, one or more values are invalid.
Client | MissingParameter | A required parameter for the API call is missing.
Client | AddressLimitExceeded | You have used the maximum number of addresses.
Client | MaxSpotInstanceCountExceeded | You have requested too many instances.
Client | RequestResourceCountExceeded | You have exceedd the limit for the number of resources you are trying to create.
Client | TagLimitExceeded | You have used the maximum number of tags on your account.
Client | InsufficientFunds | There is too little funds to execute this operation.
Client | InvalidInstanceAttributeValue | One of the attributes specified for the instance is invalid.
Client | InvalidInstanceType | The instance type requested for the cloud machine was invalid.
Client | InvalidParameterValue | One of the parameters provided had an invalid format.
Client | InvalidAMIID.NotFound | The cloud machine image requested could not be found.
Client | InvalidAMIID.NotAvailable | The cloud machine image requested is not available for new instances.
Client | InvalidHostname.Duplicate | You specified a duplicate hostname.
Client | InvalidSubnetID.NotFound | The network subnet id provided was not found.
Client | InvalidState | The cloud machine is in an invalid state to run this action.
Client | InvalidInstanceID.NotFound | The cloud machine instance you specified could not be found.
Client | InvalidZone.NotFound | The region or zone you specified is invalid.
Client | InvalidAddress.NotFound | The address you specified could not be found.
Client | InvalidInput | An invalid input was rovided to the call.
Client | InvalidKeyPair.NotFound | The corresponding SSH Key could not be found.
Client | InvalidKeyPair.Duplicate | A duplicate SSH key was uploaded.
Server | DryRunOperation | The DryRun succeeded, the API call could be executed and permission was given to run it.
Server | ServerError | An internal error occurred, try later or contact customer service.
