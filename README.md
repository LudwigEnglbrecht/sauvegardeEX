# sauvegardeEX

The sauvegardeEX system combines various extensions of the software sauvegard to enable an improved usability as well as a broader application. 

## Architecture

To make the core functionality of the software [sauvegarde](https://github.com/dupgit/sauvegarde) continious data protection usable for further applications, the existing client/server architectur was extended by a web server for an intuitive usage. In addition, in the web server area, a modular expandable area was created.

The architecture consists of all the clients, from which you want to obtain data, the cdp-forensic-webserver and the [cdp-forensic-frontend](https://github.com/danieltrtwn/cdp-forensic-frontend), which provides the GUI. Every linux client is running a cdpfgl client which sends the data, whenever a file changes, to the cdpfgl server, which is running on the same linux machine as the cdp-forensic-webserver.

![](https://github.com/meinlschmidt/cdp-forensic-webserver/tree/dabb7ede899235f7db47df657aa3562ccae37f72/architecture.png?raw=true)

# Installation

TODO

# Use cases

- Digital Forensics
- Digital Twin Mirroring

# Authors

- Philipp Meinlschmidt
- Daniel Trautwein

# About the project

This project deals with the purpose-specific extension of the software [sauvegarde](https://github.com/dupgit/sauvegarde) and was developed as part of a master student seminar at the University of Regensburg, Chair of Information Systems (Prof. Dr. Günther Pernul) under the supervision of [Mr. Ludwig Englbrecht](https://www.researchgate.net/profile/Ludwig_Englbrecht) for educational and academic use. 
