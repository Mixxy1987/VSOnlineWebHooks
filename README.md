#Webhooks

Webhooks are custom HTTP callbacks caused by some events in the system.
When an event occurs in the system, the source site makes a request to the specified URL.

##Webhooks settings

	On the portal veriscanonline.com you can set up webhooks on the page
''Settings -> Integration Services -> Webhooks''
or
https://veriscanonline.com/Settings/Webhooks

	Events that call web hooks in veriscanonline.com are
* Create History Record;
* Update History Record;
* Sign Agreement
	
	Check the checkbox ''Active'' and select the necessary events in the panel
''Settings''.
	Next, you should create one or more endpoints (up to 5).
	Specify the URL which the HTTP request will be executed to 
and check the checkbox ''Active''.
	Advice. Add a secret parameter to your URL that you are sure that the request came from VeriScan Online system.
	
	By default, veriscanonline sends a POST request in JSON format.	

{code:lang=json|title=Webhook format}	
{
  "Created": "2018-01-01T01:01:01.0000001Z",
  "Sent": "2018-01-01T01:01:01.0000001Z",
  "EventId": 0,
  "WebHookId": 0,
  "Type": "CreateCard",
  "WebHookTypeId": 2,
  "Data": {
    "HistoryLogId": 0,
    "Scanned": "2018-01-01T01:01:01.1",
    "IdNum": "IdNum",
    "FirstName": "FirstName",
    "MiddleName": "MiddleName",
    "LastName": "LastName",
    "BirthDate": "1960-01-01T01:00:00",
    "ExpDate": "2020-01-01T01:00:00",
    "State": "TN",
    "PostalCode": "99999-0000",
    "City": "City",
    "Address": "Address",
    "Gender": "Male",
    "Comments": null,
    "Phone": null,
    "Email": null,
    "GroupId": null,
    "GroupComment": null,
    "DeviceId": 9999,
    "LocationId": 999,
    "HashId": "00000000-0000-0000-0000-000000000000",
    "PhotoBase64": null,
    "Latitude": null,
    "Longitude": null,
    "IsGeoUpdated": null,
    "Tags": null,
    "Country": "UNITED STATES",
    "ScanLatitude": 0.00001,
    "ScanLongitude": -0.00001,
    "CountryCode": "USA",
    "LocationName": "LocationName",
    "GroupName": null,
    "DeviceName": "DeviceName",
    "DeviceLogin": "DeviceLogin",
    "CompletedSurvey": null
  }
}
{code}

	If you use a format other than JSON (XML, SOAP, ...), then you can use Body Template with the tags replaced with values.
For example.

{code:lang=xml|title=XML body template sample}
<?xml version="1.0" encoding="utf-8"?>
<Card xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <Scanned>%Scanned%</Scanned>
  <IdNum>%IDNum%</IdNum>
  <FirstName>%FirstName%</FirstName>
  <MiddleName>%MiddleName%</MiddleName>
  <LastName>%LastName%LastName>
  <BirthDate>%BirthDate%</BirthDate>
  <ExpDate>%ExpDate%</ExpDate>
  <State>%JurisdictionCode%</State>
  <PostalCode>%PostalCode%</PostalCode>
  <City>%City%</City>
  <Address>%Address%</Address>
  <Gender>%Gender%</Gender>
  <Comments>%Comments%</Comments>
  <Phone>%Phone%</Phone>
  <Email>%Email%</Email>
  <Tags>%Tags%</Tags>
  <GroupName>%GroupName%</GroupName>
  <DeviceName>%DeviceName%</DeviceName>
</Card>
{code}

	For each endpoint, you can specify HTTP-header.	
	
	For example, you can specify ''Content-Type text/xml'' if your endpoint receives data in XML format.
Or you can specify ''Authorization Basic bG9naW46cGFzc3dvcmQ='' (login:password in base64 format), if you use Base64-authorization.

	If your endpoint uses the OAuth authentication protocol, then you can save and then use AccessToken and RefreshToken.
	
	After you have successfully configured the endpoint and set the necessary settings on our portal, try to scan the card or
sign the agreement or update the card in accordance with the selected events.

##Webhooks history
			
	The history of the sent webhooks is displayed on the ''History'' tab.
	
	You can filter the history according to the ''Success/Fail'' criteria.
	A webhook is considered to be successful, which your service responded on with the HTTP status of 2XX.
	
	You can see the raw data sent along with the webhook. To do this, click on the ''Data/Response'' column.
	The data your service returned is displayed in the same location.
	
	You can see the data of the card if you press the ''History Log'' button.
