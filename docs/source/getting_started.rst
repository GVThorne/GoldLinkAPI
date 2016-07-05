Getting Started
===============

****************
About the API?
****************

The Gold-Link API is a SOAP based Web Service that is installed as part of the core product. The API is used by sending XML requests over the HTTP protocol.

In order to use the API you must be using a logical programming language that supports SOAP Web Service interoperability. The recommended choice on a Windows platform is to use .NET Framework and on a Linux platform is to use PHP. 

.. note:: 
    If using .NET Framework, the Gold-Vision API web service can be automatically integrated using the Visual Studio "Add Web Referenece" option.

**********
Connecting
**********
The API needs to be enabled through the product licence. If the API is not enabled for your installation or instance, please contact Gold-Vision Support at support@gold-vision.com or **+44(0) 1788 511 110**

Address
#######

You can access the web service by using the URL::
    
	<your Gold-Vision URL>/gold-link/goldlink.asmx
	
For example::

    https://example.goldvisioncrm.com/gold-link/goldlink.asmx

Authentication
##############

Authentication is performed using NTLM Authentication. Therefore, to use the API, the user's credentials must match that of a valid Gold-Vision user.

.. note::

    You can also visit the web service URL to view a list of the available methods through the API.

*****************
HTTP SOAP Example
*****************

The following is a sample SOAP 1.2 request and response for the method **AddItem**. The placeholders shown needs to be replaced with actual values. This example was found by visiting the Gold-Link URL and selecting the **AddItem** method, you can obtain similar examples for the other methods.

**Request**

.. code-block:: html

    POST /example.goldvisioncrm.com/gold-link/goldlink.asmx HTTP/1.1
	Host: example.goldvisioncrm.com
	Content-Type: application/soap+xml; charset=utf-8
	Content-Length: length

	<?xml version="1.0" encoding="utf-8"?>
	<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
		<soap12:Body>
			<AddItem xmlns="http://service.gold-vision.com/gold-link">
				<objectType>Root or Account or Contact or AccountActivity or ContactActivity or OpportunityActivity or ProjectActivity or Opportunity or Quote or Project or Profile or Product or Extension or SageSopData or SagePopData or QuoteLines or Note or SageProduct or Seminar or SeminarSession or SeminarBooking or SeminarSessionAttendee or SeminarBookingProduct or SeminarSessionProduct or IntegrationLinkList or SeminarBookingAttendee or ExchequerTxData or QuoteItem or Campaign or FormData or Appointment or AccountFinancialEntity</objectType>
				<xmlData>xml</xmlData>
			</AddItem>
		</soap12:Body>
	</soap12:Envelope>

**Response**

.. code-block:: html

    HTTP/1.1 200 OK
	Content-Type: application/soap+xml; charset=utf-8
	Content-Length: length

	<?xml version="1.0" encoding="utf-8"?>
	<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
		<soap12:Body>
			<AddItemResponse xmlns="http://service.gold-vision.com/gold-link">
				<AddItemResult>boolean</AddItemResult>
				<returnId>string</returnId>
				<success>boolean</success>
				<message>string</message>
			</AddItemResponse>
		</soap12:Body>
	</soap12:Envelope>

***************
Handling Errors
***************

Part of the XML response for any API call is **success** and **message**. If the API call failed for any reason, **success** will be false and **message** will be the error message. There are also Gold-Vision error logs that you can access from within the administration console under **Settings > Logging**, look for the log file title **Gold-Link_{date}.txt**

