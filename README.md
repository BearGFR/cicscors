Disclaimer: this is a public, informal discussion of CORS applied to CICS TS between interested parties. It is not endorsed by IBM.

# CORS requirements

CICS HTTP support is currently unhelpful if the web client (browser or REST client) sends the requests required to implement the [CORS protocol](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS).

In particular, CICS TS treats any OPTIONS request as an invalid request and returns an error to the client.

There is an [existing RFE asking for OPTIONS support (75575)](http://www.ibm.com/developerworks/rfe/execute?use_case=viewRfe&CR_ID=75575).

CORS always needs to be configured in a server responding to HTTP requests - for example, WebSphere Liberty requires [entries in it's server.xml](https://www.ibm.com/support/knowledgecenter/SS7K4U_liberty/com.ibm.websphere.wlp.zseries.doc/ae/twlp_webcontainer_cors_config.html).

How could CICS begin to react more helpfully to OPTIONS requests?

Comments from Robert Garrett:

I agree adding this support is important, especially if CICS is going to (continue to) become a major player in the world of web
services and API's.

I suggest:
Adding this support to the configuration options for a web service, but only if said web service is configured and deployed
into CICS using the 'bundle' format that makes use of XML.
I say this because I imagine that the idea of adding this support via traditional means (CSD/BAS and all the trappings thereof)
will not be appealing to the IBM folk who are charged with delivering it (thus it will take a long time to do).  I similarly
would not be a fan of a URM based approach because that means some "U" has to be responsible for creating and subsequently
maintaining the "RM".  Our shop is actively discouraging such activity and is engaged in trying to get rid of custom code
at present.
Making the support available only via bundles I'm thinking would allow IBM to deploy all the trappings of these artifacts via
XML and might also be able to make use of the existing support for Liberty JVMS's.  Also since direct modification of XML
based artifacts is not supported / discouraged all of the associated trappings of a CSD/BAS approach (doc, CSD changes, DFHCSDUP
changes, CED* changes) could be avoided.
