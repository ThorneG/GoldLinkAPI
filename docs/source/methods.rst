Methods
=======

.. note::
    A full list of available methods can be found by accessing the web service URL e.g. https://example.goldvisioncrm.com/gold-link/goldlink.asmx.

*************	
Basic Methods
*************
	
.. _GetVersion:


GetVersion
##########

This method is used to get the version number of your Gold-Vision instance.

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
	
The ``<GetVersionResult>`` node has returned the Gold-Vision version number.

***************************
Finding, Listing, Get Items
***************************

.. _FindItem:

FindItem (List Items)
#####################

This method is used to return a list of records from Gold-Vision that match the **objectType**, **filter**, **field**, **rowlimit** and **sort** nodes provided.

**Request**

.. role:: red

.. role:: green

=============================================		========================================================
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		========================================================
:red:`objectType`	 	 							:ref:`ObjectType`
:green:`filter`										:green:`XML e.g. <filter dbcolumn="" value="" type=""></filter>`
:green:`rowlimit`									:green:`XML e.g. <rowlimit value=""></rowlimit>`
:green:`sort`										:green:`XML e.g. <sort dbcolumn="" order=""></sort>`
=============================================		========================================================


**Response**

==============	========
Attribute		Type
==============	========
FindItemResult	List
success			Boolean
message			String
==============	========

For a **FindItem** request, you will be required to send an ``objectType`` and ``filters`` node. The following nodes can be applied within ``filters`` to narrow down your **FindItem** result list.

**filter**

The filter node is can be used to search for a specific field value. For example the following request will search for all Accounts that have a SUMMARY of 'Gold-Vision'.  

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
	
**sort**

The sort node is used to apply a sorting criteria to the result set. For example, the following request will return all Accounts but in a descending order with regards to their SUMMARY value.

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:FindItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:XmlFilters>
			<filters xmlns=""><sort dbcolumn="SUMMARY" order="desc" /></sort>
			 </gold:XmlFilters>
		  </gold:FindItem>
	   </soapenv:Body>
	</soapenv:Envelope>
	
**rowlimit**

The rowlimit node is used to limit the amount of records returned in the response. For example, the following request will return only 2 Accounts from all the Accounts in Gold-Vision.

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:FindItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:XmlFilters>
			<filters xmlns=""><rowlimit value="2" /></rowlimit>
			 </gold:XmlFilters>
		  </gold:FindItem>
	   </soapenv:Body>
	</soapenv:Envelope>

The following request uses all 3 filtering nodes to return 2 Accounts that begin with the letter 'B' and have been sorted in an alphabetically order.

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:FindItem>
			 <gold:objectType>Account</gold:objectType>
			 <gold:XmlFilters>
			<filters xmlns="">
			 <filter dbcolumn="SUMMARY" value="G"></filter>
			 <sort dbcolumn="SUMMARY" order="asc"></sort>
			 <rowlimit value="3"></rowlimit>
			</filters>
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
				   <list records="3">
					  <record id="4f219888-55c6-405a-95be-60281c14778e" type="Account" ac_id="4f219888-55c6-405a-95be-60281c14778e" summary="General Sales"/>
					  <record id="b1c966b1-cc83-4594-a68c-c4e6522a5107" type="Account" ac_id="b1c966b1-cc83-4594-a68c-c4e6522a5107" summary="Gold-Vision"/>
					  <record id="f0da84dc-2a56-40c0-80a2-2960fff69fe2" type="Account" ac_id="f0da84dc-2a56-40c0-80a2-2960fff69fe2" summary="Goldware"/>
				   </list>
				</gvdata>
			 </FindItemResult>
			 <success>true</success>
			 <message/>
		  </FindItemResponse>
	   </soap:Body>
	</soap:Envelope>

.. _GetItem:

GetItem
#######

This method is used to get all of the information for a particular record.

**Request**

=============================================		==================================================
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		==================================================
:red:`objectType`				 					 :ref:`ObjectType`
:red:`id`											:red:`String`
:red:`returnEmptyFields`							:red:`Boolean`
=============================================		==================================================

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

.. _AddUpdateDelete:
	
*****************
Add/Update/Delete
*****************

.. _AddItem:

AddItem
#######

This method is used to add a new record into Gold-Vision.

**Request**

=============================================	==================================================
Attribute (:red:`Required`/:green:`Optional`)	Type
=============================================	==================================================
:red:`objectType`	 							 :ref:`ObjectType`
:red:`xmlData`									:red:`XML`
=============================================	==================================================

**Response**

==============		=========
Attribute			Type
==============		=========
AddItemResult		Boolean
returnId			String
success				Boolean
message				String
==============		=========

To add a new item in Gold-Vision, you are required to make a request with an ``objectType`` and ``xmlData`` node. The ``xmlData`` node is to contain data for each field related to your new item that you are adding.

This request will add a new Account into Gold-Vision with a SUMMARY value of 'Esteiro':

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

UpdateItem
##########

This method is used to update an existing record in Gold-Vision.

**Request**

=============================================	========================================================================================================
Attribute (:red:`Required`/:green:`Optional`)	Type
=============================================	========================================================================================================
:red:`objectType`	 							 :ref:`ObjectType`
:red:`xmlData`									:red:`XML`
:red:`id`										:red:`String`
:red:`overwrite`								:red:`AllFieldsPresent or AllFieldsPresentExceptBlanks or AllFieldsPresentExceptBlanksWhereTargetEmpty`
=============================================	========================================================================================================

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

.. _GetObjectDef:

GetObjectDef
############

This method is useful when you want to get a list of possible fields available, when looking to create a new record in Gold-Vision.

**Request**

=============================================	==================================================
Attribute (:red:`Required`/:green:`Optional`)	Type
=============================================	==================================================
:red:`objectType`	 							 :ref:`ObjectType`
=============================================	==================================================

**Response**

==================		========
Attribute				Type
==================		========
GetObjectDefResult		XML
success					Boolean
message					String
==================		========

The GetObjectDef request only requires you to include the ``objectType`` node with the request. From this, a response will be returned that includes ObjectDef information related to the value included in ``objectType`` such as field names and field labels.

This request will return the ObjectDef information of an Account item:

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

Just like :ref:`FindItem`, a ``success`` node is returned along with the ``record`` node to indicate if the request is successful or not.

GetDropOptions
##############

This method is useful when getting a list of the available dropdown values for a dropdown field.

=============================================		==================
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		==================
:red:`objectType`			 						 :ref:`ObjectType`
:red:`fieldName`									:red:`String`
=============================================		==================

**Response**

====================	========
Attribute				Type
====================	========
GetDropOptionsResult	List
success					Boolean
message					String
====================	========

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:GetDropOptions>
			 <gold:objectType>Account</gold:objectType>
			 <gold:fieldName>AC_FLAG</gold:fieldName>
		  </gold:GetDropOptions>
	   </soapenv:Body>
	</soapenv:Envelope>
	
This request will return the following response that contains all the available values for the field **AC_FLAG** which is labelled as **Support Status** by default.

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <GetDropOptionsResponse xmlns="http://service.gold-vision.com/gold-link">
			 <GetDropOptionsResult>
				<drop xmlns="">
				   <row value="" text="Not Set" hlight=""/>
				   <row value="cf834a75-3223-45ef-b555-50331109a950" text="ACTIVE SUPPORT" hlight=""/>
				   <row value="c2c40237-f662-4f3d-913f-81e482fa4ca6" text="NEW CUSTOMER" hlight=""/>
				   <row value="cf1fea76-00a2-4e54-b5ac-eaf80e6d3f64" text="RESELLER - 2ND LINE SUPPORT" hlight=""/>
				   <row value="dbd76c91-baed-4011-b449-0fb2dbc0135a" text="HOLD" hlight=""/>
				   <row value="ac425e3c-7d3d-4c69-8256-eef47e9cf60c" text="UNSUPPORTED" hlight=""/>
				</drop>
			 </GetDropOptionsResult>
			 <success>true</success>
			 <message/>
		  </GetDropOptionsResponse>
	   </soap:Body>
	</soap:Envelope>

If making an :ref:`AddUpdateDelete` request to set a dropdown field such as **AC_FLAG/Support Status**, you would have to use the relevant GUID ID from the dataset returned from the **GetDropOptions** request.

	
DeleteItem
##########

This method is used to delete records in Gold-Vision.

=============================================		==================
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		==================
:red:`objectType`			 						 :ref:`ObjectType`
:red:`id`											:red:`String`
=============================================		==================

**Response**

================		========
Attribute				Type
================		========
DeleteItemResult		Boolean
success					Boolean
message					String
================		========

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:DeleteItem>
			 <gold:objectType>Contact</gold:objectType>
			 <gold:id>b3cc266e-4e98-4f6e-aee3-5b6915ee62a3</gold:id>
		  </gold:DeleteItem>
	   </soapenv:Body>
	</soapenv:Envelope>

********************
Phone System Methods
********************

LogCall
########

This method is used to log incoming and outgoing telephone calls within Gold-Vision.

=============================================		===============
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		===============
:red:`accountId`									:red:`String`
:green:`contactId`									:green:`String`
:green:`number`										:green:`String`
:red:`inbound`										:red:`Boolean`
=============================================		===============

**Response**

================		========
Attribute				Type
================		========
LogCallResult			Boolean
success					Boolean
message					String
================		========

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:LogCall>
			 <gold:accountId>71fb89cb-92ad-4973-8293-d43f1cd98673</gold:accountId>
			 <gold:contactId>ca194711-f378-48c4-88f2-b8ae22207091</gold:contactId>
			 <gold:number>01234 567890</gold:number>
			 <gold:inbound>true</gold:inbound>
		  </gold:LogCall>
	   </soapenv:Body>
	</soapenv:Envelope>

This request will return a result with a ``success`` node and a ``message`` node. If ``success`` appears as 'false', the ``message`` node will display the error that caused the request to fail.

.. note::

    It is possible to send this request without a ``contactId`` value. By leaving this node empty, a telephone call will be entered into Gold-Vision against the given Account rather than against a Contact.
	
LogCallwithDuration
###################

This method is used to log incoming and outgoing telephone calls with a duration value in Gold-Vision.

=============================================	===============
Attribute (:red:`Required`/:green:`Optional`)	Type
=============================================	===============
:red:`accountId`								:red:`String`
:green:`contactId`								:green:`String`
:green:`number`									:green:`String`
:red:`inbound`									:red:`Boolean`
:red:`duration`									:red:`Integer`
=============================================	===============

**Response**

=========================	========
Attribute					Type
=========================	========
LogCallwithDurationResult	Boolean
success						Boolean
message						String
=========================	========

This is what a **LogCallWithDuration** request will look like:

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:LogCallwithDuration>
			 <gold:accountId>71fb89cb-92ad-4973-8293-d43f1cd98673</gold:accountId>
			 <gold:contactId>ca194711-f378-48c4-88f2-b8ae22207091</gold:contactId>
			 <gold:number>01234 567890</gold:number>
			 <gold:inbound>true</gold:inbound>
			 <gold:duration>3</gold:duration>
		  </gold:LogCallwithDuration>
	   </soapenv:Body>
	</soapenv:Envelope>
	
This request adds an inbound telephone call against the Contact **Joe Bloggs** and Account **Holding Ltd** as well as giving the record a duration value of **3**.

LookupPhoneNumber
#################

This method is useful when looking to return all matching Contacts and Accounts with the input of a telephone number.

=============================================		==============
Attribute (:red:`Required`/:green:`Optional`)		Type
=============================================		==============
:red:`number`										:red:`String`
=============================================		==============

**Response**

=======================		========
Attribute					Type
=======================		========
LookupPhoneNumberResult		Boolean
success						Boolean
message						String
=======================		========

.. code-block:: html

    <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:gold="http://service.gold-vision.com/gold-link">
	   <soapenv:Header/>
	   <soapenv:Body>
		  <gold:LookupPhoneNumber>
			 <gold:number>01234 567890</gold:number>
		  </gold:LookupPhoneNumber>
	   </soapenv:Body>
	</soapenv:Envelope>
	
The response will return a ``list`` node that will contain both ``account`` and ``contact`` records if any match the telephone number sent with the original request. This is the sort of response that you are likely to receive:

.. code-block:: html

    <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	   <soap:Body>
		  <LookupPhoneNumberResponse xmlns="http://service.gold-vision.com/gold-link">
			 <LookupPhoneNumberResult>
				<gvdata xmlns="">
				   <list>
					  <account id="71fb89cb-92ad-4973-8293-d43f1cd98673">
						 <ac_name>Holding Ltd</ac_name>
						 <ac_id>71fb89cb-92ad-4973-8293-d43f1cd98673</ac_id>
						 <ac_phone/>
						 <ac_link>http://gvsandbox01/Gold-VisionThorne/goldvision.aspx?page=popthru&amp;killwindow=1&amp;action=OpenAccount&amp;actiondata=71fb89cb-92ad-4973-8293-d43f1cd98673</ac_link>
						 <contacts>
							<contact id="ca194711-f378-48c4-88f2-b8ae22207091">
							   <acc_name>Joe Bloggs</acc_name>
							   <acc_id>ca194711-f378-48c4-88f2-b8ae22207091</acc_id>
							   <acc_phone>01234 567890</acc_phone>
							   <acc_mobile/>
							   <acc_link>http://gvsandbox01/Gold-VisionThorne/goldvision.aspx?page=popthru&amp;killwindow=1&amp;action=OpenContact&amp;actiondata=ca194711-f378-48c4-88f2-b8ae22207091</acc_link>
							   <acc_match>true</acc_match>
							</contact>
						 </contacts>
					  </account>
				   </list>
				</gvdata>
			 </LookupPhoneNumberResult>
			 <success>true</success>
			 <message/>
		  </LookupPhoneNumberResponse>
	   </soap:Body>
	</soap:Envelope>
    