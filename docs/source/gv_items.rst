Gold-Vision Items
=================

.. _GVModelDiagram:

*************************
Gold-Vision Model Diagram
*************************

The diagram below helps you to gain a basic understanding of the structure for Gold-Vision items. So for example, if you were to create a new Contact in Gold-Vision, you can see that it is dependant on the Account item. Therefore, to create a new Contact, you either have to assign the contact to an existing Account or Create a new Account for the new Contact that is to be created. 

Core Items
##########

.. image:: images/GVModel.png
   :alt: Gold Vision Logo
   :align: center
   
Seminars
########
 
.. image:: images/SeminarModelGV.png
   :alt: Gold Vision Logo
   :align: center

*******
Account
*******
For the following example, I will be looking to create a new Account given that it does not exist already. The Account I wish to add is going to be called **Holdings Ltd**.

Finding the Account
###################

First of all I am going to make a Gold-Link request using :ref:`FindItem` to find out if I already have an account with the name **Holdings Ltd**. To do this, I will make the following request:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:FindItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:XmlFilters>
				<filters xmlns=""><filter dbcolumn="SUMMARY" value="Holdings Ltd" /></filters>
			 </gold:XmlFilters>
		  </gold:FindItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
This is the response:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <FindItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <FindItemResult>
				<gvdata xmlns="">
				   <list records="0"/>
				</gvdata>
			 </FindItemResult>
			 <success>true</success>
			 <message/>
		  </FindItemResponse>
	   </soap:Body>
	</soap:Envelope>
	
As you can see, the response has returned with a ``success`` result of true indicating the request was successful but also with a ``list`` attribute within the ``FindItemResult`` node. This ``list`` attribute indicates how many records have returned with a SUMMARY of **Holdings Ltd**.

From this result, it is apparent that there is no account with the name **Holdings Ltd** already in my Gold-Vision so I can then proceed to add the new account.

Updating an Account
###################

In the event that my :ref:`FindItem` request does return a result, you may decide that instead of creating a new account with the same name, you want to update the existing one instead. For example we may want to change ADDRESS_1 from **123 Old Street** to **321 New Street**.  For this situation the :ref:`FindItem` response will look something like this:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <FindItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <FindItemResult>
				<gvdata xmlns="">
				   <list records="1">
					  <record id="72f46715-49f6-453c-8c63-201e0358459e" type="Account" ac_id="72f46715-49f6-453c-8c63-201e0358459e" summary="Holdings Ltd"/>
				   </list>
				</gvdata>
			 </FindItemResult>
			 <success>true</success>
			 <message/>
		  </FindItemResponse>
	   </soap:Body>
	</soap:Envelope>
	
Using the ``record id`` from the response, we can use :ref:`GetItem` to return all the account information for **Holding Ltd**. The request will look like this:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:GetItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:id>72f46715-49f6-453c-8c63-201e0358459e</gold:id>
			 <gold:returnEmptyFields>false</gold:returnEmptyFields>
		  </gold:GetItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
with the resulting response showing as:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <GetItemResponse xmlns="http://service.gold-vision.com/gold-link">
			 <GetItemResult>
				<gvdata xmlns="">
				   <record objecttype="Account" id="72f46715-49f6-453c-8c63-201e0358459e">
					  <field name="AC_ID" readOnly="true">72f46715-49f6-453c-8c63-201e0358459e</field>
					  <field name="SUMMARY" label="Account Name" details="">Holdings Ltd</field>
					  <field name="ACG_ID" type="uid" label="Security" details="" id="78b6dbd2-8611-4e6d-9360-ddc40fe61066">Public</field>
					  <field name="AC_NUMBER" label="Account Number"></field>
					  <field name="AC_POTENTIAL" readOnly="true" label="Account Potential" type="numeric">0.00</field>
					  <field name="AC_SALES" readOnly="true" label="Account Sales" type="numeric">0.00</field>
					  <field name="AC_DISCOUNT" type="number" label="Discount">0.0E0</field>
					  <field name="NAME" label="Account Name">Holdings Ltd</field>
					  <field name="AC_FLAG" type="uid" label="Support Status" details="" mustHaveInsert="false" mustHaveUpdate="false" id="c2c40237-f662-4f3d-913f-81e482fa4ca6">NEW CUSTOMER</field>
					  <field name="US_ID_SALES" type="uid" label="Account Manager" details="" id="a0833573-314a-49a8-b52a-569980821d94">Gold-Vision Administrator</field>
					  <field name="US_ID_SUPPORT" type="uid" label="Support Manager" details="" id="">Not Assigned</field>
					  <field name="TYPE_1" type="uid" label="Esteiro Relationship" details="" mustHaveInsert="false" mustHaveUpdate="false" id="">Not Set</field>
					  <field name="TYPE_2" type="uid" label="Account Type 2" details="" id="">Not Set</field>
					  <field name="LABEL" type="uid" label="Account Type 3" id="">Not Set</field>
					  <field name="LEVEL" type="uid" label="Account Type 4" id="">Not Set</field>
					  <field name="ACC_ID_SALES" type="uid" label="Primary Contact" details="" id="12422155-e45c-4ee7-b5dc-228f004425cf">Joe Bloggs</field>
					  <field name="ACC_ID_SUPPORT" type="uid" label="Support Contact" id="">Not Assigned</field>
					  <field name="ADDRESS_1" label="Primary Address" details="" mustHaveInsert="false" mustHaveUpdate="false">123 Old Street</field>
					  <field name="TOWN" label="Town/City" details="" mustHaveInsert="false" mustHaveUpdate="false">London</field>
					  <field name="COUNTRY" label="Country" details="">United Kingdom</field>
					...
				   </record>
				</gvdata>
			 </GetItemResult>
			 <success>true</success>
			 <message/>
		  </GetItemResponse>
	   </soap:Body>
	</soap:Envelope>
	
As you can see, the resulting ``gvdata`` contains all the account information about **Holdings Ltd** including the ADDRESS_1 field of which has a value of **123 Old Street**.

To update this field to **321 New Street**, we are going to use the ADDRESS_1 field and include it in an :ref:`UpdateItem` request like below:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soap:Header/>
	   <soap:Body>
		  <gold:UpdateItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:xmlData>
				<gvdata xmlns="">
				<record><field name="ADDRESS_1">321 New Street</field></record>
				</gvdata>
			 </gold:xmlData>
			 <gold:id>72f46715-49f6-453c-8c63-201e0358459e</gold:id>
			 <gold:overwrite>AllFieldsPresent</gold:overwrite>
		  </gold:UpdateItem>
	   </soap:Body>
	</soap:Envelope>
	
This should return with a response in which ``success`` has resulted in **true**. You should now find that the ADDRESS_1 field has been updated from **123 Old Street** to **321 New Street**.

Creating a new Account
######################

In the event that you have made a :ref:`FindItem` request that was successful but returned 0 accounts with a SUMMARY of **Holding Ltd**, you may feel it is now safe to create a new Account with the same name. To do so, you would have to make an :ref:`AddItem` request as follows:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:AddItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:xmlData>
				<gvdata xmlns="">
				<record>
				<field name="SUMMARY">Holding Ltd</field>
				<field name="NAME">Holding Ltd</field>
				<field name="ADDRESS_1">321 New Street</field>
				<field name="TOWN">London</field>
				<field name="COUNTRY">United Kingdom</field>
				</record>
				</gvdata>
			 </gold:xmlData>
		  </gold:AddItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
This request will create a new Account that will also have data set for it's **Primary Address**, **City/Town** and **Country** fields.

As a result, the response will return with the Account ID of the newly created Account.

*******
Contact
*******

First of all, before we look to create a new contact we need to have a look at the :ref:`GVModelDiagram` at the top of this page. As we can see, A Contact record is dependant on an Account record. Therefore, to create a Contact in Gold-Vision via Gold-Link, we need to provide an **AC_ID** with it.

So the first thing to do would be to make a :ref:`FindItem` request to get an **AC_ID** of an Account. When creating a new Contact, this **AC_ID** is required to be included otherwise the request will fail. The following request is to add a **Joe Bloggs** to the **Holdings Ltd** Account.

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:AddItem>
			 <gold:objectType>Contact</gold:objectType>
			 <gold:xmlData>
				<gvdata xmlns="">
				<record>
					<field name="AC_ID">72f46715-49f6-453c-8c63-201e0358459e</field>
					<field name="FIRSTNAME">Joe</field>
					<field name="LASTNAME">Bloggs</field>
				</record>
				</gvdata>
			 </gold:xmlData>
		  </gold:AddItem>
	   </soapenv:Body>
	</soapenv:Envelope>

As a result, the ``returnId`` node will contain the new **ACC_ID** of the new Contact. 

***********
Opportunity
***********

To create an Opportunity, you are required to provide an **AC_ID** with the :ref:`AddItem` request. However, Opportunities, Activities, Projects, Quotes and Profiles allow you to attach a Contact from the related Account as well. However, this isn't essential and if no **ACC_ID** is provided, the Contact field will display as **Not Assigned**.

Therefore, the process for creating an Opportunity with a Contact assigned will require you to make two :ref:`FindItem` requests. The first will be to find the **AC_ID** of an Account and the second will be to find a Contact's **ACC_ID** that has that also has this **AC_ID**. An :ref:`AddItem` request can then be made to create an Opportunity with an **AC_ID** and an **ACC_ID**. The request will look like this:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:AddItem>
			 <gold:objectType>Opportunity</gold:objectType>
			 <gold:xmlData>
				<gvdata xmlns="">
				<record>
					<field name="AC_ID">72f46715-49f6-453c-8c63-201e0358459e</field>
					<field name="SUMMARY">Sales Op</field>
					<field name="ACC_ID">12422155-e45c-4ee7-b5dc-228f004425cf</field>
				</record>
				</gvdata>
			 </gold:xmlData>
		  </gold:AddItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
As a result, the ``returnId`` node will contain the new **OP_ID** of the new Opportunity.	
