Mule Magento Cloud Connector
============================

Mule Cloud connector to Magento

Installation
------------

The connector can either be installed for all applications running within the Mule instance or can be setup to be used
for a single application.

*All Applications*

Download the connector from the link above and place the resulting jar file in
/lib/user directory of the Mule installation folder.

*Single Application*

To make the connector available only to single application then place it in the
lib directory of the application otherwise if using Maven to compile and deploy
your application the following can be done:

Add the connector's maven repo to your pom.xml:

    <repositories>
        <repository>
            <id>muleforge-releases</id>
            <name>MuleForge Snapshot Repository</name>
            <url>https://repository.muleforge.org/release/</url>
            <layout>default</layout>
        </repsitory>
    </repositories>

Add the connector as a dependency to your project. This can be done by adding
the following under the dependencies element in the pom.xml file of the
application:

    <dependency>
        <groupId>org.mule.modules</groupId>
        <artifactId>mule-module-magento</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>

Configuration
-------------

You can configure the connector as follows:

    <magento:config username="value" password="value" address="value"/>

Here is detailed list of all the configuration attributes:

| attribute | description | optional | default value |
|:-----------|:-----------|:---------|:--------------|
|name|Give a name to this configuration so it can be later referenced by config-ref.|yes||
|username||no|
|password||no|
|address||no|









Add Order Shipment Comment
--------------------------

Adds a comment to the shipment. 

Example:



     <magento:add-order-shipment-comment 
    			shipmentId="#[map-payload:shipmentId]" 
           	comment="#[map-payload:comment]" 
             sendEmail="true" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the shipment's increment id|no||
|comment| the comment to add|no||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Add Order Shipment Track
------------------------

Adds a new tracking number

Example:



     <magento:add-order-shipment-track
    			shipmentId="#[map-payload:shipmentId]" 
    			carrierCode="#[map-payload:carrierCode]"
    		title="#[map-payload:title]" 
    		trackId="#[map-payload:trackId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the shipment id|no||
|carrierCode| the new track's carrier code|no||
|title| the new track's title|no||
|trackId||no||

Cancel Order
------------

Cancels an order

Example:



     <magento:cancel-order
     	   orderId="#[map-payload:orderId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order to cancel|no||

Create Order Shipment
---------------------

Creates a shipment for order

Example:



     <magento:create-order-shipment 
    			orderId="#[map-payload:orderId]"
    			comment="#[map-payload:comment]">
    		<magento:itemsQuantities>
    			<magento:itemsQuantity key="#[map-payload:orderItemId1]" value="#[map-payload:Quantity1]"/>
    			<magento:itemsQuantity key="#[map-payload:orderItemId2]" value="#[map-payload:Quantity2]"/>
    		</magento:itemsQuantities>
    	</magento:create-order-shipment>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order increment id|no||
|itemsQuantities| a map containing an entry per each (orderItemId,
           quantity) pair|no||
|comment| an optional comment|yes||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Get Order
---------

Answers the order properties for the given orderId

Example:



      <magento:get-order orderId="#[map-payload:orderId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order whose properties to fetch|no||

Get Order Invoice
-----------------

Retrieves order invoice information

Example:



      	<magento:get-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId||no||

Get Order Shipment Carriers
---------------------------

Creates an invoice for the given order

Example:



      <magento:get-order-shipment-carriers  orderId="#[map-payload:orderId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

Get Order Shipment
------------------

Adds a comment to the given order's invoice

Example:



      <magento:get-order-shipment 
    			shipmentId="#[map-payload:orderShipmentId]" /> 

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId||no||

Hold Order
----------

Puts order on hold

Example:



      <magento:hold-order orderId="#[map-payload:orderId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

List Orders
-----------

Lists order attributes that match the 
given filtering expression

Example



     <magento:list-orders 
    			filter="gt(subtotal, #[map-payload:minSubtotal])"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

List Orders Invoices
--------------------

Lists order invoices that match the given filtering expression

Example:



     <magento:list-orders-invoices filter="notnull(parent_id)" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

List Orders Shipments
---------------------

Lists order shipment atrributes that match the given 
optional filtering expression

Example:



     <magento:list-orders-shipments filter="null(parent_id)" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filter||yes||

Delete Order Shipment Track
---------------------------

Deletes the given track of the given order's shipment

<magento:delete-order-shipment-track
	shipmentId="#[map-payload:shipmentId]" trackId="#[map-payload:trackId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|shipmentId| the target shipment id|no||
|trackId| the id of the track to delete|no||

Add Order Comment
-----------------

Adds a comment to the given order id



     <magento:add-order-comment 
    				orderId="#[map-payload:orderId]"
    			status="#[map-payload:status]" 
    			comment="#[map-payload:comment]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId| the order id|no||
|status| TODO possible values?|no||
|comment||no||
|sendEmail| if an email must be sent after shipment creation|yes|false|

Unhold Order
------------

Releases order

Example:



      <magento:unhold-order orderId="#[map-payload:orderId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||

Create Order Invoice
--------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|orderId||no||
|itemsQuantities||no||
|comment||yes||
|sendEmail||yes|false|
|includeCommentInEmail||yes|false|

Add Order Invoice Comment
-------------------------

Adds a comment to the given order's invoice

Example: 



      <magento:add-order-comment 
    			orderId="#[map-payload:orderId]"
    			status="#[map-payload:status]" 
    			comment="#[map-payload:comment]" 

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||
|comment| the comment to add|no||
|sendEmail| if an email must be sent after shipment creation|yes|false|
|includeCommentInEmail| if the comment must be sent in the email|yes|false|

Capture Order Invoice
---------------------

Captures and invoice

Example: 



      <magento:capture-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice to capture|no||

Void Order Invoice
------------------

Voids an invoice

Example: 



      <magento:void-order-invoice invoiceId="#[map-payload:invoiceId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||

Cancel Order Invoice
--------------------

Cancels an order's invoice

Example: 



      <magento:cancel-order-invoice invoiceId="#[map-payload:invoiceId]"  />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|invoiceId| the invoice id|no||

Create Customer Address
-----------------------

Creates a new address for the given customer using the given address
attributes



     <magento:create-customer-address customerId="#[map-payload:customerId]"  >
    	    <magento:attributes >
    		  <magento:attribute key="city_code" value="#[map-payload:cityCode]"/>
    	    </magento:attributes>
          </magento:create-customer-address>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributes||no||

Create Customer
---------------

Creates a customer with the given attributes

Example: 



     	<magento:create-customer>
    	      <magento:attributes >
    		    <magento:attribute key="email" value="#[map-payload:email]"/>
    		    <magento:attribute key="firstname" value="#[map-payload:firstname]"/>
    		    <magento:attribute key="lastname" value="#[map-payload:lastname]"/>
    			    <magento:attribute key="password" value="#[map-payload:password]"/>
    	      </magento:attributes>
           </magento:create-customer>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributes| the attributes of the new customer|no||

Delete Customer
---------------

Deletes a customer given its id

Example:



     <magento:delete-customer customerId="#[map-payload:customerId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||

Delete Customer Address
-----------------------

Deletes a Customer Address

Example:



     <magento:delete-customer-address addressId="#[map-payload:addressId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId||no||

Get Customer
------------

Answers customer attributes for the given id. Only the selected attributes are
retrieved

Example:



     <magento:get-customer  customerId="#[map-payload:customerId]"  >
    	<magento:attributeNames>
    		<magento:attributeName>customer_name</magento:attributeName>
    			<magento:attributeName>customer_last_name </magento:attributeName>
    		<magento:attributeName>customer_age</magento:attributeName>
    	</magento:attributeNames>
      </magento:get-customer>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributeNames| the attributes to retrieve. Not empty|no||

Get Customer Address
--------------------

Answers the customer address attributes

Example: 


     <magento:get-customer-address  addressId="#[map-payload:addressId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId||no||

List Customer Addresses
-----------------------

Lists the customer address for a given customer id

Example: 



      <magento:list-customer-addresses customerId="#[map-payload:customerAddresses]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId| the id of the customer|no||

List Customer Groups
--------------------

Lists all the customer groups

Example: 



     <magento:list-customer-groups />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Customers
--------------

Answers a list of customer attributes for the given filter expression.

Example:



     <magento:list-customers filters="gteq(customer_age, #[map-payload:minCustomerAge])" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filters| an optional filtering expression.|yes||

Update Customer
---------------

Updates the given customer attributes, for the given customer id. Password can
not be updated using this method

Example:



     <magento:update-customer customerId="#[map-payload:customerId]">
    	    <magento:attributes>
    	       <magento:attribute key="lastname" value="#[map-payload:lastname]"/>
    	    </magento:attributes>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|customerId||no||
|attributes| the attributes map|no||

Update Customer Address
-----------------------

Updates the given map of customer address attributes, for the given customer address

Example:



     <magento:update-customer-address addressId="#[map-payload:addressId]">
    	  <magento:attributes>
    		<magento:attribute key="street" value="#[map-payload:street]"/>
    		<magento:attribute key="region" value="#[map-payload:region]"/>
    	   </magento:attributes>
        </magento:update-customer-address>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|addressId| the customer address to update|no||
|attributes|  the address attributes to update|no||

List Stock Items
----------------

Retrieve stock data by product ids

Example:



     <magento:list-stock-items >
    	<magento:productIdOrSkus>
    		<magento:productIdOrSku>1560</magento:productIdOrSku>
    	 	<magento:productIdOrSku>JJFO986</magento:productIdOrSku>
    	</magento:productIdOrSkus>
    </magento:list-stock-items>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productIdOrSkus| a not empty list of product ids or skus whose attributes to list|no||

Update Stock Item
-----------------

Update product stock data given its id or sku

Example:



      <magento:update-stock-item productIdOrSku="#[map-payload:productIdOrSku]">
    	<magento:attributes>
    		<magento:attribute key="qty" value="#[map-payload:quantity]"/>
    	</magento:attributes>
    </magento:update-stock-item>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productIdOrSku| the product id or sku of the product to update|no||
|attributes||no||

List Directory Countries
------------------------

Answers the list of countries
Example:


     <magento:list-directory-countries"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Directory Regions
----------------------

Answers a list of regions for the given county
Example:


     <magento:list-directory-regions countryId="#[map-payload:countryId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|countryId| the country code, in ISO2 or ISO3 format|no||

Add Product Link
----------------

Links two products, given its source and destination productIdOrSku.
Example:



      <magento:add-product-link type="#[map-payload:type]"     
                             productId="#[map-payload:productId]"
                             linkedProductIdOrSku="#[map-payload:linkedProductId]">
               <magento:attributes> 
                  <magento:attribute key="qty" value="#[map-payload:qty]"/>
               </magento:attributes>
             </magento:add-product-link>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type|           the product type|no||
|productId|           the id of the source product. Use it instead of productIdOrSku
           in case you are sure the source product identifier is a
           product id|yes||
|productSku|           the sku of the source product. Use it instead of productIdOrSku
           in case you are sure the source product identifier is a
           product sku|yes||
|productIdOrSku|           the id or sku of the source product.|yes||
|linkedProductIdOrSku|           the destination product id or sku.|no||
|attributes|           the link attributes|no||

Create Product Attribute Media
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|attributes||no||
|storeView||no||

Delete Product Attribute Media
------------------------------

Removes a product image. See catalog-product-attribute-media-remove SOAP
method.
Example:



     <magento:delete-product-attribute-media 
                 productSku="#[map-payload:productSku]" 
                 file="#[map-payload:fileName]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku
           in case you are sure the product identifier is a
           product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku
           in case you are sure the product identifier is a
           product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|file||no||

Delete Product Link
-------------------

Deletes a product's link.

Example:



     <magento:delete-product-link 
                 type="#[map-payload:type]"                    
                 productId="#[map-payload:productId]"
                 linkedProductIdOrSku="#[map-payload:linkedProductId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type| link type|no||
|productId|           the id of the source product. Use it instead of productIdOrSku
           in case you are sure the source product identifier is a
           product id|yes||
|productSku|           the sku of the source product. Use it instead of productIdOrSku
           in case you are sure the source product identifier is a
           product sku|yes||
|productIdOrSku|           the id or sku of the source product.|yes||
|linkedProductIdOrSku||no||


Get Product Attribute Media
---------------------------

Lists linked products to the given product and for the given link type.
Example:



     <magento:get-product-attribute-media 
                 productIdOrSku="#[map-payload:productIdOrSku]"
                 file="#[map-payload:fileName]"
                 storeView="#[map-payload:storeView]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|file||no||
|storeView||yes||



List Category Attributes
------------------------

Retrieve product image types. See catalog-product-attribute-media-types SOAP
method.

Example: 


     <magento:list-category-attributes setId="#[map-payload:setId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Category Attribute Options
-------------------------------

Retrieves attribute options. See catalog-category-attribute-options SOAP
method.

Example:


     <magento:list-category-attributes-options attributeId="#[map-payload:attributeId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributeId||no||
|storeView| optional|yes||

List Product Attribute Media
----------------------------

Retrieves product image list. See catalog-product-attribute-media-list SOAP
method
Example:


       <magento:list-product-attribute-media
                     productId="#[map-payload:productId]"
                     storeView="#[map-payload:storeView]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|storeView||yes||

List Product Attribute Media Types
----------------------------------

Retrieve product image types. See catalog-product-attribute-media-types SOAP
method.

Example:


     <magento:list-product-attribute-media-types setId="#[map-payload:setId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|setId| the setId|no||

List Product Attribute Options
------------------------------

Answers the product attribute options. See catalog-product-attribute-options
SOAP method.

Example:


     <magento:list-product-attribute-options attributeId="#[map-payload:attributeId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|attributeId||no||
|storeView| optional|yes||

List Product Attributes
-----------------------

Retrieves product attributes list. See catalog-product-attribute-list SOAP
methods

Example:



     <magento:list-product-attributes setId="#[map-payload:setId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|setId||no||

List Product Attribute Sets
---------------------------

Retrieves product attribute sets. See catalog-product-attribute-set-list SOAP
method.

Example:



     <magento:list-product-attribute-sets/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Product Attribute Tier Prices
----------------------------------

Retrieve product tier prices. See catalog-product-attribute-tier-price-info
SOAP Method.
Example:



     <magento:list-product-attribute-tier-prices productIdOrSku="#[map-payload:productIdOrSku]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||

List Product Link
-----------------

Lists linked products to the given product and for the given link type

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type| the link type|no||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||

List Product Link Attributes
----------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||

List Product Link Types
-----------------------

Answers product link types
Example:



     <magento:list-product-link-types />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

List Product Types
------------------

Answers product types. See catalog-product-type-list SOAP method
Example:



     <magento:list-product-types />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||

Update Category Attribute Store View
------------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||

Update Product Attribute Media
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|file||no||
|attributes||no||
|storeView||no||

Update Product Attribute Media Store View
-----------------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||

Update Product Attribute Store View
-----------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||


Update Product Link
-------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type||no||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|linkedProduct||no||
|attributes||no||

List Category Products
----------------------

Lists product of a given category. See  catalog-category-assignedProducts SOAP method.   
Example:



     <magento:list-category-products  categoryId="#[map-payload:categoryId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||

Add Category Product
--------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|position||no||

Create Category
---------------

Creates a new category. See catalog-category-create SOAP method.

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|parentId||no||
|attributes||no||
|storeView||no||

Catalog Category Current Store
------------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||no||

Delete Category
---------------

Deletes a category. See  catalog-category-delete SOAP method
Example:


     <magento:delete-category categoryId="#[map-payload:categoryId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId| the category to delete|no||

Get Category
------------

Answers category attributes. See catalog-category-info  SOAP method.
  
Example:


     <magento:get-category categoryId="#[map-payload:categoryId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||
|storeView||yes||
|attributeNames||no||

List Category Levels
--------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|website||no||
|storeView||yes||
|parentCategory||no||

Move Category
-------------

Move category in tree. See  catalog-category-move SOAP method.

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||
|parentId||no||
|afterId||no||

Delete Category Product
-----------------------

Remove a product assignment. See catalog-category-removeProduct SOAP method. 
Example:



     <magento:delete-category-product 
                 categoryId="#[map-payload:categoryId]"
                 productSku="#[map-payload:productSku]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||

Get Category Tree
-----------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|parentId||no||
|storeView||no||

Update Category
---------------

Updates a category. See catalog-category-update SOAP method

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId||no||
|attributes||no||
|storeView||no||

Update Category Product
-----------------------

Updates a category product

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|categoryId| the category id|no||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|position||no||

List Inventory Stock Items
--------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|products||no||

Update Inventory Stock Item
---------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|attributes||no||

Create Product
--------------

Creates a new product

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|type| the new product's type|no||
|set| the new product's set|no||
|sku| the new product's sku|no||
|attributes| the attributes of the new product|no||

Update Product Store View
-------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||yes||

Get Product Store View
----------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|storeView||yes||

Delete Product
--------------

Deletes a product. See catalog-product-delete SOAP method.

Example:

<magento:delete-product productId="#[map-payload:productId]" />

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||

Get Product Special Price
-------------------------

Answers a product special price. See catalog-product-getSpecialPrice SOAP method.

Example: 



     <magento:get-product-special-price productId="#[map-payload:productId]"/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|storeView||yes||

Get Product
-----------

Answers a product's attributes. See catalog-product-info SOAP method.

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|storeView| the optional store view|yes||
|attributes| the attributes to retrieve|no||

List Products
-------------

Retrieve products list by filters. See catalog-product-list SOAP method.

Example:



     <magento:list-products/>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|filters| an optional filtering expression|yes||
|storeView| an optional storeView|yes||

Update Product Special Price
----------------------------

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId||yes||
|productSku||yes||
|productIdOrSku||yes||
|specialPrice||no||
|fromDate||no||
|toDate||no||
|storeView||yes||

Update Product
--------------

Updates a product. See catalog-category-updateProduct SOAP method 
Example:



     <magento:update-product productIdOrSku="#[map-payload:productIdOrSku]">
             <magento:attributes>
                 <magento:attribute key="name" value="#[map-payload:name]"/>
             </magento:attributes>
           </magento:update-product>

| attribute | description | optional | default value | possible values |
|:-----------|:-----------|:---------|:--------------|:----------------|
|config-ref|Specify which configuration to use for this invocation|yes||
|productId|           the id of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product id|yes||
|productSku|           the sku of the product. Use it instead of productIdOrSku in
           case you are sure the product identifier is a product sku|yes||
|productIdOrSku|           the id or sku of the product.|yes||
|attributes| the not empty map of product attributes to update|no||
|storeViewIdOrCode| optional store view|yes||

















