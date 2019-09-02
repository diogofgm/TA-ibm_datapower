Latency message formats
Standard and enhanced latency messages use different formats.
Message 0x80e00073 uses the following format.
Latency: 0 0 0 0 2 0 0 1 0 0 0 3 0 0 0 0
In this example, the value 2 is in position 5. Each position indicates a duration that is being measured. The order of the durations is not linear (logical transaction processing sequence).
Message 0x80e007ad uses the following format.
ExtLatency: HR=0,BR=0,PS=0,AAA=2,AXF=2,AXF=2,ARE=2,BS=2,CS=2,BS=3, == HR=4,BR=4,PS=4,AXF=5,ARE=5,ARA=5,BS=5,TC=5
Each duration is preceded by a keyword and is recorded in the order it occurs. Durations are recorded for only completed events. The == separator divides request processing from response processing.



https://www.ibm.com/support/knowledgecenter/SS9H2Y_7.6.0/com.ibm.dp.doc/latency_messages.html

Table 1. Message 0x80e00073 values in logical transaction processing sequence
Position	Description	Phase of the transaction
1	Request header is read.	Receive request header.
3	Front side transform begun.	Front side processing.
7	Body is read from client.
6	Request-processing started in request rule.
4	Request-processing completed in request rule.
15	Back side connection attempted.	Transmit to back side.
16	Connection to server started.
2	Request header is sent.
5	Entire request is sent.
8	Response header is received.	Receive from back side.
10	Back side transform begun.	Back side processing.
14	Body is read from server.
13	Response-processing started in response rule.
11	Response-processing completed in response rule.
9	Header sent to client.	Transmit response to client.
12	Response sent.


Table 2. Message 0x80e007ad keywords in alphabetical order
Keyword	Description
Axx	Action processing keywords. The actions are enumerated in Table 3.
BR	Body read.
BS	Body sent.
CS	Connection started.
HR	Headers read.
HS	Header sent.
PC	Processing is complete for the last action in the processing rule of the processing policy.
PS	Processing is started, which is before the first action in the processing rule of the processing policy.
TC	Transaction is complete.
TS	Transaction started.
==	Separator between request and response rule processing.


Table 3. Message 0x80e007ad keywords for action processing
Keyword	Action description
AAA	Processing of a defined AAA action.
ACB	Processing of the cryptographic binary actions: PKCS #7 sign, verify, encrypt, or decrypt.
ACL	Processing of the call processing rule action.
ACO	Processing of the conditional action, which implements programmatic if-then-else logic.
ACP	Processing of the checkpoint event action, which triggers data collection.
ACV	Processing of the convert query parameters to XML action.
ADB	Start of the probe capture. You use the probe to debug transactions.
AEA	End of attach action, which reads in all attachments after the root.
AES	Processing of the event-sink action, which waits for designated asynchronous actions to complete.
AEX	Processing of the extract with XPath action, which applies an XPath expression to a context and stores the result in another context.
AFE	Processing of the fetch action, which retrieves a document from a remote location.
AFI	Processing of the filter action, which accepts or rejects documents according to filtering criteria.
AGS	Processing of the GatewayScript action.
AHR	Processing of the header rewrite action, which rewrites HTTP headers or URLs with a URL rewrite policy.
ALG	Processing of the log action, which takes a copy of a message payload and sends it to a log destination.
ALP	Processing of the for-each action, which implements a programmatic loop for each defined action. Each iteration of the loop stores its results in a separate output context.
AMR	Processing of the method rewrite action, which rewrites the HTTP method.
AOE	Processing of the on-error action, which enables user-defined error handling.
APP	Start a streaming scan for an XPath pattern.
APT	Starts the pass-through processor on the input, which immediately passes the name-value pair for more processing.
APUA	Processing of the unread attachments action, which sends all remaining attachments to the output through the MIME processor.
ARA	Processing of the results asynchronous action.
ARE	Processing of the results action.
ARS	Processing of the route with variables action.
ART	Processing of the route with XPath expression action.
ASA	Processing of the start attach action, which reads all attachments before the root and modifies the INPUT context to be only the root.
ASLM	Processing of the enforce SLM policy action.
ASM	Processing of the stream attach action, which reads each part from a MIME encoded document, finds the processing rule, and calls the processing rule.
ASQL	Processing of the SQL statement action.
ASR	Selectable runs after a non-piped parse to select the processing rule from the processing policy.
AST	Processing of the strip attachments action, which removes all or specified MIME attachments from a specified context.
ASV	Processing of the set variable action.
AVA	Processing of the validate action.
AVX	Processing of the validate action with a document-specified schema. You can specify only VALIDATE, but the DataPower® service can transform the document to VALIDATEXSI internally.
AXB	Processing of the binary transform action.
AXF	Processing of the XML transform action.
AXN	Processing of the language transform action.
AXP	Processing of the processing instruction transform action.
Note
APPJ, APPS, APPX, APRB, APRJ, and APRX are keywords that define processing of internal activities.
Table 4. Comparison of latency message values in the typical order of their occurrence
0x80e00073 Position	Description	0x80e007ad Keyword
Message initialized.	Transaction started.	TS
1	Request header is read.	HR
3	Front side transform begun.	No equivalent.
7	Body is read from client.	BR
6	Request-processing started in request rule.	PS
No equivalent.	Actions in the request rule.	Axx
4	Request-processing completed in request rule.	PC
15	Back side connection attempted.	No equivalent.
16	Connection to server started.	CS
2	Request header is sent.	HS
5	Entire request is sent.	BS
Not applicable.	Indicator dividing request rule processing and response rule processing.	==
8	Response header is received.	HR
10	Back side transform begun.	No equivalent.
14	Body is read from server.	BR
13	Response-processing started in response rule.	PS
No equivalent.	Actions in response rule.	Axx
11	Response-processing completed in response rule.	PC
9	Header sent to client.	HS
12	Body sent to client.	BS
Message created.	Transaction complete	TC