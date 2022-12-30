# HOW TO

After installing `docker` and `docker-compose`, you may download and run the install script manually, or use the following command:
```
curl -O https://gitlab.com/shardeum/validator/dashboard/-/raw/dashboard-gui-nextjs/installer.sh && chmod +x installer.sh && ./installer.sh
```

This will build the operator/dashboard image using an exisitng validator-server image.

The entryscript clones and installs the cli AND gui repos.

## Stack management
### Start the stack:
```
./docker-up.sh
```
#### This will be more effective when the info gathered in the install script is stored in persisent volume that is mounted by the container.

### Stop the stack:
```
./docker-down.sh
```

### Clean up
```
./clean.sh
```
#### this will clean up the last (lastest) build. Just meant to save a few key strokes.

# TODO

## User Experience
Instructions for the user wanting to run a Shardeum validator node will be:

### Initial Install
* Setup Docker on the machine that will be running the Shardeum validator (link to more info)
* From the command line run this command while logged in as the user that can run Docker commands
	curl URL | sh

Answer the questions to specify where the validator will save files and what ports it uses

If you chose to start the GUI you should have been given the URL to access it and set the password

### Start the GUI Manually

If you did not start the GUI or stopped it, you can start it again by following these steps

``` 
./shell.sh

operator-cli gui start
```

If the above command fails with an error that you have not set the GUI access password, run

```
operator-cli gui password
```

### Start or Stop the Validator Manually
```
./shell.sh

operator-cli status
operator-cli start
operator-cli stop
```

### Update the Validator software along with the Dashboard

Be sure that your validator is not participating in the network
```
./shell.sh

operator-cli status
operator-cli disable
```

This will set the Validator to not join the network after it has exited

Once it has exited, it will not try to rejoin since it has been disabled
```
./update.sh
```
This will stop the validator, remove the docker image, pull the current stable image and start the image; it will not need to ask questions about where to store the files and what ports to use since it will use the same settings as before

## Need to add instructions for Staking