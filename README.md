# JDK Version Manager (JVMS)

Manage multiple installations of JDK on your machine.

There are situations where the ability to switch between different versions of JDK can be very
useful. For example, if you want to test a project you're developing with the latest
bleeding edge version without uninstalling the stable version of JDK, this utility can help.

## Installation
- Download the latest release
- Decompress the zip file and copy the executable to a path of your choice
- Run the initialization command: `jvms init`
- Setup is complete! Switch and install JDK versions using the commands below

## Usage
```shell
NAME:
   jvms - JDK Version Manager

USAGE:
   jvms [global options] command [command options] [arguments...]

COMMANDS:
     init        Initialize config file
     list, ls    List the JDK installations
     install, i  Install remote available JDK
     switch, s   Switch to use the specified version
     remove, rm  Remove a specific version
     rls         Show a list of versions available for download
     proxy       Set a proxy to use for downloads
     help, h     Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h     show help
   --version, -v  print the version
```

### Example Commands
- `jvms rls` - List available JDK versions for download
- `jvms install 1.8.0_31` - Install JDK 1.8.0_31
- `jvms ls` - List installed JDK versions
- `jvms switch 1.8.0_31` - Switch JDK version to 1.8.0_31

## JDK Sources and Version Policy

JVMS supports multiple JDK distributions to give you flexibility in choosing your preferred JDK:

### Supported JDK Distributions

1. **Oracle JDK** - Included in default index (LTS versions only)
2. **Amazon Corretto** - Included in default index (LTS versions only)
3. **Adoptium (Eclipse Temurin)** - Available via API, dynamically fetched
4. **Azul Zulu** - Available via API, dynamically fetched

### LTS-Only Policy

The default index only includes **LTS (Long-Term Support)** versions:
- Java 8
- Java 11
- Java 17
- Java 21
- Java 25

Non-LTS versions are not included in the default index as they reach end-of-life in 6 months.

However, you can still install non-LTS versions if needed:
- Use `jvms rls` to see all available versions (including non-LTS from Adoptium and Azul)
- Add your own local JDK versions (see below)
- Set up a custom download server with your preferred versions

## Key Features

- No dependency on other libraries
- Simple and straightforward command-line interface
- Persistent version switching (no need to run `jvms switch` every time you open a console)
- Automatically updates across all open console windows
- Persists between system reboots

## Adding a Local JDK Version

To add a local JDK version:

1. Copy the JDK home folder to `jvms/store`
2. Rename the folder to the version number (e.g., `17.0.1`)
3. Run `jvms list` to verify the installation
4. Run `jvms switch <version>` to use the new version
5. Run `java -version` to confirm the switch

## Creating Your Own Local Download Server

1. Create a JSON file (e.g., `index.json`)
2. Add your JDK download links to it in the following format:
   ```json
   [
     {
       "version":"1.9.0",
       "url":"http://your-server/files/jdk/1.9.0.zip"
     }
   ]
   ```
3. Host this file on a static file server (e.g., nginx, Apache)
4. Run `jvms init --originalpath http://your-server/files/index.json`
5. Now you can use `jvms rls` and `jvms install` with your custom versions

### Creating a JDK Zip File

1. Open the JDK home folder
2. Compress all files to a `*.zip` file
3. Copy the zip file to your server
4. Add the zip file link to your index.json

## License

MIT.