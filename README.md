# gdbghidra - a visual bridge between a GDB session and GHIDRA

The purpose of gdbghidra is to provide means during interactive debug sessions in
gdb to quickly follow the flow in GHIDRA; similar to our [gdbida](https://github.com/Comsecuris/gdbida) plugin for IDA Pro. gdbghidra is not meant to be a full debugger. Instead, it merely serves as a small helper tool to assist during interactive debug 
sessions that make use of a mixture of tools. It provides simple means to quickly follow along a gdb debug
session in GHIDRA.

gdbghidra consists of the following two parts:
* dist/ghidra_9.0.1_PUBLIC_20190516_GDBGHIDRA.zip
* data/gdb\_ghidra\_bridge\_client.py : gdb python script

![data/gdbghidra](data/gdbghidra.gif)

Installation
============
Make a change the ~/.gdbinit configuration file to include the plugin:
```
source ~/gdb_ghidra_bridge_client.py
```

To install the plugin in GHIDRA follow these steps:

* Open GHIDRA and select `File/Install Extensions`. 
* Press the green `+` button and select `dist/ghidra_9.0.1_PUBLIC_*_GDBGHIDRA.zip`. 
* Make sure the Plugin has a tick in the box left.
* Start GHIDRA CodeBrowser.
* Open `File/Configure` and press the adapter icon in above left oft 'Ghidra Core'.
* Filter for `gdb` and make sure `GDBGhidraPlugin` is enabled.

Now you should see the `GDBGhidraPlugin` window. You can now configure the listener port using the `configuration` button and start the server using the `refresh` button.

Next, configure the gdb stub to connect to gdbghidras's port (either command line or gdbinit):
```
ghidrabridge 10.0.10.10:2305
```

Development
===========
If you want to build gdbghidra from source using GHIDRA's eclipse environment make sure to add `json-simple-1.1.1.jar` to the classpath as follows:

* Click the `Run` Menu and select `Run Configurations`.
* Navigate to `Ghidra/GDBGhidra` and select `Classpath`.
* Navigate down the list to `User Entries`, select `User Entries` and click on `ADD JARS...`.
* Select `lib/json-simple-1.1.1.jar`

Notes
=====
Please be aware that this is not considered to be finished. Specifically, the following thoughts are on my mind:
* Network listening input masks untested for errors.
* The network connection is not authenticated in any way.
* A lot of potential for additional commands. For now, I kept it super simple.
