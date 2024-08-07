# Debuggins

## Testing and debugging your code

### Working from your own GitHub branch

You will usually be developing onto your own repo. Using your own repo instead of the original one is quite easy.

1. Display your main "gameserver" file on GitHub, and select "Raw".
2. Make a test user, login to it
3. wget your Raw link and chmod +x the script.
4. Edit your "gameserver" file by changing GitHub information to your username and repo and branch.

    ```bash
    ## Github Branch Select
    # Allows for the use of different function files
    # from a different repo and/or branch.
    githubuser="YourUsername"
    githubrepo="YourRepository"
    githubbranch="YourBranchName"
    ```

Now, any command you run will get your own GitHub files, and after any change you make on your repo, `./gameserver uf` will grab new files. If you make a change and that `./gameserver uf` don't get them, it means you were too quick, and that your curl still has old files in cache; in this case, you'll need to wait a few minutes to get your modifications.

### How to test

You need to make sure that all needed commands displayed in opt work properly. So just run `./gameserver` to show available commands, then try commands one by one. A common procedure is to first work on command_install, then start, then stop, then debug, then details, then monitor.

### Oops, I found a bug

If you found a bug, either you'll instantly know how to fix it, or you won't. And either it will be a bug caused by your own code or a bug into LinuxGSM itself. So let's address those cases.

1. It's caused by your own code parts and you know how to fix it: Just go on and fix it.
2. It's caused by your own code parts but you got no idea why: Use `./gameserver dev-debug` that will add a very detailed log into your rootdir that might help you figure this out. To disable the dev-debug mode, just re-run the command. If you still can't find why it's not working, come get help on Discord's #gsm-development channel or Github issue that might have been created for this issue.
3. You found a bug into LinuxGSM itself. First, you need to be sure that it's really a bug that affects every game, by testing with another game onto the original repo, otherwise, if it only affects your game, you will usually just need to add a clever conditional check to fix the issue.
