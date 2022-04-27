# MPTCP POX Controller

## Installation of required packages
1. Run `sudo bash install.sh` to install Ripl and Riplpox

### Tests with Jellyfish:

1. Run the following command:

  `pox/pox.py riplpox.riplpox --topo=jelly,20,4,adjList_4links_20sw --routing=jelly,ecmp_4links_20sw --mode=reactive`

2. Open another terminal, re-enter the git directory and run

`./jelly_flows.sh`

	> Note: [N_FLOWS] represents the number of TCP flows that will be used in the tests, in the example there are 8 flows.

	> Note: [MN_SCRIPT_FILE] is the name of the Mininet script file that will be created when running the command, so the file does not need to exist (it will be created).

3. Start Mininet with the command 

`sudo mn --custom ripl/ripl/mn.py --topo jelly,20,4,adjList_4links_20sw --link tc --controller=remote --mac`

4. In the Mininet CLI run `source [MN_SCRIPT_FILE]`.

  `source jelly_mn_script_ecmp_1flows`
  `source jelly_mn_script_ecmp_2flows`
  .
  .
  `source jelly_mn_script_ecmp_8flows`

5. The result will be in the outputs/jelly directory.

### Tests with the Fat-Tree:

1. Run `python pox/pox.py DCController --topo=ft,[N_PODS] --routing='[ROUTE_PROTO]'`

	Example `python pox/pox.py DCController --topo=ft,4 --routing=ECMP`

2. Open another terminal and run `./fat_flows.sh`

	Example `python generate_cmds_fat.py 4 8 ecmp > fat_mn_script_ecmp_8flows`

3. Start Mininet with the command `mn --custom ripl/ripl/mn.py --topo ft,[N_PODS] --controller=remote --mac --link tc,bw=10,delay=10ms`

	Example `mn --custom ripl/ripl/mn.py --topo ft,4 --controller=remote --mac --link tc,bw=10,delay=10ms`

4. In the Mininet CLI run `source [MN_SCRIPT_FILE]`.

  `source fat_mn_script_ecmp_1flows`
  `source fat_mn_script_ecmp_2flows`
  .
  .
  `source fat_mn_script_ecmp_8flows`

5. The result will be in the outputs/fat directory.
