Methods
=======
:ref:`FindItem`, :ref:`GetObjectDef`, :ref:`AddItem`, :ref:`UpdateItem`, :ref:`GetItem` are the fundamental methods used with Gold-Link.

.. note::
    A full list of available methods can be found by accessing the web service URL e.g. https://example.goldvisioncrm.com/gold-link/goldlink.asmx.

.. _GetVersion:

**********
GetVersion
**********

**Request**

=======================		=========
Attribute					Type
=======================		=========
Empty						N/A
=======================		=========

**Response**

================	========
Attribute			Type
================	========
GetVersionResult	String
================	========

No parameters are required to make a **GetVersion** request. For example, the following request:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:GetVersion/>
	   </soapenv:Body>
	</soapenv:Envelope>
	
will return with the following response:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <GetVersionResponse xmlns="http://service.gold-vision.com/gold-link">
			 <GetVersionResult>7.0.18.17056</GetVersionResult>
		  </GetVersionResponse>
	   </soap:Body>
	</soap:Envelope>
	
As you can see, within the ``<GetVersionResult>`` node, the Gold-Vision version number has been returned.

.. _FindItem:

********
FindItem
********

**Request**

==========	==================================================
Attribute	Type
==========	==================================================
objectType	Account or Contact or AccountActivity or Quote ...
filters		XML
==========	==================================================

**Response**

==============	========
Attribute		Type
==============	========
FindItemResult	XML
success			Boolean
message			String
==============	========

For a **FindItem** request, you will be required to send an ``objectType`` and ``filters`` node.  

For this example, I will be looking to return all accounts that have a SUMMARY value of 'Gold-Vision'. This is the request that will be sent:

.. code-block:: html
    
	<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:FindItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:XmlFilters>
			<filters xmlns=""><filter dbcolumn="SUMMARY" value="Gold-Vision" /></filters>
			 </gold:XmlFilters>
		  </gold:FindItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	

Here is the response:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <FindItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <FindItemResult>
				<gvdata xmlns="">
				   <list records="1">
					  <record id="b1c966b1-cc83-4594-a68c-c4e6522a5107" type="Account" ac_id="b1c966b1-cc83-4594-a68c-c4e6522a5107" summary="Gold-Vision" />
				   </list>
				</gvdata>
			 </FindItemResult>
			 <success>true</success>
			 <message/>
		  </FindItemResponse>
	   </soap:Body>
	</soap:Envelope>

As you can see, a single record has been returned with a SUMMARY of 'Gold-Vision'. As well as this, another node ``success`` has been returned to indicate whether the request originally sent was successful or not.

.. note::

   * If you were looking to include more fields for each record returned, simply add a **<field>** node within ``filters``. For example, to include **CREATED_DATE** within the results returned above, the ``filters`` node will look like ``<filters xmlns=""><filter dbcolumn="SUMMARY" value="Gold-Vision" /><field dbcolumn="CREATED_DATE" /></filters>``.
   
   * By having neither **<field>** nor **<filters>** within ``filters``, the result list will include all Accounts.

.. _GetObjectDef:

************
GetObjectDef
************

**Request**

==========	==================================================
Attribute	Type
==========	==================================================
objectType	Account or Contact or AccountActivity or Quote ...
==========	==================================================

**Response**

==================		========
Attribute				Type
==================		========
GetObjectDefResult		XML
success					Boolean
message					String
==================		========

The GetObjectDef request only requires you to include the ``objectType`` node with the request. From this, you will be returned with a response that includes ObjectDef information related to the value included in ``objectType`` such as field names and field labels.

For example, to find more information about the Account object, the following request can be made:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:GetObjectDef>
			 <gold:objectType>Account</gold:objectType>
		  </gold:GetObjectDef>
	   </soapenv:Body>
	</soapenv:Envelope>
	
Here is a preview of the response that will be returned:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <GetObjectDefResponse xmlns="http://service.gold-vision.com/gold-link">
			 <GetObjectDefResult>
				<record compatibility="6" queryCommand="spGetAccount" updateCommand="spUpdateAccount" insertCommand="spInsertAccount" deleteCommand="spDeleteAccount" undeleteCommand="spUnDeleteAccount" dormantCommand="spDormantAccount" unDormantCommand="spUnDormantAccount" openby="" opendate="" id="" xmlns="">
				   <field name="AC_ID" primarykey="true" readOnly="true" location="" colspan=""/>
				   <field name="SUMMARY" ui="true" label="Account Name" labelref="[%ACCOUNTS] Name" templatetag="account" integtype="text" icon="template" details="" editincludesecondaryteam="false" geocode="false" location="s1r1c1" colspan="2"/>
				   <field name="ACG_ID" ui="true" type="uid" dropdown="spGetDrop AC_ACCESS" label="Security" labelref="Security" details="" editincludesecondaryteam="false" geocode="false" location="s2r9c3" colspan="2"/>
				   <field name="AC_NUMBER" label="Account Number" labelref="[%ACCOUNTS] Number" location="" colspan=""/>
				   <field name="AC_POTENTIAL" readOnly="true" ui="true" label="Account Potential" labelref="[%ACCOUNTS] Potential" type="numeric" integtype="numeric" location="" colspan=""/>
				   <field name="AC_SALES" readOnly="true" ui="true" label="Account Sales" labelref="[%ACCOUNTS] Sales" type="numeric" integtype="numeric" location="" colspan=""/>
				   <field name="AC_DISCOUNT" templatetag="ac_discount" ui="true" dropdown="spGetDropDiscount" type="number" label="Discount" integtype="numeric" location="" colspan=""/>
				   <field name="NAME" label="Account Name" labelref="[%ACCOUNTS] Name" templatetag="account" integtype="text" location="" colspan=""/>
				   <field name="AC_FLAG" templatetag="ac_flag" ui="true" type="uid" dropdown="spGetDrop AC_FLAG" label="Support Status" integtype="text" details="" editincludesecondaryteam="false" geocode="false" mustHaveInsert="false" mustHaveUpdate="false" editableUI="0" dro="AC_FLAG" location="s1r4c3" colspan="2"/>
				   <field name="US_ID_SALES" templatetag="ac_manager" ui="true" type="uid" dropdown="spDropDownSalesUsers 'SALES'" label="Account Manager" labelref="[%ACCOUNTS] Manager" owner="true" integtype="text" icon="email:OWNER_EMAIL" link="OpenUser:US_ID_SALES" details="" editincludesecondaryteam="false" geocode="false" location="s1r4c1" colspan="2"/>
				   ...
				</record>
			 </GetObjectDefResult>
			 <success>true</success>
			 <message/>
		  </GetObjectDefResponse>
	   </soap:Body>
    </soap:Envelope>

Again, just like :ref:`FindItem`, a ``success`` node is returned along with the ``record`` node to inform you if the request is successful or not.
	
.. _AddItem:

*******
AddItem
*******

**Request**

==========	==================================================
Attribute	Type
==========	==================================================
objectType	Account or Contact or AccountActivity or Quote ...
xmlData		XML
==========	==================================================

**Response**

==============		=========
Attribute			Type
==============		=========
AddItemResult		Boolean
returnId			String
success				Boolean
message				String
==============		=========

An **AddItem** request is used to add new items such as Accounts to Gold-Vision. To add a new item in Gold-Vision, you are required to make a request with an ``objectType`` and ``xmlData`` node. The ``xmlData`` node is to contain data for each field related to your new item that you are adding.

For this example, the following request will add a new Account into Gold-Vision with the SUMMARY field set to have a value of 'Esteiro':

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:AddItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:xmlData>
			 <gvdata xmlns="">
				<record><field name="SUMMARY">Esteiro</field></record>
			</gvdata>
			 </gold:xmlData>
		  </gold:AddItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
This request will return a response of:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <AddItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <AddItemResult>true</AddItemResult>
			 <returnId>09b54b7a-2de1-46da-8b0f-b42debe9f2ba</returnId>
			 <success>true</success>
			 <message/>
		  </AddItemResponse>
	   </soap:Body>
	</soap:Envelope>
	
If successful, the response will return the new item ID under ``returnId``. The above example will have created a new Account with just a SUMMARY value and nothing else. To create a new Account with more data, you will be required to nest the relevant ``field`` nodes within the ``record`` node.

.. _UpdateItem:

**********
UpdateItem
**********

**Request**

==========	================================================================================================
Attribute	Type
==========	================================================================================================
objectType	Account or Contact or AccountActivity or Quote ...
xmlData		XML
id			String
overwrite	AllFieldsPresent or AllFieldsPresentExceptBlanks or AllFieldsPresentExceptBlanksWhereTargetEmpty
==========	================================================================================================

**Response**

================	=========
Attribute			Type
================	=========
UpdateItemResult	Boolean
success				Boolean
message				String
================	=========

To make a request using **UpdateItem**, you will be required to make a request with an ``objectType``, ``xmlData``, ``id`` and ``overwrite`` node. The ``overwrite`` node can either have a value of **AllFieldsPresent**, **AllFieldsPresentExceptBlanks** or **AllFieldsPresentExceptBlanksWhereTargetEmpty**.

The following request is to update the SUMMARY field to have a value of 'Esteiro' for an Account with the given ID. The following value given for the ``overwrite`` node will overwrite the existing data even if it is blank.

.. code-block:: html
    
    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soap:Header/>
	   <soap:Body>
		  <gold:UpdateItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:xmlData>
			 <gvdata xmlns="">
				<record><field name="SUMMARY">Esteiro</field></record>
			</gvdata>
			 </gold:xmlData>
			 <gold:id>b1c966b1-cc83-4594-a68c-c4e6522a5107</gold:id>
			 <gold:overwrite>AllFieldsPresent</gold:overwrite>
		  </gold:UpdateItem>
	   </soap:Body>
	</soap:Envelope>
	
This request will return with a response of:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <UpdateItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <UpdateItemResult>true</UpdateItemResult>
			 <success>true</success>
			 <message/>
		  </UpdateItemResponse>
	   </soap:Body>
	</soap:Envelope>
	
This response has indicated that the update has been successful.

.. _GetItem:

*******
GetItem
*******

**Request**

==================		==================================================
Attribute				Type
==================		==================================================
objectType				Account or Contact or AccountActivity or Quote ...
id						String
returnEmptyFields		Boolean
==================		==================================================

**Response**

==============		========
Attribute			Type
==============		========
GetItemResult		XML
success				Boolean
message				String
==============		========

To make a request using **GetItem**, you will be required to make a request with an ``objectType``, ``id`` and ``returnEmptyFields`` node. The ``returnEmptyFields`` node will accept a value of either **true** (1) or **false** (0). 

The following request:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:GetItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:id>b1c966b1-cc83-4594-a68c-c4e6522a5107</gold:id>
			 <gold:returnEmptyFields>false</gold:returnEmptyFields>
		  </gold:GetItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
will return a response of:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <GetItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <GetItemResult>
				<gvdata xmlns="">
				   <record objecttype="Account" id="b1c966b1-cc83-4594-a68c-c4e6522a5107">
					  <field name="AC_ID" readOnly="true">b1c966b1-cc83-4594-a68c-c4e6522a5107</field>
					  <field name="SUMMARY" label="Account Name" details="">Gold-Vision</field>
					  <field name="ACG_ID" type="uid" label="Security" details="" id="78b6dbd2-8611-4e6d-9360-ddc40fe61066">Public</field>
					  <field name="AC_NUMBER" label="Account Number"></field>
					  <field name="AC_POTENTIAL" readOnly="true" label="Account Potential" type="numeric">70,425.00</field>
					  <field name="AC_SALES" readOnly="true" label="Account Sales" type="numeric">0.00</field>
					  <field name="AC_DISCOUNT" type="number" label="Discount">0.0E0</field>
					  <field name="NAME" label="Account Name">Gold-Vision</field>
					  ...
					  ...
					</record>
				</gvdata>
			 </GetItemResult>
			 <success>true</success>
			 <message/>
		  </GetItemResponse>
	   </soap:Body>
	</soap:Envelope>