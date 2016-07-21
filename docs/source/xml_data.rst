.. _Xml:

XML
===

The structure of XML nodes within Gold-Link method calls is as follows:

.. code-block:: html

    <gvdata xmlns="">
      <record>
        <field name=""> </field>
      </record>
    </gvdata>
	
.. note::

    Using :ref:`GetObjectDef` will allow you to see the available XML nodes for a specific Gold-Vision object.
	
For example, here are the XML nodes available for an **Account**:

.. code-block:: html

    <gvdata xmlns="">
	   <record>
		  <field name="AC_ID"></field>
		  <field name="SUMMARY"></field>
		  <field name="ACG_ID"></field>
		  <field name="AC_NUMBER"></field>
		  <field name="AC_POTENTIAL"></field>
		  <field name="AC_SALES"></field>
		  <field name="AC_DISCOUNT"></field>
		  <field name="NAME"></field>
		  <field name="AC_FLAG"></field>
		  <field name="US_ID_SALES"></field>
		  <field name="US_ID_SUPPORT"></field>
		  <field name="TYPE_1">/field>
		  <field name="TYPE_2"></field>
		  <field name="LABEL"></field>
		  <field name="LEVEL"></field>
		  <field name="SITE"></field>
		  <field name="ACC_ID_SALES"></field>
		  <field name="ACC_ID_SUPPORT"></field>
		  <field name="ADDRESS_1"></field>
		  <field name="ADDRESS_2"></field>
		  <field name="ADDRESS_3"></field>
		  <field name="TOWN"></field>
		  <field name="COUNTY"></field>
		  <field name="POSTCODE"></field>
		  <field name="COUNTRY"></field>
		  <field name="BILLING_ADDRESS_1"></field>
		  <field name="BILLING_ADDRESS_2"></field>
		  <field name="BILLING_ADDRESS_3"></field>
		  <field name="BILLING_TOWN"></field>
		  <field name="BILLING_COUNTY"></field>
		  <field name="BILLING_POSTCODE"></field>
		  <field name="BILLING_COUNTRY"></field>
		  <field name="PHONE_1"></field>
		  <field name="PHONE_2"></field>
		  <field name="PHONE_3"></field>
		  <field name="FAX_1"></field>
		  <field name="FAX_1_FORMATTED"></field>
		  <field name="FAX_2"></field>
		  <field name="FAX_2_FORMATTED"></field>
		  <field name="FAX_3"></field>
		  <field name="FAX_3_FORMATTED"></field>
		  <field name="WEB_SITE_1"></field>
		  <field name="WEB_SITE_2"></field>
		  <field name="SOURCE"></field>
		  <field name="INDUSTRY"></field>
		  <field name="NUMBER_EMPLOYEES"></field>
		  <field name="DETAILS"></field>
		  <field name="CREATED_DATE"></field>
		  <field name="CREATED_BY"></field>
		  <field name="UPDATED_DATE"></field>
		  <field name="UPDATED_BY"></field>
		  <field name="CREATED_INFO"></field>
		  <field name="OP_OPEN"></field>
		  <field name="REFERENCE"></field>
		  <field name="REFERENCE_SEED"></field>
		  <field name="TAGS"></field
		  <field name="SECURITY"></field>
		  <field name="EMAIL_DOMAINS"></field>
		  <field name="AC_IMPORT"></field>
		  <field name="AC_UD1"></field>
		  <field name="AC_UD2"></field>
		  <field name="AC_UD3"></field>
		  <field name="AC_UD4"></field>
		  <field name="AC_UD5"></field>
		  <field name="AC_UD6"></field>
		  <field name="AC_UD7"></field>
		  <field name="AC_UD8"></field>
		  <field name="AC_UD9"></field>
		  <field name="AC_UD10"></field>
		  <field name="AC_UD11"></field>
		  <field name="AC_UD12"></field>
		  <field name="AC_UD13"></field>
		  <field name="AC_UD14"></field>
		  <field name="AC_UD15"></field>
		  <field name="AC_UD1_ID"></field>
		  <field name="AC_UD2_ID"></field>
		  <field name="AC_UD3_ID"></field>
		  <field name="AC_UD4_ID"></field>
		  <field name="AC_UD5_ID"></field>
		  <field name="AC_UD6_ID"></field>
		  <field name="AC_UD7_ID"></field>
		  <field name="AC_UD8_ID"></field>
		  <field name="AC_UD9_ID"></field>
		  <field name="AC_UD10_ID"></field>
		  <field name="AC_UD1_DATE"></field>
		  <field name="AC_UD2_DATE"></field>
		  <field name="AC_UD3_DATE"></field>
		  <field name="AC_UD4_DATE"></field>
		  <field name="AC_UD5_DATE"></field>
		  <field name="AC_UD6_DATE"></field>
		  <field name="AC_UD7_DATE"></field>
		  <field name="AC_UD8_DATE"></field>
		  <field name="AC_UD9_DATE"></field>
		  <field name="AC_UD10_DATE"></field>
		  <field name="AC_UD1_BIT"></field>
		  <field name="AC_UD2_BIT"></field>
		  <field name="AC_UD3_BIT"></field>
		  <field name="AC_UD4_BIT"></field>
		  <field name="AC_UD5_BIT"></field>
		  <field name="AC_UD6_BIT"></field>
		  <field name="AC_UD7_BIT"></field>
		  <field name="AC_UD8_BIT"></field>
		  <field name="AC_UD9_BIT"></field>
		  <field name="AC_UD10_BIT"></field>
		  <field name="AC_UD11_BIT"></field>
		  <field name="AC_UD12_BIT"></field>
		  <field name="AC_UD13_BIT"></field>
		  <field name="AC_UD14_BIT"></field>
		  <field name="AC_UD15_BIT"></field>
		  <field name="AC_UD16_BIT"></field>
		  <field name="AC_UD17_BIT"></field>
		  <field name="AC_UD18_BIT"></field>
		  <field name="AC_UD19_BIT"></field>
		  <field name="AC_UD20_BIT"></field>
		  <field name="AC_UD21_BIT"></field>
		  <field name="AC_UD22_BIT"></field>
		  <field name="AC_UD23_BIT"></field>
		  <field name="AC_UD24_BIT"></field>
		  <field name="AC_UD1_NUMERIC"></field>
		  <field name="AC_UD2_NUMERIC"></field>
		  <field name="AC_UD3_NUMERIC"></field>
		  <field name="AC_UD4_NUMERIC"></field>
		  <field name="AC_UD5_NUMERIC"></field>
		  <field name="AC_UD6_NUMERIC"></field>
		  <field name="AC_UD7_NUMERIC"></field>
		  <field name="AC_UD8_NUMERIC"></field>
		  <field name="AC_UD9_NUMERIC"></field>
		  <field name="AC_UD10_NUMERIC"></field>
		  <field name="AC_EXTERNAL"></field>
		  <field name="AC_DORMANT"></field>
		  <field name="VALIDATIONMESSAGE"></field>
		  <field name="NEW_CONTACT"></field>
		  <field name="ACC_FULLNAME"></field>
		  <field name="ACC_FIRSTNAME"></field>
		  <field name="ACC_LASTNAME"></field>
		  <field name="ACC_TITLE"></field>
		  <field name="ACC_JOBTITLE"></field>
		  <field name="ACC_DEPARTMENT"></field>
		  <field name="ACC_BUSINESSTELEPHONENUMBER"></field>
		  <field name="ACC_EMAIL1ADDRESS"></field>
		  <field name="ACC_BUSINESSFAXNUMBER"></field>
		  <field name="OWNER_EMAIL"></field>
		  <field name="ACC_MANAGER"></field>
		  <field name="ACC_MIDDLENAME"></field>
		  <field name="ACC_EMAIL2ADDRESS"></field>
		  <field name="ACC_EMAIL3ADDRESS"></field>
		  <field name="ACC_HOMETELEPHONENUMBER"></field>
		  <field name="ACC_HOMEFAXNUMBER"></field>
		  <field name="ACC_HOMEADDRESSSTREET"></field>
		  <field name="ACC_HOMEADDRESSSTREET2"></field>
		  <field name="ACC_HOMEADDRESSSTREET3"></field>
		  <field name="ACC_HOMEADDRESSCITY"></field>
		  <field name="ACC_HOMEADDRESSSTATE"></field>
		  <field name="ACC_HOMEADDRESSPOSTALCODE"></field>
		  <field name="ACC_HOMEADDRESSCOUNTRY"></field>
		  <field name="ACC_BUSINESSADDRESSSTREET"></field>
		  <field name="ACC_BUSINESSADDRESSSTREET2"></field>
		  <field name="ACC_BUSINESSADDRESSSTREET3"></field>
		  <field name="ACC_BUSINESSADDRESSCITY"></field>
		  <field name="ACC_BUSINESSADDRESSSTATE"></field>
		  <field name="ACC_BUSINESSADDRESSPOSTALCODE"></field>
		  <field name="ACC_BUSINESSADDRESSCOUNTRY"></field>
		  <field name="AC_MANAGER" readOnly="true"></field>
		  <field name="NAME_SOUNDEX"></field>
		  <field name="NAME_LONGEST_WORD"></field>
		  <field name="USER_NAME"></field>
		  <field name="USERJOBTITLE"></field>
		  <field name="USERDIRECTPHONE"></field>
		  <field name="ISINTEGRATED"></field>
		  <field name="ISADMIN"></field>
		  <field name="ISOWNER"></field>
		  <field name="ISTEAM"></field>
		  <field name="TP_SCORE"></field>
		  <field name="TP_DATE"></field>
		  <field name="LINKEDIN_PUBLIC_ID"></field>
		  <field name="LINKEDIN_PRIVATE_ID"></field>
		  <field name="LINKEDIN_PROFILE_URL"></field>
		  <field name="LINKEDIN_IMAGE"></field>
		  <field name="LINKEDIN_NAME"></field>
		  <field name="FACEBOOK_PUBLIC_ID"></field>
		  <field name="FACEBOOK_PRIVATE_ID"></field>
		  <field name="FACEBOOK_PROFILE_URL"></field>
		  <field name="FACEBOOK_IMAGE"></field>
		  <field name="FACEBOOK_NAME"></field>
		  <field name="GPLUS_PUBLIC_ID"></field>
		  <field name="GPLUS_PRIVATE_ID"></field>
		  <field name="GPLUS_PROFILE_URL"></field>
		  <field name="GPLUS_IMAGE"></field>
		  <field name="GPLUS_NAME"></field>
		  <field name="TWITTER1_PUBLIC_ID"></field>
		  <field name="TWITTER1_PRIVATE_ID"></field>
		  <field name="TWITTER1_PROFILE_URL"></field>
		  <field name="TWITTER1_IMAGE"></field>
		  <field name="TWITTER1_NAME"></field>
		  <field name="TWITTER2_PUBLIC_ID"></field>
		  <field name="TWITTER2_PRIVATE_ID"></field>
		  <field name="TWITTER2_PROFILE_URL"></field>
		  <field name="TWITTER2_IMAGE"></field>
		  <field name="TWITTER2_NAME"></field>
		  <field name="TWITTER3_PUBLIC_ID"></field>
		  <field name="TWITTER3_PRIVATE_ID"></field>
		  <field name="TWITTER3_PROFILE_URL"></field>
		  <field name="TWITTER3_IMAGE"></field>
		  <field name="TWITTER3_NAME"></field>
		  <field name="TWITTER4_PUBLIC_ID"></field>
		  <field name="TWITTER4_PRIVATE_ID"></field>
		  <field name="TWITTER4_PROFILE_URL"></field>
		  <field name="TWITTER4_IMAGE"></field>
		  <field name="TWITTER4_NAME"></field>
		  <field name="TWITTER5_PUBLIC_ID"></field>
		  <field name="TWITTER5_PRIVATE_ID"></field>
		  <field name="TWITTER5_PROFILE_URL"></field>
		  <field name="TWITTER5_IMAGE"></field>
		  <field name="TWITTER5_NAME"></field>
		  <field name="LEAD_SUMMARY"></field>
		  <field name="LEAD_LIST_SUMMARY"></field>
		  <field name="CS_ID"></field>
		  <field name="LC_ID"></field>
	   </record>
    </gvdata>