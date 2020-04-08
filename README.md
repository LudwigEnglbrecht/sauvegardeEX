# sauvegardeEX

The sauvegardeEX system combines various extensions of the software [sauvegarde](https://github.com/dupgit/sauvegarde)
to enable an improved usability, as well as a broader application in related areas (e.g.: Digital Forensics Analysis and Digital Twin Mirroring). The "EX" in sauvegardeEX refers to "EXtension".


## Architecture

To make the core functionality of the software sauvegarde, continuous data protection, usable for further applications,
the existing client/server architecture was extended by a feature-rich web server and a frontend for an intuitive usage.
In addition, within the web server, a modular expandable area was created.

The architecture consists of a modified version of [sauvegarde](https://github.com/meinlschmidt/sauvegarde), the clients (from which you want to obtain data), the [cdp-forensic-webserver](https://github.com/meinlschmidt/cdp-forensic-webserver)
and the [cdp-forensic-frontend](https://github.com/danieltrtwn/cdp-forensic-frontend).
Every linux client is running the cdpfglclient which sends the data to the cdpfglserver, whenever a file changes. The server component 
cdpfglserver runs next to the cdp-forensic-webserver.

It is important to mention that in this version the focus is not on the recovery of data on the client, but on **the further processing of the file states on a server**. For this purpose, the client component ("CDP Restore-Client") was also installed on the computer where the newly developed web-server is running. The following graphic illustrates the new architecture. 

![](https://github.com/meinlschmidt/cdp-forensic-webserver/raw/dabb7ede899235f7db47df657aa3562ccae37f72/architecture.png)




# Installation 1/3 - The modified version of cdpfglserver

Install the [forked version of sauvegarde](https://github.com/meinlschmidt/sauvegarde) by following the readme on every client and the server machine, which will be the cdp-forensic-webserver.
Gnu/linux operating systems that can run cdpfgl can be found in their readme, we used Ubuntu 18.04 LTS for clients and server.

Start the cdpfglserver on the server machine using the default config with
```
sudo cdpfglserver
```

or create a config file for the cdpfglserver or modify the existing one to your needs as described in the readme and run it on the server machine with
```
sudo cdpfglserver -c /path/to/config/file
```

Create a config file for every cdpfglclient or modify the existing one to your needs as described in the readme.
The cdpfglclient config file contains all monitored directories and the ip address of your server machine.
Run the cdpfglclient on every client machine with
```
sudo cdpfglclient -c /path/to/config/file
```

# Installation 2/3 - cdp-forensic-webserver (on cdpfglserver)

The Webserver for using special functionalities needs to run at the same machine running the cdpfglserver.

Install Java JDK 8 or higher.

Check out the [cdp-forensic-webserver](https://github.com/meinlschmidt/cdp-forensic-webserver) repository files on the server machine,
e.g. with IntelliJ.

Update the variable "commandexternalcall" in /src/main/java/pseminar/cdp/webserver/Entropies.java to the external python script from [https://github.com/LudwigEnglbrecht/entropie](https://github.com/LudwigEnglbrecht/entropie).

After the successful build of the java project you can run the cdp-forensic-webserver.

If you did not use the default cdpfglserver config, ensure that the value of cdpServerMetaDirectory in class WebserverApplication extends the file-directory path from your cdpfglserver config by /meta.

# Installation 3/3 - cdp-forensic-frontend (any machine)
Use the cdp-forensic-frontend as GUI to use the services provided by the cdp-forensic-webserver.
To install the easy to use Web Interface, do the following steps:

Install node.js.

Download the [cdp-forensic-frontend](https://github.com/danieltrtwn/cdp-forensic-frontend) repository files manually or check them out with IntelliJ.

Install the dependencies in the project directory with
```
npm install
```

### Configuration

Set the ip address of your cdp-forensic-webserver in the file Config.js

### Run

Start the cdp-forensic-frontend with the local server of IntelliJ by clicking on the browser icon in top right corner when index.html is open or with the [npx http-server](https://www.npmjs.com/package/http-server):
```
npx http-server --cors -c-1
```

### Usage

Select the host for which you want to inspect files, optional you can add a filter, a start date and an end date to specify the query to the cdp-forensic-webserver.
As a result you can see all files which have been created and modified on the monitored directories of the host.
With the time slider you can retrace the creation and modification of the files.

If you click on a file you can see all the occurred versions of a file with a time stamp and you are able to download any version you want.
By clicking the restore icon, you can restore all file occurrences in a directory within the time range, which is at the moment selected by the time slider.
By clicking the entropy icon, you can calculate an entropy of all files from a directory.
 
![](https://github.com/danieltrtwn/cdp-forensic-frontend/raw/master/images/screenshot.png)


# Use cases of sauvegardeEX

- Digital Forensics Analysis 
- Digital Twin Mirroring
- Teaching in Higher Education

# Roadmap of SauvegardeEX

* (Web-Server and GUI) Implementing a visual file transformation flow
* (Server) Better implementation of the entropy calculation
* Capability to backup entire hard disk images (e.g.: *.vmdk)

# Authors

- Philipp Meinlschmidt
- Daniel Trautwein

Feel free to contact us or Mr. Ludwig Englbrecht via ludwig.englbrecht@wiwi.uni-regensburg.de for improvements or questions.

# About the project

This project deals with purpose-specific extensions of the software [sauvegarde](https://github.com/dupgit/sauvegarde)
and was developed as part of a master student seminar at the University of Regensburg, Chair of Information Systems (Prof. Dr. Günther Pernul), [(https://www.uni-regensburg.de/wirtschaftswissenschaften/wi-pernul/)](https://www.uni-regensburg.de/wirtschaftswissenschaften/wi-pernul/) under the supervision of [Mr. Ludwig Englbrecht](https://www.researchgate.net/profile/Ludwig_Englbrecht) during his Ph.D. Research Project. The software is intended for educational and academic use. 
