# Input

**As a CTO of a healthcare software company you need to have this information.**

## This information should have automated collection

It should be perfectly possible to automatically collect all this information automatically from production interfaces.  
Somewhere configuration files or databases exist with this information and so centralized collection should be possible and in this way the information kept up to date.

## Example inventory table

| Client   | Interface | Port In | Application In       | Port / Host Out | Application Out   | Protocol ACK Only |
| -------- | --------- | ------: | -------------------- | --------------- | ----------------- | ----------------- |
| Client A | ADT       |    5001 | Patient Registration | 6001 / emr01    | EMR               | Yes               |
| Client A | Orders    |    5002 | CPOE                 | 7001 / lis01    | Laboratory System | Yes               |
| Client B | Results   |    5003 | LIS                  | 6002 / emr01    | EMR               | No                |
| Client B | Radiology |    5004 | EMR                  | 8001 / ris01    | RIS               | Yes               |
| Client C | Billing   |    5005 | EMR                  | 1433 / sql01    | Billing System    | N/A               |

## Can you give me a spreadsheet of the port numbers and hosts our interfaces are listening on?

This is typically a binary yes or no answer. The organization either has this information at scale or they do not.

It is something that should be known.

If they do not know the hosts that each interface is receiving data from, this poses a potential security risk—how can you be sure a system hasn't been compromised? At the very least, this information should be logged for security purposes.

## What ports/hosts are we sending information to?

Again, this is very important. At scale, this information is critical and should be known organization-wide for support and business continuity purposes.

## Is the data encrypted using TLS/SSL—yes or no?

Unfortunately, many legacy systems do not have this capability, but it should be documented.

## Is the acknowledgement protocol just a simple protocol ACK, or is there more?

This is key—hopefully, it is the former, as that is much simpler. When an ACK simply signals that data has been received, it is a much easier problem to manage than if the ACK signals application errors.

The latter is fortunately rare, since most HL7 senders use the simple protocol ACK, as implementing more complexity is challenging.

I give a deeper explanation about the issues regarding [protocol versus application acks here](ack.md). 

