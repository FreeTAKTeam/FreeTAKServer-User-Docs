---
status: todo
---

# About [MIL-STD-2525](https://en.wikipedia.org/wiki/NATO_Joint_Military_Symbology) and CoT
The Center on Target (CoT) is a data exchange format primarily used in military and emergency response applications such as the TAK ecosystem.
It is designed to facilitate real-time sharing of geospatial information among various systems and users. 
The CoT protocol enables efficient communication of location, status, and other relevant situational data,
enhancing operational awareness and coordination.
MIL-STD-2525 is a military standard that specifies symbols for use on maps, charts, and other graphical displays
in military command, control, communications, computers, and intelligence (C4I) system.
The original 'NATO symbol' are expressed as a set of Military Symbols for Land Based Systems (MIL-STD-2525).
The CoT system is only partially overlapping with 2525.
On a list of 3000+ CoT's , 1000 are directly traceable to MIL-STD-2525.

The MIL_STD-2525 has had several versions:
* [MIL-STD-2525D](https://www.jcs.mil/Portals/36/Documents/Doctrine/Other_Pubs/ms_2525d.pdf) 2014
* [MIL-STD-2525C](https://www.jcs.mil/Portals/36/Documents/Doctrine/Other_Pubs/ms_2525c.pdf) 2008
* [MIL-STD-2525B](http://www.mapsymbs.com/ms2525b_ch1_full.pdf) 2005

The standard make use of 'Symbol Identification Code' (SIDC).

In MIL-STD-2525C/B,
"An alphanumeric code based on a database structure that
provides the minimum elements required to construct
the basic icon and/or a complete symbol."

MIL-STD-2525C further specifies that
A SIDC is a 15-character alphanumeric
identifier that provides the information necessary to display or transmit
a tactical symbol between MIL-STD-2525 compliant systems."

In MIL-STD-2525D this changed substantially,
"A.5.2 Elements of the symbol identification codes.
The symbol identification code is composed of eleven elements of information
which are presented in two sets of ten digits.
An additional set of ten digits composed of three elements must be used
when a symbology originator version extension flag is used."

As the SIDC does not require that all positions be used
the vacant positions are conventionally occupied by a '-'.
When used with CoT this introduces an ambiguity which is addressed below.


## Event.type

Defines what the event is about.
An event may describe a physical object, a set of raw, unprocessed bits, or a tasking. 

See the [Cursor on Target Message Router User's Guide](https://www.mitre.org/sites/default/files/pdf/09_4937.pdf) for details.

### section 2.3 'CoT Type Field Details'
Duplicated (with edits) herein:

The Cursor-on-Target Message Router often uses the CoT type string as a test for publication.
For this reason, the type field is briefly explained here.

The set of possible CoT types is defined by a tree structure.
The type attribute, as defined in Event.xsd, identifies a specific node in the type tree.
It is a hyphen delimited set of alphanumeric characters.
For example, a-f-G represents a type tree of "atoms-friendly-ground".
The root element (first character in the type field) of the tree
has several values to include atoms, bits, reservations, capability descriptions, etc.

The atoms branch of the tree leverages the MIL-STD-2525B specification for defining the detailed type.
The string is broken out as `atoms-affiliation-battle dimension-from 2525 function code`.
For example, the type string `a-h-A-MFA` represents "atoms-hostile-Airborne-Military-Attack/Strike".
The lower case `a-h` prefix is defined in `Event.xsd`.

In the discussion found below, the "atoms" branch of the type
string will be described by the term's affiliation, battle dimension, and 2525 function code
per the description in this paragraph.

The following tree diagrams the valid atomic event combinations.

#### Level 1 : atoms
* a (atom)

#### Level 2 : affiliation
* p (pending)
* u (unknown)
* a (assumed friend)
* f (friend)
* n (neutral)
* s (suspect)
* h (hostile)
* j (joker)
* k (faker)
* o (none specified)
* x (other)
  
#### Level 3 : battle dimension

* P (space)
* A (air)
* G (ground)
* S (sea surface)
* U (sea subsurface)
* X (other)

The first `-A-` is the MIL-STD-2525 battle dimension (air, ground, surface, etc).
It is derived from the battle-dimension portion of the SIDC (position 3).

#### Level 4 : function code

The remaining characters are the MIL-STD-2525B function code.
In this example, `MFA` represents "Military-Attack/Strike" which
corresponds with the SIDC / function-code (positions 5-10) `MFA---`.


### Hierarchically organized hint about event type 
The "type" attribute is a composite of components delimited by the semicolon character
(e.g. `a-f-G-I` for "Friendly Ground infrastructure").
The first component of this composite attribute is defined below.

Future versions of this schema will define other components which we expect will aid in machine filtering.
Despite the exclusion of definitions for additional components in this version of the schema,
users of this schema should expect and design an optional trailing field
delimited by the semicolon character.

This field can be ignored.
```text
component1;optional field
```

The first component (component1) is a hierarchically organized hint about type.
The intention is that this hierarchy be flexible and extensible and
facilitate simple filtering, translation and display. 

To facilitate filtering, the hierarchy needs to present key fields in an easily parsed and logical order.
To facilitate this, this component is a composite of fields separated by the "-" punctuation character,
so a valid type would be: 

```
x-x-X-X-x. 
```

Using a punctuation for field separation allows arbitrary expansion of the type space. 
```
e.g., a-fzp-mlk-gm-...
```

Field meanings are type specific.
That is, the third field of an "atom" type may represent air vs. ground
while the same field for a "reservation" type may represent purpose.

### MEANING of 'a' in the first position 
The "Atoms" portion of the type tree requires some additional explanation past the taxonomy defined below.
The "Atoms" portion of the type tree contains CoT defined fields
and part of the MIL-STD-2525 type definition.
To distinguish MIL-STD-2525 type strings from CoT defined fields,
the MIL-STD-2525 types must be represented in all upper case.
Differentiation of type namespace with upper/lower case
facilitates extension of CoT types and MIL-STD-2525 types without name space conflict.
An example:
```
 a-f-A-B-C-x
```

 * a = Atom
 * f = attitude or disposition (friendly in this case)
 * A-B-C = the symbol identification coding (SIDC) scheme for 2525 – a strings of 15 characters used to transmit symbols.
 * x = non capital CoT specific extension
 
 The organization of CoT and MIL-STD-2525 types can be determined from the taxonomy,
 but additional details are provided here.
 The "Atoms" portion of the "type" tree contains
 the "Battle Dimension" and "Function ID" fields taken from MIL-STD-2525 (see below).
 "Battle Dimension" is a single character taken from MIL-STD-2525 and is located in the position 5. 
```
a-.- **G** -I-M-N-B
```

The typical 2525 representation for "Function ID" is three groups of two characters separated by a space (e.g. "12 34 56").
The CoT schema maps this to a "-" delimited list of characters. (e.g. "1-2-3-4-5-6").
 The concatenation of the "Battle Dimension" and "Function ID" fields
 from the MIL-STD-2525 specification represented in the CoT schema will be as follows:
 
 ```
 battle dimension-func id char1-func id char2- ... -func id char6
 ```
 When an appropriate MIL-STD-2525 type exists, it should be used.
 If there is a MIL-STD-2525 representation which is close, but may be refined,
 a CoT extension to the 2525 type can be appended.
 
For example: 
`a-h-X-X-X-X-X-i` might represent hostile MIL-STD-2525 type `X-X-X-X-X` of Israeli (the 'i') manufacture.
Again, the CoT extension uses lower case. 
Conceptually, this extension defines further branching from the nearest MIL-STD-2525 tree point.
If no appropriate 2525 representation exists,
a type definition can be added to the CoT tree defined here.
The resulting definition would be represented in all lower case.
For example, `a-h-G-p-i`
might define atoms-hostile-Ground-photon cannon-infrared.
The taxonomy currently looks like this:
(Note that the coding of the sub-fields are determined entirely by the preceding fields!)
The current type tree is defined here. 

#### First position, this event describes a - Atoms

* a - Atoms - this event describes an actual "thing"

##### 2nd CoT affiliation of these atoms
 
 * p - Pending
 * u - Unknown
 * a - Assumed friend
 * f - Friend
 * n - Neutral
 * s - Suspect
 * h - Hostile
 * j - Joker
 * k - Faker
 * o - None specified
 * x - Other
 
##### Battle dimension
 Taken from MIL-STD-2525 "Battle Dimension" (upper case)
 * P - Space
 * A - Air
 * G - Ground
 * S - Sea Surface
 * U - Sea Subsurface
 * SF - Special Operations Forces

##### Function (dimension specific!)
See MIL-STD-2525B specification for function fields (must be upper case).
Any number of characters before the first "dash",
it also expresses a hierarchy (Hundreds of options).

###  The event describes: `b` - Bits ...
the first position can also contain a `b`.

**b - Bits** - Events in the "Bit" group (pos 1163++ ) carry meta information about raw data sources. For example, range-doppler radar returns or SAR imagery represent classes of information that are "bits". However, tracks derived from such sources represent objects on the battlespace and this have event type "A-..."
The intention with the "Bit" type is to facilitate the identification of germane information products.
This hierarchy is not intended to replace more detailed domain-specific meta information (such as that contained in NITF image headers or the GMTI data formats), rather it is intended to provide a domain-neutral mechanism for rapid filtering of information products.

#### Dimension
second position, like battle dimension but for 'b' types

##### i - Imagery
 * e - Electro-optical
 * i - Infra red
 * s - SAR
 * v - video
 * ...
##### r - Radar
 * m - MTI data
 * ...
##### d - Sensor detection events
 * s - Seismic
 * d - Doppler
 * a - Acoustic
 * m - Motion (e.g., IR)
 * ...
##### m - Mapping
 * p - Designated point (rally point, etc.)
 * i - initial points
 * r - rally points
 * ...

### The event describes: `r` - Reservation/Restriction/References 
 Events in this category are generally "notices" about specific areas.
 These events are used for deconfliction and conveyance of significant "area" conditions.
 Generally, the "point" entity will describe a conical region that completely encloses the affected area.
 The details entity will provide more specific bounds on precisely the region affected.
 
 * u - Unsafe (hostile capability)
 * o - Occupied (e.g., SOF forces on ground)
 * c - Contaminated (NBC event)
 * c - chemical
 * x - agents, direction,
 * y
 * z
 * f - Flight restrictions

### The event describes: `t` - Tasking (requests/orders)
Events in this category are generalized requests for service.
These may be used to request for data collection, request mensuration of a specific object, order an asset to take action against a specific point.
Generally, the "details" entity will identify the general or specific entity being tasked.
 * s - Surveillance
 * r - Relocate
 * e - Engage
 * m - Mensurate
 * x - experimental, new tasking
 ###  The event describes: `u` - drawing (applied to an area)
 * d - drawing
 * r - range
 * ...
 ###  The event describes: `c` - Capability (applied to an area)
 * s - Surveillance
 * r - Rescue
 * f - Fires
 * d - Direct fires
 * i - Indirect fires
 * l - Logistics (supply)
 * f - Fuel
       ...
### c - Communications
 * TBD

###  The event describes: `y` - reply to a task
 * c - task completed
 * s - task status
 * a - acknowledge 

## mil2525 structure

| **Pos** | **Type**              | **Value**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|:--------|:----------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1       | en: Coding scheme     | <p>S - Warfighting<br>I - Intelligence<br>O - Stability Operations<br>E – Emergency Management<br>WO – Weather</p><p>G – Tactical Group</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 2       | en: Affiliation       | P - Pending<br>U - Unknown<br>A - Assumed Friend<br>F - Friend<br>N - Neutral<br>S - Suspect<br>H - Hostile<br>G - Exercise Pending<br>W - Exercise Unknown<br>D - Exercise Friend<br>L - Exercise Neutral<br>M - Exercise Assumed Friend<br>J - Joker<br>K - Faker<br>O - None Specified                                                                                                                                                                                                                                                                                                                           |
| 3       | en: Battle Dimension  | **If** ***Coding scheme*** **is S or I:**<br>P - Space<br>A - Air<br>G - Ground<br>S - Sea Surface<br>U - Sea Subsurface<br>SF - Special Operations Forces<br><br>**If** ***Coding scheme*** **is O:**<br>V - Violent Activities<br>L - Locations<br>O – Operations<br>I - Items<br>P - Individual<br>G - Nonmilitary Group or Organization<br>R – Rape<br><br>**If** ***Coding scheme*** **is E:**<br>I - Incident<br>N - Natural Events<br>O - Operations<br>F - Infrastructure                                                                                                                                   |
| 4       | en: Status            | A - Anticipated/Planned<br>P - Present<br>C - Present/Fully Capable<br>D - Present/Damaged<br>X - Present/Destroyed<br>F - Present/Full to Capacity                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 5-10    | en: Function ID       | <p>Any number of char before the first "dash", it express also the hierarchy</p><p>(Hundreds of options)</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 11      | en: Symbol Modifier 1 | <p>A - Headquarters<br>B - Task Force HQ<br>C - Feint Dummy HQ<br>D - Feint Dummy/Task Force HQ<br>E - Task Force<br>F - Feint Dummy<br>G - Feint Dummy/Task Force<br>H – Installation</p><p>M - Mobility<br>N - Towed Array</p>                                                                                                                                                                                                                                                                                                                                                                                    |
| 12      | en: Symbol Modifier 2 | A - Team/Crew<br>B - Squad<br>C - Section<br>D - Platoon/Detachment<br>E - Company/Battery/Troop<br>F - Battalion/Squadron<br>G - Regiment/Group<br>H - Brigade<br>I - Division<br>J - Corps/Mef<br>K - Army<br>L - Army Group/Front<br>M - Region<br>N – Command<br><br>**If** ***Symbol Modifier 1*** **is M:**<br>O - Wheeled/Limited<br>P - Wheeled<br>Q - Tracked<br>R - Wheeled and Tracked<br>S - Towed<br>T - Rail<br>U - Over the Snow<br>V - Sled<br>W - Pack Animals<br>Y - Barge<br>Z – Amphibious<br><br>**If** ***Symbol Modifier 1*** **is N:**<br>S - Towed Array (Short)<br>L - Towed Array (Long) |

## Example 2525

Equipment Manufacture is part of ‘WAR.GRDTRK.INS.EQTMNF’ code is

S\*G\*IE----H\*\*\*\*
![image](https://user-images.githubusercontent.com/60719165/193574795-14a3dfce-ff51-457b-a4bc-e6196cdef2fe.png)


| S   | \*          | G      | \*               | IE          | H            |     |     |     |     |     |     |
|:----|:------------|:-------|:-----------------|:------------|:-------------|:----|:----|:----|:----|:----|:----|
| War | Affiliation | Ground | Battle Dimension | Function ID | installation |     |     |     |     |     |     |

Test code [here:](https://www.spatialillusions.com/milsymbol/example.html#angular)

## Example CoT

Equipment manufacture	Building is part of Gnd/Structure/Factory

| **Atom** | ** ** | **Affiliation** | ** ** | ** Ground ** | ** ** | ** Infrastructure ** | ** **  | ** Equipment **  |	
|:---------|:------|:----------------|:------|:-------------|:------|:---------------------|:-------|:-----------------|
| a        | -     | .               | -     | G            | -     | I                    | -      | E                |	

