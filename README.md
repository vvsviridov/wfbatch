# WFBATCH - `wfcli` Ericsson ENM wrapper

## Usage

`wfbatch [options] <nodefile>|<nodelist>|<channelsdir>  <command(s)>|<commandfile>|<commanddir> [logdirectory]`

Purpose: To send wfcli commands to several nodes in parallel.

Arguments:

1. The first argument is the nodefile, nodelist or path to dir with channels files in xml format. The nodefile is a file containing the list of nodes to connect to. Each line in the nodefile contains node name as in topology. If using the nodelist, the nodes are listed on the command line and separated by commas.

2. The second argument is the commmands, commandfile or directory with command files. See example of commands below. Commands must be devided by pipe `|` symbol. If a directory is given, then a different commandfile will be used for each node:
    - the name of each commandfile should be `node-name`.cmd
    - the `node-name` should be the same as defined in ENM topology.
    - example: node-name is node602 ==> commandfile should be node602.cmd

3. The third argument (logdirectory) is optional. If no logdirectory is specified, a default one (~/winfiol/logfiles) will be used.

Options:

- `-p <processes>` Specify the maximum number of wfcli sessions that will run in parallel (default=20, maximum=20 parallel sessions)
- `-i <seconds>` Specify the interval in seconds between spawning of each wfcli session (default=1 second).
- `-w <seconds>` Specify the interval in seconds between the checks on running sessions (default=10 seconds)
- `-o` Print output of every wfcli session both to screen and to logfile.

## Examples

1. Starts wfbatch with bsc list in file and commands string:

    `wfbatch -o bscs.txt "mml|allip:alcat=apz;"`

2. Starts wfbatch with bscs and command files directory

    `wfbatch -o BSC001,BSC002 winfiol/commandfiles`

3. Starts wfbatch with bsc channels directory and command file

    `wfbatch -o winfiol/channels commands.cmd`
