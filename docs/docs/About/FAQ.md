# Frequently Asked Questions (FAQ) about FreeTAKServer (FTS)

## What is FTS?
FTS is a TAK server written in Python that connects all your TAK devices.

## Is FTS really 'Free'?
We released our software under the "Eclipse Public License" allowing not only private usage but also commercial products built on top of it.

## TAK clients on the same network can communicate directly! So, why should I use a server?
There are many reasons for using a server, including the availability of a centralized repository of information (data packages), the administration of users and security (SSL), server-side functions (e.g., ExCheck, Data Sync), and integration with other non-TAK systems (e.g., video, audio, Telegram) using the FTS API.

## There are other servers for TAK. Why should I use FTS?
FTS is not only powerful–it's also more user-friendly when [compared](FeaturesCompared.md) to other systems.
Also, FTS is a community-driven Open Source project at its core.
Under the covers, FTS is based on a [domain model](architecture/COTDomain.md),
so it is the only TAK server that can provide analysis and interpretation
of the information it collects–not just receive requests from clients
and provides the requested data or perform the requested actions.
Other TAK servers, on the other hand, act only as information brokers:
they are services that collect, organize, and disseminate information.
The bottom line is that FTS is "smarter" than other TAK servers.

# How can I install FTS?
For information on how to set up FTS,
please see one of the [Installation Guides](../Installation/Tools.md).
