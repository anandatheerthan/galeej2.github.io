---
layout: post
title: IDoc and BDoc
date: 2013-06-02 23:31
author: administrator
comments: true
categories: [SAP CRM/ECC]
---
IDOC: An intermediate document, container for exchanging data between R/3 and other SAP and non-SAP applications. Structured collection of segments. Segments are structured collection of data elements.<br/><br/>BDOCS: Business Documents are the semantical layer for the whole CRM, regardless of implementation details. A major achievement of a semantical layer is, that the need for point-to-point mappings are eliminated. Using BDocs mean fast integration of applications. The definition of Business Documents (BDoc) does not contain implementation details. It differs depending on the underlying technology, so that the optimal representation of a BDoc can be used:<br/><br/>Implementation examples:<br/><br/>• CRM Server: Internal tables<br/><br/>• Laptops: ADO record sets<br/><br/>• Non-SAP System: XML Decoupling of Messaging
