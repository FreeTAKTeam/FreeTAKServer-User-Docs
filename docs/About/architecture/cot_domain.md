
# **CoT Domain Model**

The Cursor-On-Target (CoT) Event data model defines a Domain model
as a system of abstractions that describes selected aspects
of a sphere of knowledge for the TAK domain.
It is represented as a platform-independent model (PIM)
that is independent of the specific technological platform used to implement it.
The Domain model can be translated into an XML data schema
for exchanging time sensitive position of moving objects,
or "what", "when", and "where" (WWW) information, between systems.

![FTS CoT domain Model](https://user-images.githubusercontent.com/60719165/193834333-ea041722-e3ea-46f9-9eb6-7417c19807ea.png)


## \_\_serverdestination 

The destination of a certain message.
Indicates how to communicate back to the sender.

### \_\_serverdestination attributes

| **Name**      | **Documentation**                                                                                 |
|:--------------|---------------------------------------------------------------------------------------------------|
| destinations  | string composed by IP:port:protocol:machineID.<br>e.g. 192.168.0.103:4242:tcp:ANDROID-R52JB0CDC4E |

## \_flow-tags\_

This is a Cursor On Target detail class that holds "fingerprints" of the system that have processed a particular CoT event.
This information aids in the routine of CoT messages along a particular processing chain.
Each system that touches a particular CoT event is expected to add its own attribute to this entity.
The attribute name should reflect the particular system name,
and the value should be the time stamp when the information was sent out from that system.
Some illustrative \_flow-tags_ attributes are adocs, fbcb2, and tadilj, but the attribute list is not a closed set.

### \_flow-tags\_ attributes

| **Name**   | **Documentation**  |
|:-----------|:-------------------|
| version    |                    |
| adocs      |                    |
| fbcb2      |                    |
| tadilj     |                    |

## \_medevac\_

the medevac class is used to describe a case of someone in need to be evacuated

### \_medevac\_ attributes

| **Name**             | **Documentation**  |
|:---------------------|:-------------------|
| litter               |                    |
| freq                 |                    |
| terrain_none         |                    |
| zone_prot_selection  |                    |
| Title                |                    |
| Priority             |                    |
| medline_remarks      |                    |
| Security             |                    |
| routine              |                    |
| equipment_none       |                    |
| hlz_marking          |                    |
| casevac              |                    |
| urgent               |                    |

## \_radio  


### \_radio attributes

| **Name**  | **Documentation**  |
|:----------|:-------------------|
| rssi      |                    |
| gps       |                    |

## Attitude 


### Attitude attributes

| **Name**  | **Documentation**  |
|:----------|:-------------------|
| roll      |                    |
| pitch     |                    |
| yaw       |                    |

## chat

Class that holds information regarding chat.
When communicating with a group,
the **\_\_chat** attributes specify the unique ID of the chat group,
and the common name as to be read by the user.
The recipient, upon receipt, will see that these fields do not match their information,
and create the appropriate group.
Members will be populated from the attributes of the **chatgrp** element.

 ### chat attributes

| **Name**        | **Documentation**                       |
|:----------------|:----------------------------------------|
| senderCallsign  | the call sign of the sender             |
| chatroom        | TBD: the callsign of the receiver?      |
| groupOwner      | TBD,                                    |
| id              | TBD: the unique ID of the sender?       |
| parent          | the group where this chat is attached   |

## chatgrp

Class hosting IDs regarding the from and to

### chatgrp attributes

| **Name**  | **Documentation**             |
|:----------|:------------------------------|
| uid0      | the machine ID of the sender  |
| uid1      | another ID                    |
| id        | third ID                      |

## ** checklist**

  


1. ### ** checklist attributes**


9. ## ** checklistColumn**

  


1. ### ** checklistColumn attributes**

| **Name**    | **Documentation** |
| ----------- | ----------------- |
| columnName  |                   |
| columnType  |                   |
| columnWidth |                   |

10. ## ** checklistColumns**

  


1. ### ** checklistColumns attributes**


11. ## ** checklistDetails**

  


1. ### ** checklistDetails attributes**

| **Name**     | **Documentation** |
| ------------ | ----------------- |
| name         |                   |
| uid          |                   |
| description  |                   |
| startTime    |                   |
| templateName |                   |

12. ## ** checklistTask**

  


1. ### ** checklistTask attributes**

| **Name**        | **Documentation** |
| --------------- | ----------------- |
| value           |                   |
| status          |                   |
| completeDTG     |                   |
| notes           |                   |
| dueRelativeTime |                   |

13. ## ** checklistTasks**

  


1. ### ** checklistTasks attributes**


14. ## ** color**

  


1. ### ** color attributes**

| **Name** | **Documentation**              |
| -------- | ------------------------------ |
| argb     | integer with a colore.g. 65536 |
| value    |                                |

15. ## ** contact**

This is a Cursor On Target Class representing communications parameters for contacting a friendly element for human-to-human communications. The objective of this Class is to carry the essential information needed to contact this entity by a variety of means. Multiple ways of establishing contact can be specified;

noThe attributes callsign, phone, and email should be self-explanatory. particular mode of contact is required. Other attributes, freq, dsn, modulation, and hostname, are also available.

1. ### ** contact attributes**

| **Name**     | **Documentation**                                                                                                                                                                                                             |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| iconsetpath  |                                                                                                                                                                                                                               |
| callsign     | The unit's voice call sign                                                                                                                                                                                                    |
| freq         | The frequency (in MHz) on which the unit may be contacted via voice.                                                                                                                                                          |
| email        | e-mail address for this element (if applicable)                                                                                                                                                                               |
| endpoint     | TBD                                                                                                                                                                                                                           |
| dsn          | DSN number for this element (if applicable)                                                                                                                                                                                   |
| phone        | Phone number for this element (if applicable)                                                                                                                                                                                 |
| modulation   | Amplifies the radio frequency information provided. Contains the modulation type for the communication. (Coding tbd, should cover complex modulations such as SINCGARS hopping, csma, etc...) am\|fm                          |
| hostname     | DNS-resolvable host name                                                                                                                                                                                                      |
| version      | Version tag for this sub schema. Necessary to ensure upward compatibility with future revisions.                                                                                                                              |
| xmppUsername | user name in the xmpp network. A private, unique, and memorable "petname" or "alias" assigned by a contact to a user; represented in the 'name' attribute of the item associated with that user's JID in the contact's roster |

16. ## ** contentResource**

  


1. ### ** contentResource attributes**


17. ## ** CoT**

The Cursor-On-Target (CoT) Event data model defines an XML data schema for exchanging time sensitive position of moving objects, or "what", "when", and "where" (WWW) information, between systems.

1. ### ** CoT attributes**

| **Name**  | **Documentation** |
| --------- | ----------------- |
| Identity  |                   |
| dimension |                   |
| entity    |                   |
| type      |                   |
| lat       |                   |
| lon       |                   |
| uid       |                   |

18. ## ** creatorUid**

  


1. ### ** creatorUid attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

19. ## ** dest**

  


1. ### ** dest attributes**

| **Name** | **Documentation**                |
| -------- | -------------------------------- |
| callsign | the call sign of the destination |

20. ## ** detail**

An optional element used to hold CoT sub-schema. Detail has no special properties.

**Detail entities...**

The "detail" entity is intended to carry information that is specific to smaller communities of producers and consumers and require more intimate knowledge of the operating domain. For example, mensurated "target" events may come from dramatically different sources and need to propagate dramatically different "detail" information. A close-air-support mission will augment target details with initial point and callsign details to facilitate coordination of weapon delivery. In contrast, a

mission planning system may augment planned targets with target catalog information and weapon fuzing requirements.

Because the "details" portion of the event are of interest only to a subset of subscribers, that entity may be mentioned by reference when the event is communicated. This reduces the congestion when events are transmitted over bandwidth limited links and also prevents the retransmission of static data elements.

1. ### ** detail attributes**


21. ## ** DimensionTypes**

  


1. ### ** DimensionTypes attributes**

| **Name**          | **Documentation** |
| ----------------- | ----------------- |
| space             |                   |
| air               |                   |
| land-unit         |                   |
| land-equipment    |                   |
| land-installation |                   |
| sea-surface       |                   |
| sea-subsurface    |                   |
| subsurface        |                   |
| other             |                   |

22. ## ** DJI**

A class to handle DJI Drones

1. ### ** DJI attributes**

| **Name**    | **Documentation** |
| ----------- | ----------------- |
| spoiuid     |                   |
| homelat     |                   |
| gimbalroll  |                   |
| gimbalpitch |                   |
| homelon     |                   |
| gimbalyaw   |                   |

23. ## ** dxf**

This is a hook for an arbitrary 3D DXF description of a volume of space.

1. ### ** dxf attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| level    | "level" is used to indicate the preferred ordering of multiple shape sub-schemas. For instance, if a polyline and ellipse are both present on the shape attribute, the one with the higher level value will be the "more desirable" representation of the object. This allows producers to provide alternative representation of an objects shape while ensuring that consumers will know which of the available representation is the best. (Note that not all consumers will implement all shape variations, hence the need for the allowing multiple shape objects.)See the documentation for shape/ellipse/@level for remarks on determining the precedence order when level values are equal or are missing. |

24. ## ** dxf**

  


1. ### ** dxf attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| level    | "level" is used to indicate the preferred ordering of multiple shape sub-schemas. For instance, if a polyline and ellipse are both present on the shape attribute, the one with the higher level value will be the "more desirable" representation of the object. This allows producers to provide alternative representation of an objects shape while ensuring that consumers will know which of the available representation is the best. (Note that not all consumers will implement all shape variations, hence the need for the allowing multiple shape objects.)See the documentation for shape/ellipse/@level for remarks on determining the precedence order when level values are equal or are missing. |

25. ## ** ellipse**

The "ellipse" is a common shape abstraction used by many geomanipulation applications; it is supported natively

1. ### ** ellipse attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| major    | Ellipse major axis (meters)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| minor    | Ellipse minor axis (meters)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| angle    | Orientation of major axis with respect to true north.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| level    | "level" is used to indicate the preferred ordering of multiple shape sub-schemas.For instance, if a polyline and ellipse are both present on the shape attribute, the one with the higher level value will be the "more desirable" representation of the object. This allows producers to provide alternative representation of an objects shape while ensuring that consumers will know which of the available representation is the best. (Note that not all consumers will implement all shape variations, hence the need for the allowing multiple shape objects.)Since the level attribute is optional, it is necesary for precedence rules to exist to ensure all consumersprocess the shape definition the same way.1. The shape definition with the highest value level attribute is considered the most accurate interpretation. 2. If all shape definitions specify the same level, the order from least to most accurate interpretation is presumed to be ellipse, polyline, dxf. 3. A shape that specifies the level attribute has precedence over any that do not specify it. 4. If the level attribute is absent from all shape definitions, the order from least to most accurate interpretation is presumed to be ellipse, polyline, dxf. |
| extrude  | A "Height" of the ellipse used to make the flat object encompas a volume.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

26. ## ** emergency**

An emergency beacon the is continually send to all the connected clients until deactivated from the original creator

1. ### ** emergency attributes**

| **Name** | **Documentation**                           |
| -------- | ------------------------------------------- |
| type     | default constructor def \_\_init\_\_(self): |
| Alert    |                                             |
| cancel   | if true the emergency beacon is canceled    |

27. ## ** EntityTypes**

  


1. ### ** EntityTypes attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| military |                   |
| civilian |                   |

28. ## ** environment**

  


1. ### ** environment attributes**

| **Name**      | **Documentation** |
| ------------- | ----------------- |
| temperature   |                   |
| windDirection |                   |
| windSpeed     |                   |

29. ## ** Event**

represents a TAK event: this class is instantiated with a standard set of values.

The opex field is intended to indicate that the event is part of a live operation, an exercise, or a simulation. For backward compatibility, absence of the opex indicates "no statement", which will be interpreted in an installation specific manner.

opex="o-&lt;name>" or "e-&lt;nickname>" or "s-&lt;nickname>",

where "-&lt;name>" is optional. That is, it is permissible to specify only "o", "e", or "s" for the opex value.

- o = operations
- e = exercise

s = simulation

1. ### ** Event attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| how      | Gives a hint about how the coordinates were generated. It is used specifically to relay a hint about the types of errors that may be expected in the data and to weight the data in systems that fuse multiple inputs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| version  | Schema version of this event instance (e.g. 2.0)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| time     | time stamp with respect to Zulu time indicating when an event was generated in extended ISO 8601 formatin ProtoBuff expressed is in milliseconds                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| type     | Event.type contains the Code for the Center on Target object. It Defines what the Event is about. An event may describe a physical object, a set of raw, unprocessed bits, or a tasking.\# Hierarchically organized hint about event type (**default**is 'a-f-G-I' for "Friendly Ground infrastructure)The "type" attribute is a composite of components delimited by the semi-colon character. The first component of this composite attribute is defined below.Future versions of this schema will define other components which we expect will aid in machine filtering. Despite the exclusion of definitions for additional components in this version of the schema, users of this schema should expect and design an optional trailing field delimited by the semi-colon character. This field can be ignored.- _component1_;optional fieldThe first component (component1) is a hierarchically organized hint about type.The intention is that this hierarchy be flexible and extensible and facilitate simple filtering, translation and display. To facilitate filtering, the hierarchy needs to present key fields in an easily parsed and logical order. To facilitate this, this component is a composite of fields separated by the "-" punctuation character, so a valid type would be: x-x-X-X-x. Using a punctuation for field separation allows arbitrary expansion of the type space,_e.g., a-fzp-mlk-gm-..._Field meanings are type specific. That is, the third field of an "atom" type may represent air vs. ground while the same field for a "reservation" type may represent purpose.**MEANING of 'a' in the first position**The "Atoms" portion of the type tree requires some additional explanation past the taxonomy defined below. The "Atoms" portion of the type tree contains CoT defined fields and part of the**MIL-STD-2525**type definition.To distinguish MIL-STD-2525 type strings from CoT defined fields, the MIL-STD-2525 types must be represented in all upper case. Differentiation of type namespace with upper/lower case facilitates extension of CoT types and MIL-STD-2525 types without name space conflict. An example:a-f-**A-B-C**-x- a = Atom - f = attitude or disposition (friendly in this case)- A-B-C =the SDIC 2525 separated by dashs - x = COT specific extensionThe organization of CoT and MIL-STD-2525 types can be determined from the taxonomy below, but additional details are provided here.The "Atoms" portion of the "type" tree contains the "Battle Dimension" and "Function ID" fields taken from MIL-STD-2525."Battle Dimension" is a single character taken from MIL-STD-2525 and is located in the position 5.a-.-**G**-I-M-N-B- P - Space - A - Air - G - Ground - S - Sea Surface - U - Sea Subsurface - SF - Special Operations ForcesThe typical 2525 representation for "Function ID" is three groups of two characters separated by a space (e.g. "12 34 56"). The CoT schema maps this to a "-" delimited list of characters. (e.g. "1-2-3-4-5-6").The concatenation of the "Battle Dimension" and "Function ID" fields from the MIL-STD-2525 specification represented in the CoT schema will be as follows:battle dimension-func id char1-func id char2- ... -func id char6When an appropriate MIL-STD-2525 type exists, it should be used. If there is a MIL-STD-2525 representation which is close, but may be refined, a CoT extension to the 2525 type can be appended.for example:a-h-X-X-X-X-X-**i** might represent hostile MIL-STD-2525 type X-X-X-X-X of  **Israeli**(the 'i'**)**manufacture. Again, the CoT extension uses lower case.Conceptually, this extension defines further branching from the nearest MIL-STD-2525 tree point.If no appropriate 2525 representation exists, a type definition can be added to the CoT tree defined here. The resulting definition would be represented in all lower case. For examplea-h-G-p-imight define atoms-hostile-Ground-photon cannon-infrared.The taxonomy currently looks like this: Note that the coding of the sub fields are determined entirely by the preceding fields!) The current type tree is defined here.**+--- First position, this event describes**- a - Atoms - this event describes an actual "thing"**+--- 2nd CoT affiliation of these atoms**- ****p - Pending - u - Unknown - a - Assumed friend - f - Friend - n - Neutral - s - Suspect - h - Hostile - j - Joker - k - Faker - o - None specified - x - Other**+--- Battle dimension****\| Taken from MIL-STD-2525 "Battle Dimension" (upper case)**- P - Space- A - Air - G - Ground - S - Sea Surface - U - Sea Subsurface- SF - Special Operations Forces**+--- Function (dimension specific!)******_See MIL-STD-2525B specification for function fields (must be upper case)_Any number of char before the first "dash", it express also the hierarchy(Hundreds of options)**+--- The event describes ...********b - Bits**- Events in the "Bit" group (pos 1163++ ) carry meta information about raw data sources. For example, range-doppler radar returns or SAR imagery represent classes of information that are "bits". However, tracks derived from such sources represent objects on the battlespace and this have event type "A-..."The intention with the "Bit" type is to facilitate the identification of germane information products.This hierarchy is not intended to replace more detailed domain-specific meta information (such as that contained in NITF image headers or the GMTI data formats), rather it is intended to provide a domain-neutral mechanism for rapid filtering of information products.**+--- Dimension**second position, Like battle dimension but for 'b' types- i - Imagery1. e - Electro-optical 2. i - Infra red 3. s - SAR 4. v - video- ... - r - Radar1. m - MTI data- ... - d - Sensor detection events1. s - Seismic 2. d - Doppler 3. a - Acoustic 4. m - Motion (e.g., IR)- m - Mapping1. p - Designated point (rally point, etc.) 2. i - initial points 3. r - rally points 4. ...**r - Reservation/Restriction/References**Events in this category are generally "notices" about specific areas. These events are used for deconfliction and conveyance of significant "area" conditions. Generally, the "point" entity will describe a conical region that completely encloses the affected area. The details entity will provide more specific bounds on precisely the region affected.- u - Unsafe (hostile capability) - o - Occupied (e.g., SOF forces on ground) - c - Contaminated (NBC event) - c - chemical - x - agents, direction, - y - z - f - Flight restrictions**t - Tasking (requests/orders)**Events in this category are generalized requests for service. These may be used to request for data collection, request mesuration of a specific object, order an asset to take action against a specific point. Generally, the "details" entity will identify the general or specific entity being tasked.- s - Surveillance - r - Relocate - e - Engage - m - Mensurate**c - Capability (applied to an area)**- s - Surveillance - r - Rescue - f - Fires - d - Direct fires - i - Indirect fires - l - Logistics (supply) - f - Fuel...**c - Communications** |
| stale    | The "stale" attribute defines the ending time of the event's validity interval. The start and stale fields together define an interval in time.It has the same format as time and start.ending time when an event should no longer be considered valid l (with respect to Zulu time in extended ISO 8601 format)In protobuff is in milliseconds                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| uid      | The "uid" attribute is a globally unique name for this specific piece of information.Several "events" may be associated with one UID, but in that case, the latest (ordered by timestamp),overwrites all previous events for that UID.can have additional information attached.\[EventTYPE].\[MACHINESENDERID].Nichname.UniqueIDe.g. -_ping_means that this event is a ping,_GeoChat_indicates a chat type structure.The**UID** should be in the following format: GeoChat.&lt;sender uid>.&lt;recipient callsign or name of the group>.&lt;random string for uniqueness>. Diverging from this format should not cause significant issues; however, the UID is used as a fallback if other information cannot be parsed from the message, so issues may still be experienced. If uid does not contain any "." characters, the chat room will default to "All Chat Rooms".GeoChat.ANDROID-7C:91:22:E8:6E:4D.DIPPER.44bf77cd-289e-4ea4-8756-ce295de168ca                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| start    | format - DTGThe "start" attribute defines the starting time of the event's validity interval. The start and stale fields together define an interval in time.It has the same format as time and stale.starting time of the event's validity interval (with respect to Zulu time in extended ISO 8601 format). As different from the moment in which the element was generatedin protobuff this is expressed in milliseconds                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| access   | Specifies access controls that should be applied to the event                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| opex     | OPTIONAL: Specifies whether the event is part of a live operation, an exercise, or a simulation.The access field is intended to indicates who has access to this event. (e.g. unrestricted, nato, army, coalition...)It is currently defined as a string, and is optional in V2.0.Future version of the event schema will provide formal definition of this field.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| cot2525  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| qos      | OPTIONAL: Specifies a quality of service desired from applications processing or routing the event                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

30. ## ** filename**

  


1. ### ** filename attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

31. ## ** fileshare**

  


1. ### ** fileshare attributes**

| **Name**       | **Documentation** |
| -------------- | ----------------- |
| filename       |                   |
| name           |                   |
| senderCallsign |                   |
| senderUid      |                   |
| senderUrl      |                   |
| sha256         |                   |
| sizeInBytes    |                   |

32. ## ** fillColor**

  


1. ### ** fillColor attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| value    |                   |

33. ## ** FilterGroup**

the name of the group authorized to see the CoT

1. ### ** FilterGroup attributes**


34. ## ** group**

  


1. ### ** group attributes**

| **Name** | **Documentation**      |
| -------- | ---------------------- |
| role     |                        |
| name     |                        |
| uid      | unique ID of the group |

35. ## ** hash**

  


1. ### ** hash attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

36. ## ** Health**

this class contains information regarding the current physical status of a connected user, measured with sensors.

1. ### ** Health attributes**

| **Name**  | **Documentation** |
| --------- | ----------------- |
| heartRate |                   |
| steps     |                   |
| stress    |                   |

37. ## ** Hierarchy**

  


1. ### ** Hierarchy attributes**


38. ## ** IdentityTypes**

  


1. ### ** IdentityTypes attributes**

| **Name**       | **Documentation** |
| -------------- | ----------------- |
| pending        | pending           |
| unknown        | unknown           |
| friend         | friend            |
| neutral        |                   |
| hostile        |                   |
| assumed-friend |                   |
| suspect        |                   |
| joker          |                   |
| faker          |                   |

39. ## ** image**

This is a Cursor On TargeClass for abstract image product metadata. It is specifically limited to geographically located (though not necessarily geographically registered) image products.

It is not intended to contain all the meta data typically found in the NITF header associated with such images, but rather provides sufficient "hints" about the ISR product to facilitate collection queuing and ipl searching. Full meta data will reside in the NITF header or other IPL-specific schemas.

This class borrows from the NITF standard. Note, also, that this class presumes is is contained within a CoT Evebnt element which provides information about center poiint, etc. Similarly, the CoT_shape schema can be used to delimit the bounds of the image. Furthermore, this element may conatin a base64 encoded image file. In this case, the 'mime' attribute should indicate the image type.

1. ### ** image attributes**

| **Name**      | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type          | Image type, drawn from NITF specification. E.g., SL - side-looking radar, TI - thermal infrared, FL - forward looking infrared, RD - radar, EO - electro-optical, OP - optical, HR - high resolution radar, HS - hyperspectral, CP - color frame photography, BP - black/white frame photography, SAR - synthetic aperture radar, SARIQ - SAR radio hologram, IR - infrared, MS - multispectral, ...                                                                                                                                                                                                                                                                                                                     |
| georegistered | (DEPRECATED) True if this image has been properly geo-registered                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| source        | (REVISED) The source of this image, specifically the CoT UID of the producer. (The intention is to indicate equipment type used to collect imagery, not organization owning image.)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| resolution    | Image product resolution (expressed in meters per pixel)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| url           | URL link to image if the image is not embedded                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| version       | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| size          | Approximate image file size (bytes)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| analysis      | (DEPRECATED) True if image analysis (e.g., markup) is available                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| mime          | If an in-lined image is contained in this entity, then this attribute describes the mime type of that image. The actual image data will be base64 encoded. See http&#x3A;//www.w3schools.com/media/media_mimeref.asp for list of common mime types.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| width         | The width of the image (in pixels)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| height        | The height of the image (in pixels)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| reason        | (NEW) The reason this image was originally produced (BHA, BDA, ISR, ...) Coding is TBD but will reflect the CoT type coding structure. E.g., a-d-b Assesment-Damage-Bomb, etc...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| bands         | Number of data bands within the image. For example, an RGB image as 3 bands (Red, Green, Blue bands/channels)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| mimecsv       | Used only if the attribute 'mime' references a container type (e.g., image/x-nitf21). In this case, 'mimecsv' holds a list of Comma Separated Values to supplement the MIME type in the mime field. Nominally, the values in 'mimecsv' wil lbe mime types of the elements in the composite image. For example, if 'mime' 'image/x-nitf21', then 'mimecsv' may hold 'image/jpeg', 'image/jpeg2000', or 'image/x-eagleeye'.                                                                                                                                                                                                                                                                                                |
| quality       | This expresses how the tradeoff between image quality and compression were made for this image. This is usually a 'relative' quality measure, an unsigned floating point value between 0.0 (highest compression) and 1.0 (highest quality). Implementers should attempt to map this scalar value to an approximate linear progression of visual quality as determined on a typical sample image. If the field's value carries an explicit sign (+/-) including +0 or -0, it represents the exact value expressed in a range appropriate to the compression type expressed in 'mime' or 'mimecsv'. For example, with 'image/x-eagleeye' the EagleEye clip setting, the quality setting may range from -4096.0 to +4096.0. |

40. ## ** Input**

this class can drive input filtering without auth messages.

1. ### ** Input attributes**

| **Name** | **Documentation**                                                                                                  |
| -------- | ------------------------------------------------------------------------------------------------------------------ |
| name     |                                                                                                                    |
| Protocol |                                                                                                                    |
| Port     |                                                                                                                    |
| auth     | Previously the only valid value for the &lt;input> "auth" attribute was "ldap". "file" is now another valid value. |

41. ## ** keywords**

  


1. ### ** keywords attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

42. ## ** labels_on**

  


1. ### ** labels_on attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| value    |                   |

43. ## ** link**

This is a Cursor On Target Class for linking to either another CoT event or an arbitrary Internet resource. The objective of this class is to provide an abstract way to express a relationship between a CoT object and other object. This allows, for example, a sensor point of interest to be linked back to its source, or a PPLI from a wingman to be associated with his flight lead. Linkages are always unidirectional.

One entity may have multiple links (i.e., it may be related to multiples other entities). For processing simplicity, it is required that the relationship graphs will directed and acyclic (no cycles). The link, itself, names the relationship (using a hierarchy similar to the CoT type), the UID of the related object (whether CoT or not), possibly provides a URL for retrieving that object.

links are used for example in routes.

1. ### ** link attributes**

| **Name**        | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| uid             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| production_time | the time in which this link has been produced (e.g. "2020-11-26T14:19:02Z")                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| relation        | The type of relationship (e.g, subject, object, indirect object) that this link describes. This is a hierarchy much like the event type field.Common values: "c"                                                                                                                                                                                                                                                                                                                                               |
| type            | The CoT type of the referenced MIL 2525 object. This is included because it is generally the key item needed in a tasking. Common types are:- **Control Point:** "b-m-p-c" - **Waypoint**: "b-m-p-w"                                                                                                                                                                                                                                                                                                           |
| url             | If present, this is a URL through which the linked object can be retrieved. If the URL is missing, then the object should be a periodic message (e.g., blue force track) that can be read from a CoT stream.                                                                                                                                                                                                                                                                                                   |
| parent_callsign | the call sign of the client that produced this link                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| remarks         | Remarks associated with this link.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| mime            | Internet Media type of the referenced object. If the link is to a CoT event, the mime attribute is optional and its type may be application/xml or text/xml as described in RFC 3023, "XML Media Types", or the unregistered type, application/cot+xml. If the link is to an arbitrary resource, the mime attribute is required and and appropriate Internet media type must be specified. Registered media types are managed by the IANA and are listed at http&#x3A;//www.iana.org/assignments/media-types/. |
| version         | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions.                                                                                                                                                                                                                                                                                                                                                                                                              |
| point           | location of a point in Format: "Lat,Lng" decimal values. e.g.38.843641314210366,-77.04564214131744                                                                                                                                                                                                                                                                                                                                                                                                             |

44. ## ** Marti**

Messages sent through the TAK server require an additional element to assist the server with properly routing your messages. If this element is not included, the server will interpret this as a message to all recipients, and the message will be sent to everyone, and depending upon the client software, this could mean a private message would be displayed publicly.

1. ### ** Marti attributes**


45. ## ** mimeType**

  


1. ### ** mimeType attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

46. ## ** mission**

  


1. ### ** mission attributes**

| **Name**  | **Documentation** |
| --------- | ----------------- |
| type      |                   |
| tool      |                   |
| name      |                   |
| authorUid |                   |

47. ## ** Mission**

Represent a TAK Mission

1. ### ** Mission attributes**

| **Name**    | **Documentation** |
| ----------- | ----------------- |
| name        |                   |
| server      |                   |
| description |                   |

48. ## ** MissionChange**

  


1. ### ** MissionChange attributes**


49. ## ** MissionChanges**

  


1. ### ** MissionChanges attributes**


50. ## ** missionName**

  


1. ### ** missionName attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

51. ## ** name**

  


1. ### ** name attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

52. ## ** point**

  


1. ### ** point attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| lat      | Latitude referred to the WGS 84 ellipsoid in degrees                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| lon      | Longitude referred to the WGS 84 in degrees                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ce       | Circular area around the point defined by lat and lon fields in meters. Although named ce, this field is intended to define a circular area around the event point, not necessarily an error (e.g. Describing a reservation area is not an "error").If it is appropriate for the "ce" field to represent an error value (e.g. event describes laser designated target), the value will represent the one sigma point for a zero mean normal (Guassian) distribution.                                                                                                                                                                                                                           |
| le       | Linear Error in meters associated with the HAE field. Although named le, this field is intended to define a height range about the event point, not necessarily an error. This field, along with the ce field allow for the definition of a cylindrical volume about the point. If it is appropriate for the "le" field to represent an error (e.g. event describes laser designated target), the value will represent the one sigma point for a zero mean normal (Guassian) distribution.A height range about the event point in meters associated with the HAE field. When used to represent error, the value represents the one sigma point for a zero mean normal (Gaussian) distribution. |
| hae      | Height above Ellipsoid based on WGS-84 ellipsoid (measured in meters)HAE acronym for Height above Ellipsoid based on WGS-84 ellipsoid (measured in meters).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

53. ## ** polyline**

The poly line provides a mechanism to express arbitrarily complex two-dimenstional shapes. This is used for representing oddly shaped objects such as exclusion zones, etc. Though generally closed, it is not necessarily a closed line, thus allowing polyline to represent objects such as phasing lines, etc.

1. ### ** polyline attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| vertex   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| level    | "level" is used to indicate the preferred ordering of multiple shape sub-schemas. For instance, if a polyline and ellipse are both present on the shape attribute, the one with the higher level value will be the "more desirable" representation of the object. This allows producers to provide alternative representation of an objects shape while ensuring that consumers will know which of the available representation is the best. (Note that not all consumers will implement all shape variations, hence the need for the allowing multiple shape objects.)See the documentation for shape/ellipse/@level for remarks on determining the precedence order when level values are equal or are missing. |
| closed   | True if the list of verticies should be considered a closed polygon (an implicit line will be added from vertex N to vertex 0).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

54. ## ** Precisionlocation**

some type of location?

1. ### ** Precisionlocation attributes**

| **Name**             | **Documentation**       |
| -------------------- | ----------------------- |
| altsrc               | TDB can be DTED0 or ??? |
| geopointsrc          |                         |
| PRECISE_IMAGE_FILE   |                         |
| PRECISE_IMAGE_FILE_X |                         |
| PRECISE_IMAGE_FILE_Y |                         |

55. ## ** remarks**

This is a Cursor On TargetClass for a generic remarks (aka "FreeText").

Provides a place to annotate CoT with free text information. e.g. comments from other users about the current CoT.
Used also for the geoChat.

**the xml body of this class is used to transport the chat message**

While the use of free text is strongly discouraged (it hampers machine-to-machine communication) it is a pragmatic necessity. This entity attempts to encapsulate freetext in a way that simplifies subsequent machine processing. The content of this entity is presumed to be a human-readable chunk of textual data. The attributes merely aid in the machine handling of the data.

1. ### ** remarks attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| time     | the time of the remark was added to the CoT object                                                                                                                                                                                                                                                                                                                                    |
| to       | Intended recipeint(s) of this remark information. Tentative field coding as follows: The to attribute may contain the UID of the entity to whom the message is addressed. (Implementors should expect that future versions of this sub schema will allow a comma separated list of UIDs.) Absense of an explict addressee means the message is broadcast.e.g. ANDROID-359975090666199 |
| source   | Source specifies the sender’s UID – this is what is parsed by recipients to determine the sender, with the UID format being the fallback.                                                                                                                                                                                                                                             |
| version  | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions.                                                                                                                                                                                                                                                                                     |
| keywords | Used to track a conversation thread. The format is a comma-separated list of freetext keywords.ex. keywords="debriefing" - Describes a conversation about debriefingex. keywords="mission-A" - Describes a conversation about mission-Aex. keywords="tasking_B, subject_C" - Describes a conversation about tasking_B and subject_C                                                   |
| sourceID |                                                                                                                                                                                                                                                                                                                                                                                       |

56. ## ** request**

This is a Cursor On Target sub-schema for a generic request. This schema contains information common to all requests, specifically where responses should be sent, the overall priority of the request, if immediate willco/cantco acknowledgement is needed, etc. Detail information for specific request types are carried in sub-schemas nested within this one.

Notice that this is not the same as in**TAKRequest**

1. ### ** request attributes**

| **Name**  | **Documentation**                                                                                                                                                                                                                                                                                                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| notify    | Network endpoint to which status notifications should be delivered. (A network endpoint is represented as an URL, e.g., tcp://hostname:port, udp://hostname:port. The previous format, host:port, e.g., 192.168.0.1:71556, is deprecated, but implementers should be aware that this format may be in use.                                               |
| wilcoby   | An optional field that requests the receiving system to provide a positive or negative akcnowledgement (WILCO/CANTCO) by a specific time. This is used to ensure that deadline driven requests are made known to the operator.                                                                                                                           |
| priority  | This optional field indicates this request's relative priority with respect to other requests. (At present, no specific coding scheme is in mandated, but a floating point value between 0.0(low) and 1.0(high) is in current (limited) use.)                                                                                                            |
| version   | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions.                                                                                                                                                                                                                                                        |
| to        | When present, this field contains the CoT UID of the specific entity who is being addressed. It is assumed that all CoT entities that can provide a service are reported as friendly atoms.                                                                                                                                                              |
| authority | This is a 'signature block' which holds the CoT uid of the entity which has uathorized the request. The authorizing entity is not necessarily the originator of the request and might not be associated with the 'notify' field. Authority is intended to provide services (such as a striker) a mechanism to verify that the request has been approved. |
| streamto  |                                                                                                                                                                                                                                                                                                                                                          |

57. ## ** route**

  


1. ### ** route attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| sender   |                   |

58. ## ** routeinfo**

  


1. ### ** routeinfo attributes**

| **Name**    | **Documentation** |
| ----------- | ----------------- |
| \_\_navcues |                   |

59. ## ** sensor**

This is (the root class of) a Cursor On Target sub-schema for a steerable, staring sensor such as EO, IR, or Radar sensor. The root class is intended to capture only information on the sensor's orientation and field of view is. Details about it's spectrum, sensitivity, resolution, modality, performance, etc., should be captured in a "derived" subschema for that particular type of sensor. All orientation attributes associated with sensor are normalized to an geodedic frame of reference, removing platform factors such as roll, pitch, yaw, etc. Therefore an "azimuth" of 0 means the sensor is pointed north regardless of its platform heading or attitude.

1. ### ** sensor attributes**

| **Name**                 | **Documentation**                                                                                                                                                        |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| elevation                |                                                                                                                                                                          |
| version                  | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions.                                                                        |
| type                     | The sensor type. This is a type hierarchy much like the CoT type tree. E.g., r - raster, r-e - raster EO, r-e-z-c - raster EO zoom continuous. See types.txt for details |
| vfov                     |                                                                                                                                                                          |
| model                    | This is the sensor model. E.g., LANTRIN, TARPS, etc.                                                                                                                     |
| fov                      | field of view                                                                                                                                                            |
| roll                     |                                                                                                                                                                          |
| fovBlue                  |                                                                                                                                                                          |
| displayMagneticReference |                                                                                                                                                                          |
| range                    |                                                                                                                                                                          |
| fovGreen                 |                                                                                                                                                                          |
| fovAlpha                 |                                                                                                                                                                          |
| hideFov                  |                                                                                                                                                                          |
| fovRed                   |                                                                                                                                                                          |
| azimuth                  |                                                                                                                                                                          |

60. ## ** shape**

This is a Cursor On Target sub-schema for a generic shape description. Many objects are not adequately represented by the simple "point" object in the CoT base schema. However, it is counterproductive to burden all CoT applications to understand arbitrary shapes, so "shape" is an optional attribute that can be used to communicate between shape-aware apprications. The "point" object in the base schema must still be populated and the CE and LE fields in the point entity must be set such that the point completely encloses the area described in any shape entity in the detail section. (This is needed so that CoT applications can quickly filter out objects that are clearly outside an area of interest.

1. ### ** shape attributes**

| **Name** | **Documentation**                                                                                                                                                                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ellipse  | The "ellipse" is a common shape abstraction used by many geomanipulation applications; it is supported natively.                                                                                                                                                                                                  |
| link     |                                                                                                                                                                                                                                                                                                                   |
| polyline | The poly line provides a mechanism to express arbitrarily complex two-dimenstional shapes. This is used for representing oddly shaped objects such as exclusion zones, etc. Though generally closed, it is not necessarily a closed line, thus allowing polyline to represent objects such as phasing lines, etc. |
| dxf      | This is a hook for an arbitrary 3D DXF description of a volume of space.                                                                                                                                                                                                                                          |
| version  | Version tag for this sub schema. Can be used to ensure upward compatibility with future revisions.                                                                                                                                                                                                                |

61. ## ** size**

  


1. ### ** size attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

62. ## ** spatial**

This is a Cursor On TargetClass for spatial information of physical entity. It is intended to appear in the detail section of the Cursor On Target schema. It has elements to represent attitude and associated first derivatives (spin). The intention behind the spatial element is to convey the attitude of a body moving through space with respect to its "nominal" flight attitude.

1. ### ** spatial attributes**

| **Name** | **Documentation**                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------- |
| attitude | Attitude represents the attitude of the entity described by the Cursor On Target base schema.     |
| spin     | Spin represents the first derivative of attributes found in attitude.                             |
| version  | Version tag for this sub schema. Neccessary to ensure upward compatibility with future revisions. |

63. ## ** spin**

  


1. ### ** spin attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| roll     |                   |
| pitch    |                   |
| yaw      |                   |

64. ## ** status**

The status element provides a container for elements reporting different kinds of

status. e.g. a fuel subschema is used to report the amount of burnable fuel

remaining in liters and the current burn rate (in liters per second).

1. ### ** status attributes**

| **Name**  | **Documentation**                             |
| --------- | --------------------------------------------- |
| battery   | % of the battery on the phone                 |
| readiness | probably boolean to determine if ready or not |

65. ## ** strokeColor**

  


1. ### ** strokeColor attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| value    |                   |

66. ## ** strokeWeight**

  


1. ### ** strokeWeight attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| value    |                   |

67. ## ** submissionTime**

  


1. ### ** submissionTime attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

68. ## ** submitter**

  


1. ### ** submitter attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

69. ## ** TakControl**

A server which supports the TAK Protocol**MAY**send the following CoT XML message to indicate this support (whitespace added, xml header omitted):

_&lt;event version='2.0' uid='protouid' type='t-x-takp-v' time='TIME' start='TIME' stale='TIME' how='m-g'>_

_&lt;point lat='0.0' lon='0.0' hae='0.0' ce='999999' le='999999'/>_

_&lt;detail>_

_&lt;TakControl>_

_&lt;TakProtocolSupport version="1"/>_

_&lt;/TakControl>_

_&lt;/detail>_

_&lt;/event>_

This message may contain one or more TakProtocolSupport elements inside the single &lt;TakControl> detail, each specifying a supported version.

The TAK server MUST send this message no more than once per connection.

To allow for ancillary information in the negotiation, the TakProtocolSupport element_MAY_contain additional attributes compliant

with the Protocol version indicated.

1. ### ** TakControl attributes**


70. ## ** TAKControlSupport**

set from

1. ### ** TAKControlSupport attributes**

| **Name** | **Documentation**                                                                                    |
| -------- | ---------------------------------------------------------------------------------------------------- |
| version  | version attribute is an integer number specifying a version of the TAK Protocol the server supports. |

71. ## ** TakRequest**

  


1. ### ** TakRequest attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| version  |                   |

72. ## ** TakResponse**

is sent in the procedure of negotiating protolcs to indicates if the server is accepting the client request to switch to an higher level of the protocol

1. ### ** TakResponse attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| status   |                   |

73. ## ** takv**

Provides the type and version of the TAK client

1. ### ** takv attributes**

| **Name** | **Documentation**                        |
| -------- | ---------------------------------------- |
| platform | the variant of TAK                       |
| device   | type of physical device                  |
| os       | the operating system running TAK         |
| version  | the version of TAK running on the device |

74. ## ** templates**

a class for checklist templates

1. ### ** templates attributes**


75. ## ** timestamp**

  


1. ### ** timestamp attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

76. ## ** tog**

  


1. ### ** tog attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| enabled  |                   |

77. ## ** tool**

  


1. ### ** tool attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

78. ## ** track**

The track element specifies**direction** and **speed**of travel. It has two required attributes: course and speed. It also has optional attributes for specifying the vertical component of the motion vector (slope) and errors associated with course, speed, and slope.

**Course**denotes the direction of motion and is specified as the number of degrees measured clockwise from true North.

**Speed**is specified in meters per second as speed over ground.

There is no constraint on the precision used for these values.

1. ### ** track attributes**

| **Name** | **Documentation**                                                             |
| -------- | ----------------------------------------------------------------------------- |
| speed    |                                                                               |
| eCourse  | 1-sigma error on a Gaussian distribution associated with the course attribute |
| course   |                                                                               |
| eSpeed   | 1-sigma error on a Gaussian distribution associated with the speed attribute  |
| eSlope   | 1-sigma error on a Gaussian distribution associated with the slope attribute  |
| version  |                                                                               |

79. ## ** type**

  


1. ### ** type attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

80. ## ** uastool**

  


1. ### ** uastool attributes**

| **Name**    | **Documentation** |
| ----------- | ----------------- |
| extendedCot |                   |
| activeRoute |                   |

81. ## ** uid**

This is a Cursor On Target detail Class that holds the unique ID assigned by each system that processed this event.

Most systems (including CoT) have their own method for assigning system-wide unique identifiers for a particular object. In general, it is not possible for a single UID to be used for all systems. This 'uid' entity provides a common place where each systems can record its particular UID for each CoT event. Like the \_flow-tags\_ element, each system is responsible for adding its own attribute to this entity. The name of the attribute should represent the system, and the value of the attribute should be the id that system assigned to this CoT object.

1. ### ** uid attributes**

| **Name** | **Documentation**        |
| -------- | ------------------------ |
| version  |                          |
| Droid    | TBD, maybe from Android? |

82. ## ** uid**

special class used in mission only for ID

1. ### ** uid attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| INTAG    |                   |

83. ## ** usericon**

the image used to display the COt

1. ### ** usericon attributes**

| **Name**    | **Documentation**                                                                                                                                                                                                                                                |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| iconsetpath | the path of the icon image usedMIL 2525 STD- COT_MAPPING_2525B/a-u/a-u-GICON- 34ae1613-9645-4222-a9d2-e5f243dea2865/Military/EA-6B.png - 'f7f71666-8b28-4b57-9fbb-e38e61d33b79/Google/hiker.png'/in alternative for a spot- COT_MAPPING_SPOTMAP/b-m-p-s-m/-65536 |

84. ## ** vehicle**

  


1. ### ** vehicle attributes**

| **Name**                 | **Documentation** |
| ------------------------ | ----------------- |
| goHomeBatteryPercent     |                   |
| hal                      |                   |
| flightTimeRemaining      |                   |
| typeTag                  |                   |
| batteryRemainingCapacity |                   |
| isFlying                 |                   |
| flightTime               |                   |
| type                     |                   |
| batteryMaxCapacity       |                   |
| voltage                  |                   |

85. ## ** vertex**

  


1. ### ** vertex attributes**

| **Name** | **Documentation**                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| hae      | Height Above Ellipsoid (HAE) in Meters. If absent, the value of the point/@hae in the CoT event base schema is used.                   |
| lat      | Latitude based on WGS-84 ellipsoid in signed degree-decimal format (e.g. -33.350000). Range -90 -> +90. Positive values denote north.  |
| lon      | Longitude based on WGS-84 ellipsoid in signed degree-decimal format (e.g. 44.383333). Range -180 -> +180. Positive values denote east. |

86. ## ** video**

  


1. ### ** video attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| sensor   |                   |
| spi      |                   |
| url      |                   |

87. ## ** Text**

  


1. ### ** Text attributes**


88. ## ** bullseye_bearingRef**

  


1. ### ** bullseye_bearingRef attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| T        |                   |
| M        |                   |
| G        |                   |

89. ## ** checklistColumnType**

  


1. ### ** checklistColumnType attributes**

| **Name**     | **Documentation** |
| ------------ | ----------------- |
| ShortString  |                   |
| LongString   |                   |
| Integer      |                   |
| ActualTime   |                   |
| RelativeTime |                   |

90. ## ** checklistStatus**

  


1. ### ** checklistStatus attributes**

| **Name**        | **Documentation** |
| --------------- | ----------------- |
| Pending         |                   |
| Complete        |                   |
| Complete (late) |                   |
| Late            |                   |

91. ## ** checklistTaskStatus**

  


1. ### ** checklistTaskStatus attributes**

| **Name**        | **Documentation** |
| --------------- | ----------------- |
| Pending         |                   |
| Complete        |                   |
| Complete (late) |                   |
| Late            |                   |

92. ## ** MissionType**

  


1. ### ** MissionType attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| CREATE   |                   |
| CHANGE   |                   |

93. ## ** route_fil**

  


1. ### ** route_fil attributes**

| **Name** | **Documentation** |
| -------- | ----------------- |
| Infil    |                   |
| Exfil    |                   |

94. ## ** route_method**

  


1. ### ** route_method attributes**

| **Name**   | **Documentation** |
| ---------- | ----------------- |
| Driving    |                   |
| Walking    |                   |
| Flying     |                   |
| Swimming   |                   |
| Watercraft |                   |

95. ## ** route_order**

  


1. ### ** route_order attributes**

| **Name**                | **Documentation** |
| ----------------------- | ----------------- |
| Ascending Check Points  |                   |
| Descending Check Points |                   |

96. ## ** route_routetype**

  


1. ### ** route_routetype attributes**

| **Name**  | **Documentation** |
| --------- | ----------------- |
| Primary   |                   |
| Secondary |                   |

97. ## ** TeamColor**

  


1. ### ** TeamColor attributes**

| **Name**   | **Documentation** |
| ---------- | ----------------- |
| Yellow     |                   |
| Red        |                   |
| Blue       |                   |
| Orange     |                   |
| Magenta    |                   |
| Maroon     |                   |
| Purple     |                   |
| Dark Blue  |                   |
| Cyan       |                   |
| Teal       |                   |
| Green      |                   |
| Dark Green |                   |
| Brown      |                   |

98. ## ** TeamRole**

  


1. ### ** TeamRole attributes**

| **Name**         | **Documentation** |
| ---------------- | ----------------- |
| Team Member      |                   |
| Team Lead        |                   |
| HQ               |                   |
| Sniper           |                   |
| Medic            |                   |
| Forward Observer |                   |
| RTO              |                   |
| K9               |                   |

  
  
