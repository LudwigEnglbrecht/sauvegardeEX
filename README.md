# sauvegardeEX

The sauvegardeEX system combines various extensions of the software sauvegard to enable an improved usability as well as a broader application. 

## Architecture

To make the core functionality of the software [sauvegarde](https://github.com/dupgit/sauvegarde) continious data protection usable for further applications, the existing client/server architectur was extended by a web server for an intuitive usage. In addition, in the web server area, a modular expandable area was created.

The architecture consists of all the clients, from which you want to obtain data, the cdp-forensic-webserver and the [cdp-forensic-frontend](https://github.com/danieltrtwn/cdp-forensic-frontend), which provides the GUI. Every linux client is running a cdpfgl client which sends the data, whenever a file changes, to the cdpfgl server, which is running on the same linux machine as the cdp-forensic-webserver.

![](https://github.com/meinlschmidt/cdp-forensic-webserver/raw/dabb7ede899235f7db47df657aa3562ccae37f72/architecture.png)

# Installation 1/3 - The modified version of cdpfgl Server

Install the [forked version of cdpfgl](https://github.com/meinlschmidt/sauvegarde) by following the readme on every client and the server machine, which will be the cdp-forensic-webserver.
Gnu/linux operating systems that can run cdpfgl can be found in the readme, we used Ubuntu 18.04 LTS for clients and server.

Start the cdp server on the server machine using the default config with
```
sudo cdpfglserver
```

or create a config file for the cdp server or modify the existing one to your needs as described in the readme and run it on the server machine with
```
sudo cdpfglserver -c /path/to/config/file
```

Create a config file for every cdp client or modify the existing one to your needs as described in their readme.
The cdp client config file contains all monitored directories and the ip address of your server machine.
Run the cdp client on every client machine with
```
sudo cdpfglclient -c /path/to/config/file
```

# Installation 2/3 - cdp-forensic-webserver (on cdpfgl Server)

The Webserver for using special functionalities needs to be installed at the same machine running the cdpfgl Server.

Check out this repository on the server machine e.g. with IntelliJ and run the cdp-forensic-webserver.
If you did not use the default cdp server config, ensure that the value of cdpServerMetaDirectory in class WebserverApplication extends the file-directory path from your cdp server config by /meta.

Use the [cdp-forensic-frontend](https://github.com/danieltrtwn/cdp-forensic-frontend) as GUI to use the cdp-forensic-webserver services.

# Installation 3/3 - cdp-forensic-frontend (any machine)

To install the easy to use Web Interface (cdp-forensic-frontend) follow the following steps:

Install node.js.

Download the repository files manually or check them out with IntelliJ.

Install the dependencies in the project directory with
```
npm install
```

### Configuration

Set the ip address of your [cdp-forensic-webserver](https://github.com/meinlschmidt/cdp-forensic-webserver) in the file Config.js

### Run

Start the frontend with the local server of IntelliJ by clicking on the browser icon in top right corner when index.html is open or with the [npx http-server](https://www.npmjs.com/package/http-server):
```
npx http-server --cors -c-1
```

### Usage

Select the host for which you want to inspect files, optional you can add a filter, a start date and an end date to specify the query to the webserver.
As a result you can see all files which have been created and modified on the monitored directories of the host.
With the time slider you can retrace the creation and modification of the files.

If you click on a file you can see all the occurred versions of a file with a time stamp and you are able to download any version you want.
By clicking the restore icon, you can restore all file occurrences in a directory within the time range, which is at the moment selected by the time slider.
By clicking the entropy icon, you can calculate an entropy of all files from a directory.
 
![](https://github.com/danieltrtwn/cdp-forensic-frontend/raw/master/images/screenshot.png)


# Use cases of sauvegardeEx

- Digital Forensics Fingerprinting
- Digital Twin Mirroring

# Authors

- Philipp Meinlschmidt
- Daniel Trautwein

Feel free to contact us or [Mr. Ludwig Englbrecht](https://www.researchgate.net/profile/Ludwig_Englbrecht) for improvements or questions.

# About the project

This project deals with the purpose-specific extension of the software [sauvegarde](https://github.com/dupgit/sauvegarde) and was developed as part of a master student seminar at the University of Regensburg, Chair of Information Systems (Prof. Dr. Günther Pernul) under the supervision of [Mr. Ludwig Englbrecht](https://www.researchgate.net/profile/Ludwig_Englbrecht) for educational and academic use. 
