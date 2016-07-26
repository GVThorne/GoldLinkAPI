Getting Started
===============

.. |visual_studio| raw:: html

    <a href="https://msdn.microsoft.com/en-us/library/bb628649.aspx" target="_blank">Microsoft Visual Studio - Add Web Reference</a>
	
.. |soapui| raw:: html

    <a href="https://www.soapui.org/" target="_blank">SoapUI</a>

************
Introduction
************

The Gold-Link API is a SOAP based Web Service that is installed as part of the core product. The API is used by sending XML requests over the HTTP protocol.

In order to use the API you must be using a logical programming language that supports SOAP Web Service interoperability. The recommended choice on a Windows platform is to use .NET Framework and on a Linux platform is to use PHP. 

.. note:: 
    If using .NET Framework, the Gold-Vision API web service can be automatically integrated using the Visual Studio "Add Web Reference" option. More information on how to use this feature can be found here -  |visual_studio|.

**********
Connecting
**********
The API needs to be enabled through the product licence. If the API is not enabled for your installation or instance, please contact Gold-Vision Support at support@gold-vision.com or **+44(0) 1788 511 110** (UK & Europe) or **+1 (647) 494 9870** (North America) | **+1 (877)673 1230** (Toll-Free)

Address
#######

You can access the web service by using the URL::
    
	<your Gold-Vision URL>/gold-link/goldlink.asmx
	
For example::

    https://example.goldvisioncrm.com/gold-link/goldlink.asmx
	
.. note::

    * The Gold-Vision API is built into individual implementations and therefore the URL will be unique for a particular install.
    * Visiting the web service URL will let you view a list of the available methods through the API.

Authentication
##############

Authentication is performed using NTLM Authentication. Therefore, to use the API, the user's credentials must match that of a valid Gold-Vision user.


*****************
HTTP SOAP Example
*****************

The following is a sample SOAP request and response for the method :ref:`AddItem`.

**Request**

.. code-block:: html

    POST /example.goldvisioncrm.com/gold-link/goldlink.asmx HTTP/1.1
	Host: example.goldvisioncrm.com
	Content-Type: application/soap+xml; charset=utf-8
	
    <?xml version="1.0" encoding="utf-8"?>
	<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://service.gold-vision.com/gold-link">
	<soap:Body>
		<AddItem xmlns="http://service.gold-vision.com/gold-link">
		 <objectType>Account</objectType>
		 <xmlData>
		  <gvdata xmlns="">
		   <record>
		    <field name="SUMMARY">Holding Ltd</field>
		    <field name="NAME">Holding Ltd</field>
		    <field name="ADDRESS_1">321 New Street</field>
		    <field name="TOWN">London</field>
		    <field name="COUNTRY">United Kingdom</field>
		   </record>
		  </gvdata>
		 </xmlData>
		</AddItem>
	</soap:Body>
    </soap:Envelope>

**Response**

.. code-block:: html

    HTTP/1.1 200 OK
	Content-Type: application/soap+xml; charset=utf-8
	Content-Length: length

	<?xml version="1.0" encoding="utf-8"?>
	<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://service.gold-vision.com/gold-link">
		<soap:Body>
			<AddItemResponse xmlns="http://service.gold-vision.com/gold-link">
				<AddItemResult>true</AddItemResult>
				<returnId>71fb89cb-92ad-4973-8293-d43f1cd98673</returnId>
				<success>true</success>
				<message></message>
			</AddItemResponse>
		</soap:Body>
	</soap:Envelope>

********************
SOAP Request Testing
********************
If you are unfamiliar with making SOAP requests, a good point to start with is to use a Functional Testing solution such as  |soapui|.

By using a solution such as **SoapUI**, you are able to send requests to Gold-Link and observe the responses within a user friendly user interface.

.. note::

    Throughout the rest of this documentation, all of the SOAP requests and responses have been generated using a Functional Testing solution.
	
***************
Handling Errors
***************

Part of the XML response for any API call is **success** and **message**. If the API call failed for any reason, **success** will be false and **message** will contain the error message.

The Gold-Vision log files will contain detailed error messages and can be accessed through **Settings > Logging** within the Administration Console. The file containing the Gold-Link errors will be labelled as **Gold-Link_{date}.txt**.



