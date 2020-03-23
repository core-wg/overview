---
stand_alone: true
ipr: trust200902
docname: draft-bormann-core-overview-latest
keyword: Internet-Draft
cat: info
pi:
  toc: 'yes'
  tocompact: 'yes'
  tocdepth: '3'
  tocindent: 'yes'
  symrefs: 'yes'
  sortrefs: 'yes'
  comments: 'yes'
  inline: 'yes'
  strict: 'no'
  compact: 'yes'
  subcompact: 'no'
title: CoRE Working Group — Overview
abbrev: CoRE Working Group -- Overview
date: 2020-03-23
author:
-
  name: Carsten Bormann
  org: Universitaet Bremen TZI
  street: Postfach 330440
  city: Bremen
  code: D-28359
  country: Germany
  phone: +49-421-218-63921
  email: cabo@tzi.org
- ins: J. J. Jimenez
  name: Jaime Jimenez
  org: Ericsson
  email: jaime.jimenez@ericsson.com

--- abstract

The IETF "Constrained RESTful Environments" (CoRE) Working Group standardizes application layer protocols that can be used by resource-constrained devices, as can be found in the Internet of Things (IoT).  It is part of a cluster of about a dozen IETF WGs defining specifications for these environments.

This short document provides an overview of the activies of the CoRE WG as of end of March, 2020.

--- middle


# Introduction {#intro}


The IETF "Constrained RESTful Environments" (CoRE) Working Group standardizes application layer protocols that can be used by resource-constrained devices, as can be found in the Internet of Things (IoT).  It is part of a cluster of about a dozen IETF WGs that define networking (e.g., 6Lo), routing (e.g., ROLL), and security (e.g., ACE, LAKE, SUIT) for these environments.  This cluster has been growing since 2005; ten years ago, on 2010-03-09, CoRE was added to it.

# Main Specification

The main specification of CoRE is the Constrained Application Protocol (CoAP) {{?RFC7252}}.  CoAP is for applications including constrained devices what HTTP is for general purpose applications. By using UDP as the transport protocol as opposed to HTTP's use of TCP, and by removing much of the baggage of of HTTP, CoAP can be run on quite simple platforms and with very little power use.  Both protocols share the Representational State Transfer (REST) architecture, the same set of verbs (GET, PUT, POST, DELETE), and quite similar semantics.

Since CoAP's approval in 2013, further specifications have been added to support the Observe pattern of change notifications from a server (low-complexity server-push) {{?RFC7641}}, to support larger transfers {{?RFC7959}}, to add verbs (FETCH, PATCH, and idempotent iPATCH {{?RFC8132}}), and to enable the use of CoAP over TCP {{?RFC8323}}.  {{?RFC8768}} recently added a way to detect and mitigate loops in a proxy configuration, motivated by the requirements of the Distributed Denial-of-Service Open Threat Signaling (DOTS {{?I-D.ietf-dots-signal-channel}}) specification.

Two further extensions are now in completion: reducing the need for per-request state in clients and proxies {{?I-D.ietf-core-stateless}} (in IETF last call) and improving the security between multiple active requests {{?I-D.ietf-core-echo-request-tag}}, further reducing CoAP's exploitability in denial of service attacks (completed working-group last call).

# Security

Security has always been a critical enabler for IoT.  Similar to the way the HTTP web uses TLS, CoAP was kicked off with a security architecture based on Datagram TLS (DTLS), which provides high levels of security, but does not support end-to-end security in a configuration that includes proxies.
Object Security for CoRE (OSCORE) now provides end-to-end security over proxy paths that may include both CoAP and HTTP {{?RFC8613}}.

One interesting aspect of OSCORE is that it also supports group communication, as it occurs in multicasting requests to collect responses from a group of nodes.  CoAP has supported multicast requests from the outset, and {{?RFC7390}},
Group Communication on top of IP multicast, provides additional specfication for this.  As DTLS only supports unicast, without a security architecture RFC 7390 was published an experimental RFC.  Work is now underway to revise this  RFC {{?I-D.dijk-core-groupcomm-bis}}, which includes making use of the capabilities provided by OSCORE for group communication {{?I-D.ietf-core-oscore-groupcomm}}.  Work is now under way in the CoRE, ACE, and LAKE working groups to complement this basis with additional specifications making use of OSCORE and CoAP group communication.

# Operations and Management

IoT systems need to support a large number of nodes, which need to be configured and integrated into an IoT system.  A discovery and self-description architecture based on web links has been the first product of the WG {{?RFC6690}}, which is now being complemented by a registration and discovery function (CoRE Resource Directory {{?I-D.ietf-core-resource-directory}}, in IESG processing).

Constrained nodes also need management functions.  While many IoT SDOs are integrating these right into their IoT data format specifications, the IETF has its own architecture for describing management information, YANG {{?RFC7950}}.  The "CORECONF" specifications that are in Working Group Last Call (including YANG-CBOR {{?I-D.ietf-core-yang-cbor}}) make this widely used approach of providing management interfaces available in a highly efficient way that is applicable to constrained environments, as our complement to the established YANG protocols NETCONF and RESTCONF.

# Data Formats

While CoAP can be used with many different data formats, a simple CoRE format for sensor and actuator data, Sensor Measurement Lists (SenML), was defined in {{?RFC8428}}.  Recently, a number of specifications have been readied in support of SenML that are now undergoing final processing by the RFC editor:  Support for the RFC 8132 verbs {{?I-D.ietf-core-senml-etch}}, and modifications to the SenML units registry {{?I-D.ietf-core-senml-more-units}} that make it more accessible as a basis for data format standards of other Standards Development Organizations (SDOs).
A foundation for further data format specification that combines the web-linking approach of RFC 6690 with more modern data representation techniques is now being worked on under the name CoRAL {{?I-D.ietf-core-coral}}; application specifications such as CoAP pubsub {{?I-D.ietf-core-coap-pubsub}} are expected to pivot to this basis.

# Further Information

To follow and contribute to CoRE's work, please refer to the core status page (<https://tools.ietf.org/wg/core/>) and join the core mailing list: *core@ietf.org* via <https://www.ietf.org/mailman/listinfo/core>.

--- back

# Acknowledgements
{: numbered="no"}

Marco Tiloca provided comments on a draft of this document.

