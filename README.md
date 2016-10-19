##MRN (Machine Readable News) on Elektron
####EMA Java Console Example

#####Overview
example150__NewsAnalytics__Streaming is a simple example that uses EMA Java/Elektron SDK
to demonstrate subscription, decoding and parsing of four MRN data feeds: 

* MRN_HDLN
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

_MRN_HOST_ 14002 _MRN_SERVICE_ MRN_HDLN _MRN_USER_
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
