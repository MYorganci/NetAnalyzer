# NetAnalyzer
Sample online tool to analyze domain and IP status, performance and various quality parameters

NetAnalyzer
The NetAnalyzer is an online tool to analyze domain and IP status, performance and various quality parameters.

The main application is the NetAnalyzer program which interfaces the users and has a Swagger Rest API definitions defined for it. The other processes (listed in the table below) operate behind the NetAnalyzer program and not meant to be directly accessed by the users.

How to see the REST API definitions
http://159.255.42.8:600/swagger

How to see the supported Network Services
GET  http://159.255.42.8:600/api/NetAnalyzer

How to see a sample input (Json)
GET http://159.255.42.8:600/api/NetAnalyzer/sampleinput.

How to see a sample output (Json)
GET http://159.255.42.8:600/api/NetAnalyzer/sampleoutput

How to query a subset (or all) of the supported Network services
PUT http://159.255.42.8:600/api/NetAnalyzer/{IP or Domain}
[Optional] Json input parameter(s) - see "How to see a sample input (Json)" above.
E.g. PUT http://159.255.42.8:600/api/NetAnalyzer/159.255.42.8

Behind the scenes Processes (not publicly exposed with Swagger)
Process Name	URL	Example
LookupPing	159.255.42.8:602/api/Ping 	http://159.255.42.8:602/api/Ping/159.255.42.8
		http://159.255.42.8:602/api/ping
LookupGeoIP	159.255.42.8:603/api/geoipinfo	http://159.255.42.8:603/api/geoipinfo/159.255.42.8
LookupRDAP	159.255.42.8:604/api/RDAP	http://159.255.42.8:604/api/rdap/159.255.42.8 true
		http://159.255.42.8:604/api/rdap/fixitkibris.com false
LookupReverseDNS	159.255.42.8:605/api/ReverseDNS	http://159.255.42.8:605/api/ReverseDNS/159.255.42.8
LookupVirusTotal	159.255.42.8:606/api/VirusTotal	http://159.255.42.8:606/api/VirusTotal/fixitkibris.com

Source Code
The complete source code projects are on the following public GitHub location
https://github.com/MYorganci/NetAnalyzer

Design Notes
• For NetAnalyzer I used Put method for the API so I can use JSON to specify the inputs
• Validation as a separate method to it can be improved/updated in one place
• Rest Calls to worker processes made via one method to standardization & code reuse

Known Issues
	1. The following service names might not return values when run on fast servers, although they work on local developer workstation.
		a. Ping
		b. VirusTotal
[Cosmetic] The netServices entry attribute 'valid' is visible whereas it need not be. It is harmless, but should be removed nonetheless.
