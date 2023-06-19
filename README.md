## MRN (Machine Readable News) on Refinitiv Real-Time

#### Introduction
This set of examples is one of the many learning materials published by Refinitiv to help developers learning Refinitiv APIs; this source code is part of the [Introduction to Machine Readable News (MRN) with Enterprise Message API (EMA)](https://developers.refinitiv.com/en/article-catalog/article/introduction-machine-readable-news-mrn-elektron-message-api-ema).  Please consult this page for more learning materials and documentation about this API.

For any question related to this article or the examples please use the Developer Community [Q&A Forum](https://community.developers.refinitiv.com/).

***Note:** To be able to ask questions and to benefit from the full content available on the [Refinitiv Developer Community portal](https://developers.refinitiv.com/) we recommend you to [register here](https://developers.refinitiv.com/content/devportal/en_us/register.html) or [login here](https://developers.refinitiv.com/content/devportal/en_us/initCookie.html).*

#### EMA Java Console Example

##### Overview
NewsAnalytics__Streaming_Console is a simple example that uses EMA Java/Refinitiv Real-Time SDK to demonstrate subscription, decoding and parsing of MRN data feeds: 

* MRN_STORY
* MRN_TRSI
* MRN_TRNA

##### How to Build
We used:

* Oracle Java 8
* Refinitiv Real-Time SDK Java
* Eclipse IDE

##### How to Run
Command line arguments:

_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_STORY _MRN_USER_
_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRNA _MRN_USER_
_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRSI _MRN_USER_
 
##### Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
    * Accumulate all fragments if more than one
    * Concatenate the fragments
    * Unzip using gunzip
    * Pretty-print json

===================================================================================================

#### EMA Java GUI Example

##### Overview
NewsAnalytics__Streaming_GUI is a GUI Viewer that allows to view side-by-side and demonstrates subscribing, decoding and parsing of MRN data RICs: 

* MRN_STORY
* MRN_TRSI
* MRN_TRNA

##### How to Build
We used:

* Oracle Java 8
* Refinitiv Real-Time SDK Java 1.2.1

Download Refinitiv Real-Time SDK Java from https://developers.refinitiv.com/en/api-catalog/elektron/elektron-sdk-java/download
Copy Refinitiv Real-Time SDK Java jar files to \lib\
The file structure should looks like this:
	\bin\
		\com\refinitiv\ema\examples\mrn\
											\AppClient.class
											\MRNConsumer.class
											\MRNFXMain$1.class
											\MRNFXMain.class
	\css\
		\dark.css
		\EikonWebUI.css
		\EikonWebUI-main-Custom.css
		\EikonWebUI-main-Custom-formatted.css
		\Nova_View.css
		\WebUI.css
	\lib\
		\ansipage-3.2.1.0.jar
		\commons-codec-1.4.jar
		\commons-collections-3.2.2.jar
		\commons-configuration-1.10.jar
		\commons-lang-2.6.jar
		\commons-logging-1.1.1.jar
		\commons-logging-1.2.jar
		\ema-3.6.0.0-javadoc.jar
		\ema-3.6.0.0.jar
		\gradle-wrapper.jar
		\httpclient-4.1.2.jar
		\httpclient-cache-4.1.2.jar
		\httpcore-4.1.2.jar
		\httpmime-4.1.2.jar
		\java-json.jar
		\jdacsUpalib.jar
		\mockito-all-1.9.0.jar
		\slf4j-api-1.7.12.jar
		\slf4j-jdk14-1.7.12.jar
		\eta-3.6.0.0.jar
		\etaValueAdd-3.6.0.0.jar
		\etaValueAddCache-3.6.0.0.jar
		\xpp3-1.1.4c.jar
	\src\
		\com\refinitiv\ema\examples\mrn\
											\MRNConsumer.java
											\MRNFXMain.java
	\compile.bat
	\ExampleMRNStreamingGUI.md
	\run.bat

Open a command line and launch "compile.bat"

##### How to Run
Command line arguments:
<ADS_HOST> <ADS_PORT> <MRN_SERVICE> <MRN_USER>
Suggested VM Options:
-Xmx2028m -Xms1024m
 
##### Parsing Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
    * Accumulate all fragments if more than one
    * Concatenate the fragments
    * Unzip using gunzip
    * Pretty-print json
	* Convert RMTES String to UTF-8 String

##### Understanding MRN Data
To better understande the data from any and all MRN streams, one can:
* Stop the stream of data by clicking Stop button
* Copy a piece of data
* Paste it outside the example, into a text file, or onto an excel sheet
* Resume the stream by clicking Resume when ready 
Streaming data from the four RICs (streams) is presented side-by-side so that one can easily:
* Visually compare the data between the streams
* Select the stream that is best suited for a specific use case

===================================================================================================

#### EMA Java Store Example

##### Overview
NewsAnalytics_Store example illustrates subscribing, decoding and parsing of MRN News Analytics via MRN_TRNA RIC, and storing archiving the data
into MySQL database.  Subsequently, the collected data is ready for analysis and visualization.  Simultaneously or consequently, it can be used for custom target alerting. 

##### How to Build
We used:

* Oracle Java 8
* Refinitiv Real-Time SDK Java
* Eclipse IDE with EclipseLink
* MySQL database

##### How to Run
Command line arguments:
_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRNA _MRN_USER_
Suggested VM Options: 
-Xmx2028m -Xms1024m
Database setup:
Create database named MRN
Optionally, drop tables within before the run
 
##### Parsing Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
    * Accumulate all fragments if more than one
    * Concatenate the fragments
    * Unzip using gunzip
    * Pretty-print json

##### Storing approach
RNA ratings are 
* Converted from json objects into custom objects
* As custom objects, they stored in database in the corresponding custom tables
EclipseLink is used, two types of persisted objects are defined in persistence.xml
* RNARating
* AnalyticScore
Each rating is identified by GUID which is original news identifier, it is stored with RNARating.  Each rating carries one to many analytic scores.  Each analytic score is identified by RIC, Permid or news category (N2), and is stored with source timestamp.
