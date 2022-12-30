# Frequent Asked Question about FreeTAKServer (FTS)

## what is FTS?
FTS is a TAK server written in Python, that connects all yout TAK devices

## Is FTS really 'Free'?
We released our software under the 'Eclipse Public License" allowing not only private usage but also commerical product build on the top of it.

## TAK clients on the same network can communicate directly! so, why should I use a server?
there are many reasons for use a server including a centralized collection of information (data packages), administration of users and security (SSL), 
server side functions (ExCheck, Data Sync), integration with other non-TAK systems (video, Audio, telegram) using the FTS API.

## there are also other servers for TAK, why should I use FTS?
FTS is not only powerfull, it's als  user friendlier  [Compared](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/About/FeaturesCompared.md) to other systems.
Also FTS is a community driven Open Source project at his core. Under the cover, FTS is based on a [domain model](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/About/architecture/COTDomain.md)
so it's the only TAKL server that can provide analysis and interpretation of the information they collect. It for requests from clients and provides the requested data or performs the requested actions.
All other TAK servers , on the other hand, act as information brokers: a service that collects, organizes, and disseminates information.
the bottom line is that FTs is 'Smarter' that other TAK servers.

# How can I install FTS?
please see follow out [Installation guides](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/Tools/) to setup FTS
