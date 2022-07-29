# Install the Spatial Administration Utility

Download and install the Spatial CLI from the **TODO**. This topic also describes how to connect to the Spatial server.

---
**Note:**\
The Administration Utility requires Java 11 or later. Verify that Java 11 is in the system PATH variable before running the Administration Utility.

---


To launch the command line interface, do one of the following:

### Running on Linux

```shell
./spatial-cli.sh
```

### Running on Windows

```shell
spatial-cli.cmd
```

---
**Note:**
If necessary, modify the .sh or .cmd file to use the path to your Java installation.
Connect to the Spectrum Technology Platform server by typing this command:

```shell
connect --h servername:port --u username --p password --s SSLTrueOrFalse
```

---

### Connect to server


| Parameter | Description                                                                                                             |
|-----------|-------------------------------------------------------------------------------------------------------------------------|
| --h       | servername:port                                                                                                         |
| --u       | username that has access to connect to the spatial server                                                               |
| --p       | password for the user                                                                                                   |
| --s       | `true` if want to use secured HTTPS connection. `false` for HTTP see: [Enabling HTTPS for CLI](#Enabling HTTPS for CLI) |

```shell
connect --h myserver:8080 --u admin --p myPassword1 --s false
```

#### Enabling HTTPS for CLI

To connect with remote server over secure connection, we need to add certificate and its path in batch file which starts the application.

For Windows update `spatial-cli.bat` add following in the next line after `DEFAULT_JVM_OPTS=` make sure to define `PATH_TO_CERTIFICATE` and the `password` for the keyStore and trustStore.

```shell
set CLIENT_CERT=PATH_TO_CERTIFICATE
set SPATIAL_CLI_OPTS=-Djavax.net.ssl.keyStore=%CLIENT_CERT% -Djavax.net.ssl.keyStorePassword=password -Djavax.net.ssl.trustStore=%CLIENT_CERT% -Djavax.net.ssl.trustStorePassword=password
```

This will enable HTTPS for cli and allow you to use the `--s true` param for the connect command

```shell
connect --h myserver:8080 --u admin --p myPassword1 --s true
```



Once you are connected you can run commands. Some tips:
- For a list of available commands, type `help` or press the tab key.
- To auto-complete a command, type the first few characters then press the tab key. For example, typing `us` then pressing the tab key automatically completes the command `user`. Pressing the tab key again will display a list of all the `user` commands.
- If you specify an option value that contains a space, enclose the value in double quotes.

When you are done, type exit to exit the Administration Utility.
