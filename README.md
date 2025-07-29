# Encrypted Directory

Using `ecryptfs-utils` this Bash script makes a setup for an encrypted environment inside of the created ecryptfs directory. It works out-of-the-box under Arch Linux based systems. Also it supports sound feedback using `sox` and autmatic unmounting using timeout settings and more.

## <u> Getting Started </u>

Execute `./src/main.sh`. It's using *Pacman* to install requirements if needed. After the script was executed, inside of the encrypted environment you can create your own `.bashrc` and if your exiting the shell using `exit` the encrypted directory will be automaticly unmounted (default) and environment variables like `$HOME` will be set to default.

### Dependencies

The required packages for the complete support of every feature (some are optional like sound feedback) can be found within the `./src/setup.sh`.

* `sox`
* `ecryptfs`
* `firefox`

### Setting Up

As explained normally the script installs the dependencies automaticly and finds the location of the encrypted directory by itself.

```bash
#!/bin/bash
git clone git@github.com:TheUnixDemon/EncryptedDirectory.git && ./EncryptedDirectory/src/main.sh 
```

For using this script later on look into [Start Script](#shelllevelonetwo). Also if you want to use the [arguments](#args) inside of the encrypted environment that you will enter after starting the script, make use of the explaination inside of [**Private Directory**](#shelllevelthree) to load this script inside of the same shell level. Furthermore to check or alter the settings of this script go to [**Settings**](#settings).

<a name="args"></a>
### Arguments

The script `./src/main.sh` supports some arguments like ...

* `-u` - unmount encrypted directory
* `-p` - copying from encrypted directory to `./preset`
* `-f` - starting a Firefox instance inside of encrypted environment

```bash
#!/bin/bash
./src/main.sh -f # starting firefox
```

<a name="shelllevelonetwo"></a>
### Start Script        **»** Shell Level *One* to *Two*

You start the script in a sub shell when you are in Shell level **1**. So it will load up it's variables outside of your first shell.

```bash
#!/bin/bash
./src/main.sh"
```

<a name="shelllevelthree"></a>
### Private Directory   **»** Shell Level *Three*

If you are within the private environment you are within the shell level **3**. So you should load scripts using `source`. (`$WORKINGDIR` - script location)

```bash
#!/bin/bash
SCRIPT=$(cd "$WORKINGDIR" && source "main.sh")
```

<a name="settings"></a>
## <u> Settings </u>

As explained at the beginning, you can alter the default settings at `./src/env.sh`.

```bash
#!/bin/bash 

...
# options
SOUND="false"       # enable/disable sox notification feedback for unmounting
TIMEOUT="false"     # automaticly umount after TLIMIT if no inteference
TLIMIT=60           # time limit
USE_FIREFOX="false" # automaticly starting firefox after mounting the encrypted directory
```

If `TIMEOUT="true"` and `TLIMIT=60` every sixty secounds the script will check if a process is using the encrypted directory. If not the mounted directory will be unmounted afterwards. Also If you have set `SOUND="true"` a sound will accure to notify you that your encrypted directory was successfully unmounted.