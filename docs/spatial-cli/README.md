# Install the Spatial CLI Utility

Download and install the Spatial CLI from the **TODO::ONE_DRIVE_LINK**. This topic also describes how to connect to the Spatial Server cloud.

---
**Note:**\
The CLI Utility requires Java 8 or later. Verify that Java 8 is in the system PATH variable before running the Spatial CLI Utility.

---
After downloading CLI utility from the respective link kindly follow the steps mentioned below.

1. Extract the contents of the zip file.
2. Extracted content will have two directories i.e. ***bin*** and ***lib*** at root. ***lib*** directory contains necessary jar dependencies for execution and ***bin*** directory contains two files, one for Windows system and other one for Linux system.
3. To launch the command line interface, do one of the following:
   - If you are running the server on a Linux system, execute **spatial-cli**
   - If you are running the server on a Windows system, execute **spatial-cli.bat**

---
Connect to the Spatial Server cloud by typing this command:

```
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
- To auto-complete a command, type the first few characters then press the tab key. For example, typing `conn` then pressing the tab key automatically completes the command `connect`. Pressing the tab key again will display a list of all parameters for that command that can be used.
- If you specify an option value that contains a space, enclose the value in double quotes.

When you are done, type **exit** to exit the Spatial CLI Utility.

---
### limrepo  export
The limrepo export command exports named resources (such as named tables) from the Spatial Server repository to a local file system.

Resources are exported with their full repository paths in the target folder. For example, if you run `limrepo export --s /Samples/NamedTables --o C:\export`, the tool creates ***C:\export\Samples\NamedTables\WorldTable***, and so on for each named table under the NamedTables folder or directory.

#### Usage
```
limrepo  export  --s  SourceRepositoryPath  --o  OutputFilePath --a true
```
or simply
```
export  --s  SourceRepositoryPath  --o  OutputFilePath --a true
```
This is very basic example of this command with required parameters to execute the command.

> To see a list of parameters, type ```help "limrepo  export"``` or ```help export```



**Note:**\
The limrepo  export command will always recursively export all folders, including empty ones.

|  Argument |  Required | Description   |
| :------------ | :------------ | :------------ |
|  --s or source | Yes  |  Specifies the path to the resource or a folder to be exported. |
| --o or output  | Yes  | Specifies the path to a folder on the local file system where you want to export. This can be a new folder or an existing folder; however, an existing folder must be empty otherwise the export will fail.  |
| -q or --quiet  | No  | Disables the display of the resources copied during the export; that is, operates in quiet mode. <br>If the flag is not specified, then the default value is false.<br>If flag is specified then we must supply the value to be true or false otherwise error will be thrown.<br>Example if flag --q is specified then complete passed parameters should be **--q true** or **--q false**. Otherwise, Error will be thrown. |
| --f or --fullpaths  | No  | If the flag is not specified, then the default value is false. <br>If flag is specified, then we must supply the value to be true or false otherwise error will be thrown.<br>Example if --f is specified then complete values should be -**-f true** or **--f false**. Otherwise, Error will be thrown in command line.  |
| --r or --recursive  | No  | Recursively exports subfolders (children of the specified source).<br> Prints the full source and output paths.<br>If the flag is not specified, then the default value is true.<br>If flag is specified, then we must supply the value to be true or false otherwise error will be thrown.<br> Example if --r is specified then complete values should be **--r true** or **--r false**. Otherwise, Error will be thrown. |
| --c or --continueonerror  | No  | Continues with the export if an error occurs.<br>If the flag is not specified, then the default value is false. <br>If flag is specified, then we must supply the value to be true or false otherwise error will be thrown.<br>Example if --c is specified then complete values should be **--c true** or **--c false**. Otherwise, Error will be thrown. |
| --a or --acl  | No  | Preserves existing permissions for the exported resources in the export folder on the local file system. An access control list (ACL) indicates the operations each user or role can perform on a named resource, such as create, view, edit, or delete.<br>If the flag is not specified, then the default value is false. <br>If flag is specified, then we must supply the value to be true or false otherwise error will be thrown.<br> Example if --a is specified then complete values should be **--a true** or **--a false**. Otherwise, Error will be thrown.|

#### Example
Following example exports the named resources in the repository's \Samples folder to C:\myrepository\samples on your local file system.
```
limrepo export --s /Samples --o C:\myrepository\samples --a true
```
### Note

> If you are passing flag in that command then its value has to be be passed after the flag is written in the command. See example below

```limrepo export --s /Samples --o C:\myrepository\samples --r``` (No flag value for **--r** is specified hence error will be thrown)

Correct statement would be
```limrepo export --s /Samples --o C:\myrepository\samples --r true```
or
```limrepo export --s /Samples --o C:\myrepository\samples --r false```

Above statement needs to be followed for all the given flags **--q, --f, --r, --c, --a** if provided

---
### limrepo  import

The limrepo import command imports named resources (such as named tables) from a local file system into the Spatial repository.

When importing, you must point to the same folder or directory you exported to previously. For example, if you run `limrepo export  --s  /Samples/NamedTables  --o  C:\export`, the tool creates ***C:\export\Samples\NamedTables\WorldTable***, for each named table under the NamedTables folder or directory. Resources are exported with their full repository paths in the target folder. Running `limrepo import  --s  C:\export` then imports WorldTable back to ***/Samples/NamedTables/WorldTable***.

**Note:**\
The limrepo import command will always recursively import all folders, including empty ones.

#### Usage
```
limrepo import  --s  SourceFilePath
```
or simply
```
import  --s  SourceFilePath
```
This is very basic example of this command with required parameters to execute the command.
> To see a list of parameters, type ```help "limrepo  import"``` or ```help import```

|  Argument |  Required | Description   |
| :------------ | :------------ | :------------ |
|--s or source|Yes|Specifies the path to the resource or a folder on the local file system that is to be imported. This must be the root folder of a previous export on the local file system.|
|--q or --quiet|No|Disables the display of the resources copied during the import; that is, operates in quiet mode.<br>If the flag is not specified, then the default value is false.<br>If flag is specified then we must supply the value to be true or false otherwise error will be thrown.<br>Example if flag --q is specified then complete passed parameters should be **--q true** or **--q false**. Otherwise, Error will be thrown in command line. |
|--u or --update|No|Specifies whether to overwrite existing resources if resources with the same name are already on the server.<br>If the flag is not specified, then the default value is true.<br>If the flag is not specified, then the default value is true.<br>If flag is specified then we must supply the value to be true or false otherwise error will be thrown.<br>Example if --u is specified then complete values should be **--u true** or **--u false**. Otherwise, Error will be thrown in command line.  |
|--f or --fullpaths|No| Prints the full source and output paths.<br>If the flag is not specified, then the default value is false.<br>If flag is specified then we must supply the value to be true or false otherwise error will be thrown.<br>Example if flag --f is specified then complete passed parameters should be **--f true** or **--f false**. Otherwise, Error will be thrown in command line.  |
|--c or --continueonerror|No| Continues with the import if an error occurs.<br>If the flag is not specified, then the default value is false.<br>If flag is specified then we must supply the value to be true or false otherwise error will be thrown.<br>Example if flag --c is specified then complete passed parameters should be **--c true** or **--c false**. Otherwise, Error will be thrown in command line.  |

#### Example
This example imports the named resources from C:/myrepository/samples on your local file system.
```limrepo import --s C:/myrepository/samples```

### Note

> If you are passing flag in that command then its value has to be be passed after the flag is written in the command. See example below

```limrepo import --s C:/myrepository/samples --u``` (No flag value for **--u** is specified hence error will be thrown)

Correct statement would be
```limrepo import --s C:/myrepository/samples --u true```
or
```limrepo import --s C:/myrepository/samples --u false```

Above statement needs to be followed for all the given flags **--q, --f, --u, --c** if provided

---
#### Current Limitation of CLI Utility

In Windows system backward single slash `\` doesn't work in the **import** command for example `limrepo import --s C:\myrepository\samples` will throw an error of path not found. So either we have to provide forward slashes i.e.  `/` in between the path or provide double backward slashes `\\`

**Here is an example**

`limrepo import --s C:\\myrepository\\samples` (with double backward slashes)

`limrepo import --s C:/myrepository/samples` (with forward slashes)
