# HANA_TA

CREATE FULLE TEXT INDEX

CREATE FULLTEXT INDEX FT_TWEETS ON TWEETS(TWEET)
CONFIGURATION 'EXTRACTION_CORE'
TEXT ANALYSIS ON;


SELECT 
COLUMN_NAME, STATUS, TOTAL_DOCUMENT_COUNT, 
INDEXED_DOCUMENT_COUNT, QUEUE_DOCUMENT_COUNT,
ERROR_DOCUMENT_COUNT
FROM M_FULLTEXT_QUEUES
WHERE SCHEMA_NAME = 'SAP_HANA_DEMO'
AND TABLE_NAME = 'TWEETS';


SELECT TA_TYPE, count(*)
FROM "$TA_FT_TWEETS"
GROUP BY TA_TYPE
ORDER BY 2 DESC;


SELECT TA_TOKEN, count(*)
FROM "$TA_FT_TWEETS"
WHERE TA_TYPE = 'PRODUCT'
GROUP BY TA_TOKEN
ORDER BY 2 DESC;



<?xml version="1.0" encoding="UTF-8"?>  
<dictionary xmlns="http://www.sap.com/ta/4.0">  
   <entity_category name="Company">  
      <entity_name standard_form="Apple">  
            <variant name ="iPhone"/>  
            <variant name ="iphone"/>  
            <variant name ="iPhone 3GS"/>  
            <variant name ="iPhones"/>  
            <variant name ="IPHONE"/>  
            <variant name ="Iphone"/>
	<variant name ="iPhone 4G"/>
            <variant name ="iPod Apple"/>  
            <variant name ="ipod"/>  
            <variant name ="iPod touch"/>  
            <variant name ="ipod touch"/>  
            <variant name ="iPod Touch"/>  
	<variant name ="Ipod"/>  
	<variant name ="IPOD"/>  
	<variant name ="iPods"/>  
	<variant name ="iPad"/>  
	<variant name ="ipad"/>  
	<variant name ="IPad"/>  
	<variant name ="IPAD"/>  
	<variant name ="iPAD"/>  
      </entity_name>  
      <entity_name standard_form="RIM">  
            <variant name ="Blackberry"/>  
            <variant name ="BlackBerry"/>  
            <variant name ="BLACKBERRY"/>  
            <variant name ="blackberry tour"/>  
            <variant name ="blackberry bold"/>  
	<variant name ="blackberry storm"/>
	<variant name ="blackberry curve"/>
	<variant name ="BlackBerry Storm"/>
      </entity_name> 
      <entity_name standard_form="Microsoft">  
            <variant name ="Xbox"/>  
            <variant name ="Xbox Live"/>  
            <variant name ="xbox"/>  
            <variant name ="Xbox 360"/>  
            <variant name ="xbox live"/>  
	<variant name ="xbox 360"/>
	<variant name ="XBOX"/>
	<variant name ="XBOX 360"/>
      </entity_name> 	
      <entity_name standard_form="Nintendo">  
            <variant name ="Wii"/>  
            <variant name ="wii"/>  
            <variant name ="wii fit"/>  
            <variant name ="WII"/>  
            <variant name ="Wii Fit"/>  
	<variant name ="wii fit plus"/>
	<variant name ="Wii fit"/>
	<variant name ="Nintendo Wii"/>
	  </entity_name>
     <entity_name standard_form="Sony">  
            <variant name ="PlayStation"/>  
            <variant name ="PS3"/>  
            <variant name ="ps3"/>  
            <variant name ="Ps3"/>  
            <variant name ="PSP"/>  
	<variant name ="psp"/>
	<variant name ="playstation"/>
	<variant name ="PLAYSTATION"/>
	<variant name ="PS4"/>  
            <variant name ="ps4"/>  
            <variant name ="Ps4"/>
      </entity_name>
     </entity_category>  
</dictionary>


CUSTOM.hdbtextconfig
<property name="Dictionaries" type="string-list">
   <string-list-value>sap.hana.ta.config::company.hdbtextdict</string-list-value>
</property>


DROP FULLTEXT INDEX FT_TWEETS;


CREATE FULLTEXT INDEX FT_TWEETS ON TWEETS(TWEET)
CONFIGURATION 'sap.hana.ta.config::CUSTOM'
TEXT ANALYSIS ON;


SELECT TA_NORMALIZED, count(*)
FROM "$TA_FT_TWEETS"
WHERE TA_TYPE = 'Company'
GROUP BY TA_NORMALIZED
ORDER BY 2 DESC;

