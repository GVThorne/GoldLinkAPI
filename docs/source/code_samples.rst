Code Samples
============

**********
Javascript
**********

First a XML HTTP request object will be generated and the API endpoints will be declared as follows:

.. code-block:: javascript


    var http_glink = null;
    var soap_ns = 'http://service.gold-vision.com/gold-link'
    var soap_get_version = '"'+soap_ns+'/GetVersion"';
    var soap_find_item = '"'+soap_ns+'/FindItem"';   
    var soap_get_item = '"'+soap_ns+'/GetItem"';   
    var soap_add_item = '"'+soap_ns+'/AddItem"';   
    var soap_update_item = '"'+soap_ns+'/UpdateItem"';   
    var soap_get_drop_options = '"'+soap_ns+'/GetDropOptions"';  
	
    // This generates an XML Http request object
    function glink_getXmlHttp() {
	try {
		var req;
		try { req = new XMLHttpRequest(); }
		catch (e2) {
			try { req = new ActiveXObject("Msxml2.XMLHTTP"); }
			catch(e3) {
				try { req = new ActiveXObject("Microsoft.XMLHTTP"); } 
				catch (e4) { req = false; }
			}
		}		
		return req;
	} catch(e) { alert('Error: ' + e.message); }
	}
	
Then, create the object that will be executed to make the request. It will take in a SOAP Action and return with the response. This is what it will look like:

.. code-block:: javascript

    function glink_execute(soapAction, soapXml, callBackFunction) {
	var s = '';                    
	s += '<?xml version="1.0" encoding="utf-8"?>';
	s += '<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">';
	s += '  <soap:Body>';
	// Soap data
	s += soapXml;
	s += '  </soap:Body>';
	s += '</soap:Envelope>';   
	// Process request
	http_glink = this.getXmlHttp();
	http_glink.open('POST', this.url + '?z=' + new Date().getTime(), true); 	
	http_glink.setRequestHeader("Content-Type", "text/xml; charset=utf-8");
	http_glink.setRequestHeader("Content-Length", s.length);
	http_glink.setRequestHeader("SOAPAction", soapAction);
	http_glink.onreadystatechange = function() {
		if (http_glink.readyState == 4) {
			if (http_glink.status == 200)
				callBackFunction(http_glink.responseXML);
			else if (http_glink.status == 500)
				alert("500 - Server error!");
			else if (http_glink.status == 404) 
				alert("404 - Service not found!");
			else 
				alert("Unexpected status: " + http_glink.status);
		}	            
	}
	http_glink.send(s);
	}

Now, create our functions to make the SOAP requests. For example, a :ref:`FindItem` request will look like this:

.. code-block:: javascript

    function glink_findItem(objectType, filterParams, extraFields, callBackFunction) {
		// Build find 
		var s = '';
		s += '<FindItem xmlns="'+soap_ns+'">';
		s += '<objectType>'+objectType+'</objectType>';
		s += '<XmlFilters><filters xmlns="">';
		for (i = 0; i < filterParams.length; i++) 
			s += '<filter dbcolumn="'+filterParams[i]["dbcolumn"]+'" type="'+filterParams[i]["type"]+'" value="'+filterParams[i]["value"]+'" />';    
		for (i = 0; i < extraFields.length; i++) 
			s += '<field dbcolumn="'+extraFields[i]["dbcolumn"]+'" />';    
		s += '</filters></XmlFilters>';
		s += '</FindItem>';        
		// Send to Gold-Link
		this.execute(soap_find_item, s, callBackFunction); 
	}
	
Finally, this function simply associates the above functions with the 'glink' object.

.. code-block:: javascript

    function glink(url) {
		// This simply associates the above functions with the 'glink' object
        this.url = url;
        this.execute = glink_execute;
        this.findItem = glink_findItem;
		this.getItem = glink_getItem;
		this.addItem = glink_addItem;
		this.updateItem = glink_updateItem;
		this.getDropOptions = glink_getDropOptions;
		this.getXmlHttp = glink_getXmlHttp;
    }
	
.. note::

    A Javascript example that interacts with the Gold-Link API can be found here: `Javascript Example <https://github.com/GVThorne/GoldLinkAPI/tree/master/javascript_example>`_
	
***
PHP
***

First, a PHP file that contains the authentication details of the SOAP request will be created. This file will be called **GVGoldLinkNTLM.php**.

.. code-block:: php

    <?php
    class GVGoldLinkNTLMSoapClient extends NTLMSoapClient {
	protected $user = 'DOMAIN\USERNAME';
	protected $password = 'PASSWORD';
    }
	?>

Now, the creation of a method for making the requests will exist in a separate file. The following request will be contained within a PHP file called **NTLMSoapClient.php**:

.. code-block:: php

    <?php
    class NTLMSoapClient extends SoapClient {
	function __doRequest($request, $location, $action, $version) {
			
		$headers = array(
			'Method: POST',
			'Connection: Keep-Alive',
			'User-Agent: PHP-SOAP-CURL',
			'Content-Type: text/xml; charset=utf-8',
			'SOAPAction: "'.$action.'"',
		);
		//echo $request;
		$this->__last_request_headers = $headers;
		$ch = curl_init($location);
		curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
		curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
		curl_setopt($ch, CURLOPT_POST, true );
		curl_setopt($ch, CURLOPT_POSTFIELDS, $request);
		curl_setopt($ch, CURLOPT_HTTP_VERSION, CURL_HTTP_VERSION_1_1);
		curl_setopt($ch, CURLOPT_HTTPAUTH, CURLAUTH_NTLM);
		curl_setopt($ch, CURLOPT_USERPWD, $this->user.':'.$this->password);
		$response = curl_exec($ch);
		
		return $response;
	}
	
	function __getLastRequestHeaders() {
		return implode("\n", $this->__last_request_headers)."\n";
	}
    }
	?>
	
Request can now be made using PHP. The following example will make a :ref:`GetVersion` Gold-Link request:

.. code-block:: php

    <!DOCTYPE html>
	<html>
	<head>
		<title>GoldLink with PHP - Basic Examples</title>
	</head>
	<body>
		<h3>GoldLink with PHP - Basic Examples</h3>
		<?php
			// Include the required classes
			include 'GVGoldLinkNTLM.php';

			// The URL of the WSDL file for Gold-Link
			$url = 'http://' . $GVAddress . '/gold-link/goldlink.asmx?wsdl';

			// Unregister the current HTTP wrapper
			stream_wrapper_unregister('http');

			// Register the new HTTP wrapper
			stream_wrapper_register('http', 'GVGoldLinkNTLMStream') or die("Failed to register protocol");

			// Now, all requests to a http page will be done by GVGoldLinkNTLMStream.
			// Instantiate the client
			$GVGLclient = new GVGoldLinkNTLMSoapClient($url);

			//Gold-Vision Version
			$GVVersion = $GVGLclient->GetVersion()->{'GetVersionResult'};
			echo '<p>GV Version: '.$GVVersion.'</p>';

			// Restore the original HTTP stream wrapper
			stream_wrapper_restore('http');
		?>
	</body>
    </html>
	
.. note::

    A PHP example that interacts with the Gold-Link API can be found here: `PHP Example <https://github.com/GVThorne/GoldLinkAPI/tree/master/php_example>`_
	
**
C#
**

For this code example, I have used the **Add Web Reference** feature within Visual Studio. This then allows me to create a Data Access model that handles the authentication and method calls.

A model called **GVDataModel** will be created and it will contain the following structure:

.. code-block:: csharp

    public class GVDataModel
	{
		#region Enums
		
		#region Filters
		
		#region Fields
		
		private local.esteiro.goldlink gL;
		
		#region Constructors
		
		#region Private Methods
		
		#region Public Methods
	}
	
Enums
#####

This region is designed to contain various enumerators to make things easier when dealing with large amounts of data. The following is an example of an enumerator that could be used within Gold-Link.

.. code-block:: csharp

    public enum FilterType
	{
		Day = 0,
		Week = 1,
		None = 2
	}

Filters
#######

This region is designed to contain all of your Filter elements that will be used later within your Private and Public methods. The following is an example of a 'sortBy' filter that will either filter by CREATED_DATE or DUE_DATE. 

.. code-block:: csharp

    private XElement sortBy(SortType sortType)
	{
		switch (sortType)
		{
			case SortType.CreatedDate: return new XElement
			(
				"sort",
				new XAttribute[] 
			{ 
				new XAttribute("dbcolumn", "CREATED_DATE"),
				new XAttribute("order", "ascending") 
			}
			);
			case SortType.DueDate: return new XElement
			(
				"sort",
				new XAttribute[] 
			{ 
				new XAttribute("dbcolumn", "DUE_DATE"),
				new XAttribute("order", "ascending") 
			}
			);
			default: return new XElement
			(
				"sort",
				new XAttribute[] 
				{ 
					new XAttribute("dbcolumn", "DUE_DATE"),
					new XAttribute("order", "ascending") 
				}
			);
		}
	}
	
Fields
######

This region is designed to contain all of the fields that you wish to include when making certain requests such as :ref:`AddItem`.

.. code-block:: csharp

    private XElement Summary()
	{
		return new XElement
		(
			"field",
			new XAttribute[]
		{
			new XAttribute("dbcolumn", "SUMMARY"),
		}
		);
	}
	
Constructors
############

This is the most important part of your model. This is where the Gold-Link connection is constructed and where the authentication is made.

The following example is dependent on the Gold-Link URL, Gold-Link Domain, Gold-Link User and Gold-Link Password being set within your application's configuration file.

.. code-block:: csharp

    public GVDataModel()
	{
		this.gL = new mycompany.goldlink();
		this.gL.Url = Properties.Settings.Default.mycompany_goldlink;
		if (string.IsNullOrEmpty(Properties.Settings.Default.GoldLinkUser))
		{
			gL.UseDefaultCredentials = true;
		}
		else
		{
			this.gL.UseDefaultCredentials = false;
			NetworkCredential gLCred = new NetworkCredential();
			gLCred.UserName = Properties.Settings.Default.GoldLinkUser;
			gLCred.Domain = Properties.Settings.Default.GoldLinkDomain;
			gLCred.Password = Properties.Settings.Default.GoldLinkPassword;
			this.gL.Credentials = gLCred;
		}
	}

Private Methods
###############

This is where most of the actual Gold-Link requests will be made.

.. code-block:: csharp

    private List<Activity> getActivities(SortType sortType)
	{
		List<Activity> tActivities = new List<Activity>();

		//Results
		string result;
		bool success;

		//XML Filters
		XElement XmlFilters =
			new XElement
			(
				"filters",
				new Object[] 
			{ 
				new XAttribute("xmlns",""),
				sortBy(sortType),
				Summary()
			}
			);

		//Result
		XmlNode XmlResult = gL.FindItem(GoldLink.ObjectType.AccountActivity, CreateXmlNode(XmlFilters), out success, out result);
		XmlNode listElement = XmlResult.FirstChild;

		//Loop through returned Xml and store
		foreach (XmlElement child in listElement.ChildNodes)
		{
			tActivities.Add
			(
				new Activity
				(
					child.Attributes.GetNamedItem("id").Value,
					child.Attributes.GetNamedItem("summary").Value,
					DateTime.Parse(child.Attributes.GetNamedItem("due_date").Value)
				)
			);
		}
		return tActivities;
	}

Public Methods
##############

Finally, the Public Methods section will contain the list of methods available to call within your application.

.. code-block:: csharp

    public Dictionary<string, string[]> ActivtyReturn()
	{
		Dictionary<string, string[]> ActivityList = new Dictionary<string, string[]>();
		List<Activity> oActivity = new List<Activity>();

		try
		{
			oActivity = getActivities();
		}
		catch (Exception e)
		{

		}

		string[] activ = new string[] { };
		int i = 0;

		foreach (Activity oAct in oActivity)
		{
			activ[i] = oAct.summary;
			i++;
		}
		
		return ActivityList;
	}
	
