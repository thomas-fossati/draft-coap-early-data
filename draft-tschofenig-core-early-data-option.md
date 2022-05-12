---
title: Early Data Option for CoAP
abbrev: CoAP Early Data
docname: draft-tschofenig-core-early-data-option-latest
category: std
consensus: true
submissiontype: IETF

ipr: trust200902
area: ART
workgroup: CoRE Working Group
keyword: CoAP, Option, Early Data, TLS 1.3

stand_alone: yes
pi:
  rfcedstyle: yes
  toc: yes
  tocindent: yes
  sortrefs: yes
  symrefs: yes
  strict: yes
  comments: yes
  inline: yes
  text-list-symbols: o-*+
  compact: yes
  subcompact: yes
  consensus: false

author:
 - name: Hannes Tschofenig
   organization: "Arm Limited"
   email: Hannes.Tschofenig@gmx.net
 - name: Thomas Fossati
   organization: "Arm Limited"
   email: Thomas.Fossati@arm.com

normative:
  DTLS13: RFC9147
  TLS13: RFC8446
  CoAP: RFC7252

entity:
  SELF: "RFCthis"

--- abstract

TODO

--- middle

# Introduction

TODO

## Requirements Language

{::boilerplate bcp14-tagged}

# 0-RTT Data

When clients and servers share a PSK, TLS/DTLS 1.3 allows clients to send data
on the first flight ("early data"). This features reduces communication setup
latency but requires application layer protocols to define its use with the
0-RTT data functionality.

For HTTP this functionality is described in {{!RFC8470}}. This document
specifies the application profile for CoAP, which follows the design of
{{!RFC8470}}.

For a given request, the level of tolerance to replay risk is specific to the
resource it operates upon (and therefore only known to the origin server).  In
general, if processing a request does not have state-changing side effects,
the consequences of replay are not significant. The server can choose whether
it will process early data before the TLS handshake completes.

It is RECOMMENDED that origin servers allow resources to explicitly configure
whether early data is appropriate in requests.

This document specifies the Early-Data option, which indicates that the
request has been conveyed in early data and that a client understands the 4.25
(Too Early) status code. The semantic follows {{!RFC8470}}.

| No. | C | U | N | R | Name | Format | Length | Default | E |
| --- | - | - | - | - | ---- | ------ | ------ | ------- | - |
| TBD | x | | | | Early-Data | empty | 0 | (none) | x |
{: #fig-early-data title="Early-Data Option"}

<cref>Note that 4.25 is just the suggested CoAP response code, which has not
been registered yet.</cref>

# Open Issues

A list of open issues can be found at
https://github.com/thomas-fossati/draft-coap-early-data/issues

# Security Considerations

TODO


# IANA Considerations

## New Option

IANA is asked to add the Option defined in {{tbl-early-data-option}} to the
CoAP Option Numbers registry.

| Number | Name | Reference |
| ------ | ---- | --------- |
| TBD | Early-Data | {{&SELF}} |
{: #tbl-early-data-option align="left"
   title="Early-Data Option"}

## New Response Code

IANA is asked to add the Response Code defined in {{tbl-too-early-code}} to
the CoAP Response Code registry.

| Code | Description | Reference |
| ---- | ----------- | --------- |
| 4.25 | Too Early   | {{&SELF}} |
{: #tbl-too-early-code align="left"
   title="Too Early Response Code"}

--- back

# Acknowledgments
{:unnumbered}

TODO

