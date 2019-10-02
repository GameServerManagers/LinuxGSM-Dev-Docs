# Directories



All LinuxGSM directories are set through the following variables.

* `${rootdir}` \| The top level directory for LinuxGSM
* \|\_\_ `${lgsmdir}` \| `${rootdir}/lgsm` \|Contains all LinuxGSM related files
* \| \\_\_ `${functionsdir}` \| `${lgsmdir}/functions` \| All LinuxGSM script functions
* \| \\_\_ `${libdir}` \| `${lgsmdir}/lib` \| Any lib files required for game servers
* \| \\_\_ `${tmpdir}` \| `${lgsmdir}/tmp` \| Temp directory
* \| \\_\_ `${backupdir}` \| `${lgsmdir}/backups` \| Backups are saved here
* \|\_\_ `${serverfiles}` \| `${rootdir}\serverfiles` \| Game server files
* \|\_\_ `${logdir}` \| `${rootdir}\log` \| Logs directory
* \|\\_\_ `${scriptlogdir}` \| `${logdir}\script` \| LinuxGSM specific logs
* \|\\_\_ `${consolelogdir}` \| `${logdir}\console` \|  TMUX \(console output\) logs
* \|\\_\_ `${gamelogdir}` \| `${systemdir}/logs` \| symbolic link to game logs

### Server Specific Directories

Each game server also has its own specific directories these are defined through the following variables

### Server Specific Directories

* `${systemdir}` \| `${serverfiles}/ShooterGame` \|
* `${executabledir}` \| `${systemdir}/Binaries/Linux` \| Location of the binary file
* `${executable}` \| `./ShooterGameServer` \| The binary file
* `${servercfgdir}` \| `${systemdir}/Saved/Config/LinuxServer` \| Server config location
* `${servercfg}` \| `GameUserSettings.ini` \| Server config name
* `${servercfgdefault}` \| `GameUserSettings.ini` \| Default Server config name
* `${servercfgfullpath}`\| `${servercfgdir}/${servercfg}` \| Default Server config location

