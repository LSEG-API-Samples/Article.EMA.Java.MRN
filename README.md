##MRN (Machine Readable News) on Elektron

####Introduction
This project is one of the many learning materials published by Thomson Reuters to help developers learning Thomson Reuters APIs.
This specific project source code is part of the [Introduction to machine readable news with Elektron Message API](https://developers.thomsonreuters.com/article/mrn-article). Please consult this page for more learning materials and documentation about this API.

For any question related to this tutorial|article|example ***(use the appropriate term)*** please use the Developer Community [Q&A Forum](https://community.developers.thomsonreuters.com).

***Note:** To be able to ask questions and to benefit from the full content available on the [Thomson Reuters Developer Community portal](https://developers.thomsonreuters.com) we recommend you to [register here]( https://developers.thomsonreuters.com/iam/register) or [login here]( https://developers.thomsonreuters.com/iam/login?destination_path=Lw%3D%3D).*

####EMA Java Console Example

#####Overview
example150__NewsAnalytics__Streaming is a simple example that uses EMA Java/Elektron SDK
to demonstrate subscription, decoding and parsing of MRN data streams: 

* MRN_STORY
* MRN_TRSI
* MRN_TRNA

#####How to Build
We used:

* Oracle Java 8
* Elektron SDK Java
* Eclipse IDE

#####How to Run
Command line arguments: 

_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_STORY _MRN_USER_

_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRNA _MRN_USER_

_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRSI _MRN_USER_


#####Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
  * Accumulate all fragments if more than one
  * Concatenate the fragments
  * Unzip using gunzip
  * Pretty-print json
  



####EMA Java GUI Example
#####Overview
NewsAnalytics__Streaming_GUI is a GUI Viewer that allows to view side-by-side and demonstrates subscribing, decoding and parsing of MRN data RICs: 
* MRN_STORY
* MRN_TRSI
* MRN_TRNA

#####How to Build
We used:
* Oracle Java 8
* Elektron SDK Java
* NetBeans IDE

#####How to Run
Command line arguments:
_MRN_HOST_ 14002 _MRN_SERVICE_ _MRN_USER_

Suggested VM Options:
-Xmx2028m -Xms1024m

#####Parsing Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
   * Accumulate all fragments if more than one
   * Concatenate the fragments
   * Unzip using gunzip
   * Pretty-print json

#####Understanding MRN Data

To better understande the data from any and all MRN streams, one can:
* Stop the stream of data by clicking Stop button
* Copy a piece of data
* Paste it outside the example, into a text file, or onto an excel sheet
* Resume the stream by clicking Resume when ready

Streaming data from the four RICs (streams) is presented side-by-side so that one can easily:
* Visually compare the data between the streams
* Select the stream that is best suited for a specific use case




####EMA Java Store Example
#####Overview
NewsAnalytics_Store example illustrates subscribing, decoding and parsing of MRN News Analytics via MRN_TRNA RIC, and storing archiving the data into MySQL database.  Subsequently, the collected data is ready for analysis and visualization.  Simultaneously or consequently, it can be used for custom target alerting. 

#####How to Build
We used:

* Oracle Java 8
* Elektron SDK Java
* Eclipse IDE with EclipseLink
* MySQL database

#####How to Run
Command line arguments:
_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_TRNA _MRN_USER_
Suggested VM Options: 
-Xmx2028m -Xms1024m
Database setup:
Create database named MRN
Optionally, drop tables within before the run

#####Parsing Approach
* Subscribe to the feed, request domain News Analytics, register for updates
* On an update of type FieldList, look type BUFFER named FRAGMENT, decode:
    * Accumulate all fragments if more than one
    * Concatenate the fragments
    * Unzip using gunzip
    * Pretty-print json
    
#####Storing approach
TRNA ratings are 
* Converted from json objects into custom objects
* As custom objects, they stored in database in the corresponding custom tables

EclipseLink is used, two types of persisted objects are defined in persistence.xml
* TRNARating
* AnalyticScore

Each rating is identified by GUID which is original news identifier, it is stored with TRNARating.  Each rating carries one to many analytic scores.  Each analytic score is identified by RIC, Permid or news category (N2), and is stored with source timestamp.   
