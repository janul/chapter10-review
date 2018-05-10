# Multiparty Federation

"Information security is a fundamentally cooperative endeavor, one in
which responsibility and authority are distributed across a wide array
of actors." Ashwin J. Mathew

Federated identity protocols like SAML and OpenID Connect enable us to
authenticate people in other domains.  But trust issues quickly surface.
For example, if your organization operates a website with valuable
content, and someone you authenticated at another domain steals the
content, what recourse do you have? If your organization operates
an OpenID Provider, and a relying party website is hacked (potentially exposing
your account holder's personal information) do you expect to be notified? And
what rights do you have to update information at identity providers
or websites that you use? These related federated trust considerations are aptly
described by Scott David, a legal identity scholar, as the "triangle of trust."

![Figure 10 - Triangle of Trust](./assurance_protection_control.png)

Figure 10-1 conveys what type of trust is needed, and by whom. It uses
OpenID Connect vocabulary (OP, RP) but you could substitute the equivalent
SAML terms (IDP, SP). While you are most likely to hear about "Level of
Assurance" of an authentication, you are less likely to hear about the
"Level of Protection" or "Level of Control". But these trust considerations
are equally important.

Let's summarize for each vertex:

* Level of Assurance (LOA): The RP (website) needs assurance from the OP.  Is the
person who is the subject of the assertion really who they say they are? How
well did you identity proof this person? Did you check a state issued ID?
Did you verify with the issuer that the ID was valid? How well did you
authenticate the person? And how secure are your account recovery procedures?
The OP provides assurance, and is some cases liability protection, to the RP.
The assertion is only as good as the identity management and security practices
behind it.  

* Level of protection (LOP): The OP wants the website to protect the data.
Most RP's will write data to their database. Using
federated identity, RP's don't need the secret credentials (e.g. passwords),
but it is common for RP's to create a local account for each person to track
their history and preferences. Whether or not the person approved the release
of information explicitly or implicitly to the RP, most OP's expect a certain
amount of diligence with regard to the handling of shared PII. The RP should
adopt best practices for data security.

* Level of control (LOC): The person wants to update, remove or otherwise direct the
use of their data. Today people are demanding control of their data as a
human right. However, within an ecosystem, the concept of data ownership gets
murky fast, as a person can't necessarily demand the removal for their personal
information. For example, if an employee places an order, who's data is it? The
employee's? The buyer's? Or seller's?  Federation agreements can specify more
clearly what rights people have to control the use and accuracy of the data.

Our national, state, and international laws can't be relied on to
create a workable trust fabric. At best, they are a
patchwork of frequently outdated regulations, that tend to
inconsistently address issues of assurance, protection and control.
For example, in the US, the HIPPA regulations specify data must
be protected by encryption. Other government regulations are
proscriptive about assurance, but say nothing less about protection.
The EU GDPR regulations focus on giving the person more control
over their data--we don't have such protections in the U.S.

Two organizations can achieve trust by describing all the contingencies
in legal contracts. For example, the contract can specify acceptable
types of authentication, the procedure for breach notifications, and
obligations to update or remove a person's information upon their
request. However, in a large ecosystem with many companies, requiring
each pair of organizations to negotiate a bilateral agreement is not
efficient. Each organization would need n-1 agreements, where n is the
number of ecosystem participants.

A better approach is to define one standard contract that level sets
assurance, protection and control within the community. If each
federation participant signs a standard participant agreement,
one-off agreements can be greatly reduced.

Federations have existed for a long time. In government, a federation
describes multiple autonomous states ceding authority to a central entity. The
United States itself is "federal"--i.e. granted certain powers in the Constitution
by the states in the interest of efficiency. The Internet itself is a federation--
those connected agree to use IP addresses. Internet standards enable tcp,
udp, tls, http and other communication streams.

There are many existing industry federations. If you are a member
of a stock exchange, a sports league, or even a farming collective,
you decide that it's worthwhile to give up some autonomy to gain
efficiency in an ecosystem.

Information security federations define the **tools and rules** for trust.
The first identity federations improved connectivity. The EduRoam
higher education network enables reciprocal WiFi across participating
campuses. Higher education was also an early adopter of SAML federations.
In the U.S., InCommon (https://incommon.org) has approximately 1000 members:
700 universities and 300 web sites. InCommon also has an interfederation
agreement with eduGAIN. Government, defense, pharmaceutical
and automotive industries also have created supply chain SAML federations.

![Figure 10-2 - Federation and Interfederation trust](./hub_and_spoke_trust.png)

Federation "tools" are protocols, data structures and vocabularies.
Imagine how expensive it would be if every website used a different
identifier for first name and last name. InCommon specifies that
participants must support the eduPerson attributes. Beyond user claims,
identity federations could define standard vocabularies for authentication
mechanisms, OAuth scopes, and other custom schema.

Federation "rules" are the legal agreements that bind the parties
together. There are a few legal recipes for how to
accomplish this. The following recipe is for three agreements:
a "Federation Policy", which defines the top level governance; a
"Data Protection Code of Conduct", which defines not
just protection, but also privacy responsibility of
participants that hold data about people; and finally,
the "Network Use Agreement", which should be displayed
each time the person is authenticated at a participant.

Federations are not tied to specific protocols or technologies. Technical and
legal innovations are inevitable, and effective federations will evolve to
address new realities.

### Federation Policy

Does the federation have a steering committee? If so,
This document describes the governance of the federation.
how many members? Serving for how long? Voting in what
way? The Federation Policy should also define how
the federation is managed. Who will operate the day
to day services?  How should the federation  market itself
to drive more memberships? The Federation Policy covers
a few more important areas like disputes resolution, and
how an organization could become a participant. You
can find quite a few federation polices on the
Internet, as these are public documents, and most
large federation operators point you to them.

###  Data Protection Code of Conduct

With the intent of giving people more control of their data,
participants agree to a Data Protection Code of Conduct,
regarding the handling of personal information. The
federation can define the baseline expectations for consent,
notification and data protection. The document may
also detail the data retention period and the
rights of a person to access or rectify their data.

###  Network Use Agreement

Ultimately, the buck stops with people. End-users have to take
responsibility for their own security hygiene. That includes
taking the appropriate level of care to protect their credentials
from loss or compromise. The network banner, also informs the
person about their rights to correct information, to request
removal from a service, and sometimes where to direct questions at the
federation or participant.

## Federation Actors

As this is a book for geeks, not lawyers, back to the tools! Figure 10-3 shows
the actors that participate in an identity federation.

![Figure 10-3 - Federation Actors](./figure02-federation-actors.png)

* Registration Authority: trusted third party that operates the federation
technical infrastructure. For example, a hosting company, ISP, or
telecommunications provider.

* Federation Operators: the organization that makes the rules, specifies
the tools, and vets members. The federation should also perform due diligence
on the Registration Authority, as the federation is partially liable for
its operation.  

* Participant: An organization who is qualified to join a federation, and who
signs all the necessary legal agreements, and pays all fees.

* Entity: a service operated by a participant or the federation. Generally,
the service needs to register its cryptographic signing key with the federation,
and the web endpoints where its services can be found. It may also register
other information that is useful to publish centrally, for example to help
other participants or end users find or better utilize its service. It's
not uncommon for a participant to have several entities, for example, a
university may operate an SAML IDP and several websites.

## Joining a federation

A participant is born once an organization signs the necessary legal agreements,
and performs all the required duties, such as paying any fees.  The federations
vets the participant, and countersigns the documents. The participant
specifies administrative, legal and technical contacts, and shares its technical
configuration information, such as web endpoints and the public keys for each
of its services. This metadata about its services is filtered and published by
the federation. The federation may add additional configuration information,
such as whether the entity qualifies as a certain federation managed category--
e.g. the Research and Scholarship (R&S) category in the higher education
federation community.

## Federation Trust Models

In addition to the trust generated by the agreements on a shared set of rules,
multi-party federations also use technology to improve security.

The primary trust model used on the Internet today is SSL/TLS. We drill it into
people's heads: make sure the little green padlock icon is green! Browsers make
it really confusing for people to navigate to an https websites where the SSL
certificate is invalid. This trust model relies on the idea that the only
organization that controls a domain can get a certificate for that domain from
a well known certification authority--one that has its root certificate
installed in the browser. In general, this trust model works pretty well, but
it's not secure enough for certain organizations that need to mitigate more risk
then for the average ecommerce transaction.

In addition to SSL, SAML and OpenID Connect define mechanisms to sign and
encrypt identity assertions.  If you download the public keys via HTTPS, then
the trust model is still SSL/TLS. However, if the federation provides an
out-of-band, highly secure way for the participant to upload its public keys
to the federation operator, and the consumer of the identity assertion uses
the federation's copy of the public key, it adds security over SSL/TLS.
To forge the signature, the attacker would need to break into both the
participant, and the federation.

## SAML federations via metadata aggregate

SAML metadata allows for the description of multiple entities. A SAML
federation metadata aggregate is a big  file with all the entities
for all the participants. The federation signs this XML file with its
private signing key, and publishes it.

A metadata aggregate can get pretty big. Each entity publishes its public
certificates. There is also XML needed to describe the endpoints and other SAML
options. An already big metadata aggregate can get even bigger during
inter-federation, if one federation imports all the entities of another
federation.

For many SAML federations, publication of metadata is an automated process that
happens every five minutes or so. In terms of operations, the SAML federation metadata can be published as a flat file. This makes global distribution of the document easier, as the federation or registration authority needs no runtime infrastructure other then a web server. The metadata aggregate can just be copied to multiple data centers, enabling more robust deployments.

In SAML, both IDP and SP entities are treated similarly in the metadata. Both
are required to have a stable entityID, which is like a primary key--the
entityID must be unique in the metadata. It's a common convention to use the URL of the entity's metadata as the value for the entityID (a url is collision
resistant.) The other common convention is to use a URN as the value for the entityID. As mentioned above, the metadata published by the entity may or may
not be the same as the metadata published for that entity by the federation,
as the federation may add extra information about the entity to its aggregate.

There are a few drawbacks of the metadata aggregate approach:
 * The metadata aggregate is that it is hard to search. It's very flat, so inevitably, you need to iterate through all the entries (which can be very slow if you're parsing the XML at runtime).
 * Inter-federation does not scale well. A large file can get even bigger if you are including entities from another federation. The process of copying files,
 and perhaps transforming them to meet your federation's metadata conventions can be onerous.
 * As a rule of thumb, size is limited to a few thousand entities.

## Trustmarks

Most of this content is thanks to the Georgia Tech Research Institute (GTRI)
with the support of the National Strategy for Trusted Identities in Cyberspace
(NSTIC) via the National Institute of Standards and Technology (NIST).  
Standard disclaimer: "The views expressed do not necessarily reflect the
official policies of NIST or NSTIC; nor does mention by trade names, commercial
practices, or organizations imply endorsement by the U.S. Government."

Trustmarks enable organizations to convey security risks in a machine readable
format. A trustmark can be an assertion about anything! For example, technical
interoperability (e.g. vocabularies and protocols), LOA / LOP / LOC
considerations, or business. The legal aspects of trustmarks are conveyed not
through the trustmarks themselves, but via the trustmark policies and/or
trustmark agreements under which trustmarks are issued and used.

This kind of federation is potentially more efficient then a centralized
or "monolithic" federation.

![Figure 10- : Potential Cost Savings from a Trustmark Framework](./cost_savings_for_trust_marks.jpg)

The blue curve represents the growth of costs when establishing trust through
a series of pairwise (bilateral) trust relationships. This curve is linear,
because on average, each new pairwise relationship established requires roughly
the same amount of time and effort as was required for each previously
established relationship. This curve represents a worst-case scenario, and is an
unacceptable strategy for any ecosystem that wishes to establish more than a
trivial number of trust relationships with other organizations.

The red curve represents the growth of costs when establishing trust through
a series of traditional trust frameworks. The route of monolithic trust
frameworks tends to imply joining multiple monolithic trust frameworks over time.
The strategy of joining multiple monolithic trust frameworks does not scale as
poorly as the bilateral trust strategy discussed above; however, it is still
suboptimal. Since each new monolithic trust framework is opaque, it is unlikely
that a significant amount of the prior work, which was performed during the
process of joining previous monolithic trust frameworks, will be applicable
when joining the next monolithic trust framework.

The green curve represents the growth of costs when establishing trust through
a componentized trustmark framework in which individual trust components tend
to be reused between trust frameworks. In this scenario, joining a new trust
framework requires three steps.

* Determining which trustmarks are required by the new framework
* Determining which required trustmarks are already possessed, and which need
  to be acquired.
* Acquiring the necessary trustmarks that are not already possessed

Over time, as the organization seeks to join multiple componentized trust
frameworks, it is increasingly likely to already possess many or most (or all)
of the necessary trustmarks based on its previous efforts to join other trust
frameworks. This causes the cost growth curve to become flat, or nearly flat,
over time.

This analysis illustrates one of the most important benefits of trustmarks: not
only do trustmarks enable componentization and reuse of trust and
interoperability criteria, but they also carry the potential for significant
cost savings over time as the ecosystem grows to encompass many communities
that engage in a variety of cross-COI collaboration scenarios.

For more information on trust marks, including the trustmark XML specification,
a database of existing security trustmarks (many!), and lots of great
theoretical information, visit GTRI's trustmark page: https://trustmark.gtri.gatech.edu/

## OpenID federations

OpenID federations are moving in the direction as trustmarks toward a
componentized trust model. However, OpenID presents some unique challenges.
It starts with how entities are named. In SAML, both IDP's and SP's have an
entityID, which is a convenient way to reference them in a federation's
metadata. In OpenID Connect, it's a requirement that the OpenID Provider
publishes it's metadata (although they don't call it that) on a URL--the .well-known/openid-configuration endpoint. This aligns very well with SAML--we
can use that as the value to uniquely identify an OP in a federation.

However, what is the entityID for an OpenID RP? During OpenID dynamic client
registration, the OP issues a client_id. So the same client will have a
different client_id at each OP. One could argue that the `redirect_uri` is a
reasonable way to identify a client. However, you need to take into account
that `redirect_uri`, may be multi-value, and the RP may update it, so it's not
a great primary key. In OpenID Connect it would impossible to require an RP to
publish its metadata--OpenID supports mobile clients, and Javascript clients
that only exist as code in the person's browser. SAML doesn't have this problem
because it was designed to solve trust with server-side web applications
(excepting the ECP profile of SAML, which is esoteric.)

These changes have required new ideas for the OpenID Connect federation
specification, which does away with the idea of a federation aggregate, and
replaces it with a dynamic componentized trust model.

The OpenID Provider keys used to sign and encrypt assertions are rotated every
two days according to current best practices. That's a lot--SAML keys are
usually rotated every few months, or every year. One of the innovations of
OpenID federation is to introduce a stable signing key for the OP, the
location of which is published on the OpenID Provider discovery page.
The public signing keys are stored by the client, and provide additional trust
over TLS/SSL (after the key is retrieved). The  signing key is used to publish
a verifiable OpenID discovery document.

The other innovation introduced by the OpenID Connect federation spec is the
idea of metadata_statements, a kind of OAuth software statement, issued
by the federation. The technical mechanics of how metadata_statements
are created are somewhat complicated--it involves successive cryptographic
operations. Remember, an OAuth software statement is not what it sounds
like--it's actually a JSON document used by the client at registration like
a registration token. The metadata statement would be created by the developer,
and signed, then passed to the organization and signed, and then passed to the
federation and signed. In practice, it's a little complex, but perhaps with
adoption of this standard, the right tooling will evolve over time to make it
easier.

The OpenID Connect federation specification is still a draft at the time of
this book's publication. Software implementations are experimental.

## OTTO Federation

OTTO is a set of standards under development at the Kantara Initiative. OTTO
stands for the "Open Trust Taxonomy for federation Operators".  It is a set
of APIs for federation management, and an extensible JSON-LD vocabulary to
model federation data. Like the OpenID federation spec, it has no adoption by
current federations, and only one very early software implementation of the
API's.

OTTO addresses some of the weaknesses of existing SAML federations. The OTTO
API's standardize operation by the registration authority. How does a
participant join a federation? How to register or update an entity? How to
leave a federation?

OTTO API's provide a standard way to do these things. In SAML, federation
operators either wrote their own operational software, or used open source
software to manage federation data. Some federations offer participants no
automated interface--registration and updates happen via a manual process.
If federations become more common, consistency would offer more efficiency
to participants and operators alike.

OTTO APIs provide a query mechanism to obtain information from the federation.
While this comes at additional operational complexity--the federation operator
is no longer just copying a static file to a web server---hosting APIs has
become somewhat of a mainstream activity for organizations. And registration
authorities who specialize in hosting federations will certainly have the
technical capability.

One of the other goals of OTTO was to make inter-federation more scalable.
SAML's approach of copying the data from one federation to another is not
particularly effective. It results in large files, and raises challenges
around filtering the data, as the imported metadata may not align perfectly
with the metadata conventions of the federation that consumes it, and may need
to be transformed. The design of OTTO is to use linked data to enable
one federation to reference the data of another.

In addition to the API's, OTTO defines several JSON-LD vocabularies. The OTTO
core vocabulary defines the common denominator for registration authority,
federation, participant, entity, and schema. It also defines vocabulary
extensions for SAML and OpenID--the two most important initial
use cases. But it leaves open the possibility that new protocols and new
trust models will evolve, and that it can be extended to meet those new
requirements by supporting additional standard or even custom (industry
specific) vocabularies.

### OTTO API

The registration authority hosts the OTTO API, which consists of a number of
service endpoints.

* *Configuration endpoint* : Returns a json document describing the federation
services of the registration authority--basically the URLs of all the endpoints
described below. This is published as
`https://domain/optional-path/.well-known/otto-configuration`

* *Federation endpoint* : This is the workhorse endpoint. First it is used by
the registration authority to add, edit, and delete federations. It is
used by an organization that wants to sponsor a federation. The federation
uses this endpoint to add and remove participants. It is used by
participants to request to join or leave a federation. And finally, it can
be used by anyone to search public information about the hosted federations.

* *Participant endpoint* : This endpoint is used by federation software to
create a participant, lookup information about a participant, or otherwise
update a participant's data. It is also used to link a participant to
federations and entities. Lookup by reference id is supported.

* *Entity endpoint* : This endpoint is used by participant software to create,
update and delete entities and to link them to participants (who operate them)
or federations.  Lookup by reference id is supported.

* *Metadata endpoint* : This endpoint, hosted by the Registration Authority,
enables the management of metadata of the federation. The API requires
a `category` (e.g. OpenID or SAML), and allows optional parameters
metadataFormat and expiration. Metadata could be periodically downloaded
and published in the traditional way (i.e. copy to a bunch of servers.)
Or it can be handled more dynamically: perhaps software for a participant
will obtain a software statement or metadata statement on the fly.

* *Schema endpoint* : This endpoint, hosted by the registration authority,
enables the management of schema available to federations. The `category`
property is required. For example, the OpenID vocabulary defines
`UserClaim`, `Scope`, and `ACR` as values for schema category. Somewhat
circuitously, when you create a schema, you have to say if it's required.
For example, perhaps email address is a required user claim in certain
federations.  The schema endpoint enables software to view, create, and
update schema, and to link schema with an entity or federation. The endpoints
also enable lookup of a schema by id, and an endpoint to return all
available schema categories.

### OTTO vocabulary

JSON-LD 1.0 is a W3C specification, which can be found at
https://www.w3.org/TR/json-ld/. It is a lightweight syntax to serialize Linked
Data in JSON. Since JSON-LD is 100% compatible with JSON, you can use your
existing JSON tools and libraries. JSON is better for security. Compared with
XML, JSON is simpler, and parser developers are less prone to security snafus.

Although there are many good reasons to use JSON-LD, three features were
important to OTTO:

1. **Linking** You can refer to a JSON object in a different domain. Many of the
objects are related. For example, entities are operated by a participant, a
federation has participants, a registration authority operates federations.
This capability can reduce some of the data duplication and filtering challenges
in the current metadata aggregate approach.

1. **Extensibility** A JSON-LD class may be a subclass of another class, inheriting its properties. The OTTO Core Vocabulary defines building blocks, with which additional OTTO vocabularies can be built. For example SAML IDP and OpenID OP both use OTTO
Entity as a subclass. Future vocabularies may address UMA, ACE, PKI, and other protocols yet to be invented, and hopefully will not have to re-invent--just
supplement.

1. **Re-Use** OTTO used schema from https://schema.org as a starting point. This means
our vocabulary was almost complete--OTTO defines some additional vocabulary
for federation specific stuff. For example, in OTTO a participant is a subclass of
schema.org Organization,  http://schema.org/Organization.

![Figure 10- : Vocabulary Overview](./otto-schema-overview.jpg)

#### OTTO Core Vocabulary

All core OTTO classes have an `@id` and `name` property. The `@id` is a globally
unique identifier--a primary key used for linking data. The issuer of the
`@id` should either use a GUID algorithm or a hierarchical name space (such as
a url). The `name` property is a human readable identifier.  Following is a
summary of the information stored in each.

* **RA** - Subclass of schema.org/Organization. Contains the OTTO
  endpoint URI's (e.g. federation_endpoint, participant_endpoint). The
  `registers` property specifies the hosted federations.
* **Participant** - Subclass of schema.org/Organization. Entities are linked by the `operates` property. Federations are linked by the `memberOf` property.
Participant contact information can also be published here.
* **Entity** - Subclass of schema.org/Thing.  A technical service of a participant.
The `operates` property indicates the resource. The `operatedBy` and  
`federatedBy` properties specify the organization and federation links. The
`supports` property can be used to describe schema requirements, or to
publish trustmarks. The `category`property can be used by the federation to
group Entities to faciliate trust management (e.g. R&S websites).
* **Federation** - Subclass of schema.org/Organization. The `member` and
 `federates` property links participants and entities respectively. The
 `metadata` property specifies the federation's public keys, certificates
 and other cryptographic information to enable verification of federation
 assertions, and encrypted communication. The `sponsor` property specifies
 the Organization responsible for governance. Federation contact information
 and legal agreements can be listed. The federation can use the `supports`
 property to publish schema standards, like user claim identifiers (e.g.
 givenName or first_name?), and trustmarks (as mentioned in the section above).
* **Metadata** - Subclass of schema.org/Thing. This class specifies its
`metadataFormat`, `expiration` and `category` (e.g. OpenID or SAML).
OTTO extension vocabularies (like OpenID and SAML) subclass metadata,
adding the necessary details for their protocols.
* **Schema** - Subclass of schema.org/Thing. Also uses the `category`
property to group schema (e.g. "user_claims", "scope"). The `required`
boolean can be used by an Entity, e.g. an SP might require the
email address attribute. The `sameAs` property can be used to
link Schema to eliminate overlap.

### OTTO Next

OTTO is still under development at the Kantara Initiative. You can read the
draft specifications, meeting minutes, and visit the test site:
* OTTO Github: https://github.com/KantaraInitiative/wg-otto
* OTTO API's: https://gluu.co/otto-api
* Core Vocabulary: https://gluu.co/otto-vocab
* OpenID Vocabulary: https://gluu.co/otto-openid
* SAML Vocabulary: https://gluu.co/otto-saml
* Swagger Demo site (not guaranteed to be up!): http://otto-test.gluu.org/swagger/

## Jagger

Developed by HEAnet to manage the Edugate multiparty SAML federation.
in Ireland, Jagger is an easy to deploy and operate federation management
platform that provides a website for participant administrators to join and
update a federation, and for federation administrators to approve and publish
SAML metadata. One of the nice features is that it supports the management of multiple federations, making it an excellent choice for a registration authority. The following figures show some of the screen shots from Jagger's website, which you can find at https://jagger.heanet.com

![Figure 10- : screenshot](./jagger-idp-list.png)

## Federation Registry

Developed by the Australian higher education federation, Federation Registration
is a java platform for hosting a single federation. Features:

* A focus on organizations as the key building block for the federation
* Allows for organizations to be service providers only
* A personalised dashboard view of the federation for all users
* A highly refined, multi-browser, HTML5 compliant user interface
* The user interface is fully themeable to suit the look and feel of your organization
* Multilingual capable out of the box
* Management for all aspects of SAML 2 compliant Identity and Service Providers
* SAML 2.x compliant metadata generation
* Additional assistance for Shibboleth IDP and SP administrators including automated Attribute Filter generation
* Public registration for organizations, Identity Providers and Service Providers that are new to the federation
* A fully customisable workflow engine to handle registrations and other critical federation changes
* Compliance reporting to gain insight to various areas of your federation
* A hand crafted model of the entire SAML 2 metadata specification for use in automated object relational mapping
* Federation integrated, automatically provisioned user accounts with fine grained access control

![Figure 10- : screenshot](./FR2-screenshot.png)

## OTTO-Node / Fides

Fides is a web application that enables a person to register, then register an
organization, and apply to become a member of the federation. It includes
enrollment of an OpenID Provider, using the discovery features of OpenID
Connect. A federation administrator manually approves membership applications.

This project included support for creation of "badge assertions", which
is a JSON-LD data structure defined in the Open Badges 2.0 specification,
which can be found at https://gluu.co/open-badges-2-0. In our pilot, we were
using badges to convey professional training and certifications that were
specific to the emergency responder community. The fides federation admin can
authorize an organization to issue certain types of badges.

Fides also calls the OTTO API's--for example when a federation admin approves
a new participant, Fides calls the OTTO federation endpoint to make the link.

This software, a part of the ERASMUS project, has been funded in part by the United States Department of Homeland Security's Science and Technology Directorate. The content of this book does not necessarily reflect the position or the policy of the U.S. Government and no official endorsement should be inferred. All the code is transparent and free open source. Fides and OTTO Node code can be found in Gluu's github repository: https://github.com/GluuFederation/otto-node
https://github.com/GluuFederation/erasmus/tree/master/FIDES

![Figure 10- : screenshot](./![Figure 10- : screenshot](./fides-federation.png))
