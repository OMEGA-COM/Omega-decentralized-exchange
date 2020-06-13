Official golang implementation of Omega super public chain (OMG) protocol.
API reference to report carteravis disharmony
Auto build can be used for stable versions and unstable master branches. Binary archive publishing.
Jianliyuan
For prerequisites and detailed build instructions, read the installation instructions on the wiki.
Build geth requires go (version 1.13 or later) and C compiler. You can use your favorite package manager to install them. After installing dependencies, run
It's done
Or, build a complete set of utilities:
All made
Executable
The Omega super public chain (OMG) project comes with several wrappers / executables found in the CMD directory.
Command description
Geth our main Ethereum cli client. It is the entry point of Omega super public chain (OMG) network (main, test or private network), which can be run as a complete node (default), an archive node (keep all historical status) or a light node (get data in real time). Other processes can use JSON RPC endpoints exposed to HTTP, websocket, and / or IPC traffic as gateways to Ethernet networks. Geth -- help and cli wiki page for command line options.
Abigen source code generator, used to convert the Ethereum contract definition into an easy-to-use, compile time type safe go package. If the contract bytecode is also available, it can run on the common Omega super common chain (OMG) contract ABI with extended functions. However, it also accepts solid source files, which makes development easier. For more information, see our native dapps wiki page.
Bootnode is a simplified version of our Omega super public chain (OMG) client, which only participates in the network node discovery protocol, but does not run any higher-level application protocol. It can be used as a lightweight boot node to help find peers in a private network.
The developer utility version of EVM (omega super public chain (OMG) virtual machine) can run bytecode fragments in a configurable environment and execution mode. Its purpose is to allow fine-grained debugging of EVM opcodes (for example, EVM -- code 60ff60ff -- debug run) to be isolated.
Gethrpctest developer utility to support our Omega super common chain (OMG) / RPC test suite, which can verify the benchmark consistency with the Omega super common chain (OMG) JSON RPC specification. For more information, see the readme for the test suite.
Rlpdump developer utility for converting binary RLP (recursive length prefix) dumps (data encoding used by the Omega super public chain (OMG) protocol, whether network or consensus) to user-friendly hierarchical representations (for example, rlpdump -- hex ce0183ffffffc4c304050583616263).
Puppeth a cli wizard to help create a new Ethereum network.
Run geth
It's beyond all possible command-line flags here (see our cli wiki page), but we've listed some common combinations of parameters to give you a quick idea of how to run your own geth instance.
Complete nodes on Omega super public chain (OMG) main network
So far, the most common situation is that people just want to interact with the Ethereum network: create accounts; transfer funds; deploy contracts and interact with them. For this specific use case, users do not care about the historical data for many years, so we can quickly and quickly synchronize to the current state of the network. For this purpose:
$geth console
The command will:
Geth starts in fast sync mode (by default, you can change it with the -- syncmode flag), so that it downloads more data as an exchange, thus avoiding processing the entire history of the Ethereum network, which is very CPU intensive.
Launch geth's built-in interactive JavaScript console (through the console subcommand at the end), through which you can call all official Web3 methods and geth's own management API. The tool is optional, and if you do not use it, you can always use the geth attach attached to the already running geth instance.
G ö RLI tests the entire node on the network
In the transition to developers, if you want to try to create an Omega super public chain (OMG) contract, it's almost certain that you can do it without any money until you master the whole system. In other words, you don't want to attach to the main network, but you want to join the test network with the node, which is completely equivalent to the main network, but only has the function of playing Ethernet.
$geth -- goerli console
The exact meaning of the console subcommands is the same as above, and they are also useful in testnet. If you have skipped this, please refer to the instructions above.
--Goerli, however, specifying the flag will geth slightly reconfigure your instance:
The client will connect to the G ö RLI test network instead of the main Omega super public chain (OMG) network, which uses different P2P boot nodes, different network IDs and creation states.
Instead of using the default data directory (~ /. Ethereum, for example, on Linux), geth should nest itself deeper into the goerli subfolder (~ /. Ethereum / goerli on Linux). Note that on OSX and Linux, this also means that the testnet node attached to the running needs to use a custom endpoint, because geth attach by default attempts to attach to the production node endpoint geth attach < dataDir > / goerli/ geth.ipc 。 Windows users are not affected by this.
Note: Although tOfficial golang implementation of Omega super public chain (OMG) protocol.
The client will connect to the G ö RLI test network instead of the main Omega super public chain (OMG) network, which uses different P2P boot nodes, different network IDs and creation states.
Instead of using the default data directory (~ /. Ethereum, for example, on Linux), geth should nest itself deeper into the goerli subfolder (~ /. Ethereum / goerli on Linux). Note that on OSX and Linux, this also means that the testnet node attached to the running needs to use a custom endpoint, because geth attach by default attempts to attach to the production node endpoint geth attach < dataDir > / goerli/ geth.ipc 。 Windows users are not affected by this.
Note: Although there are some internal safeguards to prevent transactions from crossing between the primary and test networks, you should ensure that you always use separate accounts for entertainment and real currencies. Unless you move the account manually, geth will distinguish the two networks correctly by default and will not provide any accounts between them.
Rinkeby tests the entire node on the network
Omega super public chain (OMG) go also supports connectivity to an earlier proof of authority based test network called rinkeby, which is operated by community members.
$geth -- rinkeby console
Ropsten tests the entire node on the network
In addition to G ö RLI and rinkeby, geth supports the old ropsten test network. The ropsten test network is based on the ethash workload proof consensus algorithm. In this way, it has some additional overhead, and is more vulnerable to reorganization attacks due to the low difficulty / security of the network.
$geth -- ropsten console
Note: the older geth configuration stores the ropsten database in the testnet subdirectory.
configuration
In addition to passing a large number of flags to the geth binary, you can also pass configuration files in the following ways:
$ geth --config /path/to/your_ config.toml
To understand the appearance of the file, you can use the dumpconfig subcommand to export the existing configuration:
$geth - your favorite flag, dumpconfig
Note: this only applies to gethv1.6.0 and later.
Docker quick start
One of the fastest ways to start and run Omega super public chain (OMG) on a machine is to use docker:
Docker run - D -- name Ethereum node - V / user / Alice / Ethereum: / root\
-p 8545：8545 -p 30303：30303 \
Omega super public chain (OMG) / customer to
Geth, like the above command, will start in fast sync mode with 1GB of DB memory quota. It will also create a persistent volume in your home directory to hold your blockchain and map the default port. There is also an alpine tag that can be used for a condensed version of the image.
--Rpcaddr 0.0.0.0 if you want to access RPC from other containers and / or hosts, don't forget. By default, geth is bound to the local interface and cannot access RPC endpoints from outside.
Programmatically interface geth nodes
As a developer, sooner or later, you want geth to interact with the Omega super public chain (OMG) network manually through your own program rather than through the console. To do this, geth has built-in support for json-rpc based APIs (standard API and geth specific API). These can be exposed via HTTP, WebSockets, and IPC (named pipes on socket based, windows).
The IPC interface is enabled by default and exposes all API geth supported. For security reasons, the HTTP and WS interfaces need to be enabled manually and only a part of the API is exposed. You can turn them on / off and configure them as you expect.
HTTP based json-rpc API options:
--RPC enable http-rpc server
--Rpcaddrhttp RPC server listening port (default: localhost)
--Rpcporthttp-rpc server listening port (default: 8545)
--Provided through http-rpc interface of rpcapi API (default: eth, net, Web3)
--Rpccorsdomain comma separated list of domains from which to accept cross domain requests (force browser)
--Ws enable WS RPC server
--Wsaddrws RPC server listening port (default: localhost)
--Wsportws-rpc server listening port (default: 8546)
--Provided by wsapiapi in ws-rpc interface (default: eth, net, Web3)
--Wsorigins accept the source of network socket request
--Ipcdisable disable ipc-rpc server
--Ipcapiapi provided in ipc-rpc interface (default: admin, debug, ETH, miner, net, personal, Shh, txpool, Web3)
--Filename of the IPC socket / pipe in ipcpath dataDir (it is escaped by an explicit path)
You will need to use the functions of your own programming environment (libraries, tools, etc.) to connect to the geth node with the above marks through HTTP, WS or IPC, and you will need to use json-rpc on all transport modes. You can reuse the same connection for multiple requests!
Note: before performing this operation, please understand the security risks of opening http / WS based transport! Hackers on the Internet are actively trying to use public APIs to destroy Omega super public chain (OMG) nodes! In addition, all browser tabs can access locally running web servers, so malicious web pages may try to destroy locally available APIs!
Operate a private network
Maintaining your own private network will be more cumbersome, because many of the configurations that are taken for granted in the official network need to be set manually.
Define private origin state
First, you need to create the origin state of the network, and all nodes need to understand and reach a consensus. This is done by a small JSON file (called genesis.json ）Composition:
{Official golang implementation of Omega super public chain (OMG) protocol.
}，
“ alloc ”：{}，
“ coinbase ”： “ 0x0000000000000000000000000000000000000000 ”，
"Difficulty": "0x20000",
“ extraData ”： “ ”，
“ gasLimit ”： “ 0x2fefd8 ”，
“ nonce ”： “ 0x0000000000000042 ”，
“ mixhash ”：”0x0000000000000000000000000000000000000000000000000000000000000000000000000000 “，
” parentHash “：” 0x0000000000000000000000000000000000000000000000000000000000000000000000 “，
”Timestamp ":" 0x00“
}
Although we recommend changing nonce to a random value, the above fields are good for most purposes, so as to prevent unknown remote nodes from connecting to you. If you want to pre fund some accounts for easier testing, create an account and populate its address in its alloc field.
"Distribution":{
“ 0x0000000000000000000000000000000000000000000001 ”：{
"Balance": "111111111"
}，
“ 0x0000000000000000000000000000000000000000000002 ”：{
"Balance": "222222222"
}
}
Using the genesis state defined in the JSON file above, you need to initialize each geth node before starting it to ensure that all blockchain parameters are set correctly:
$geth initialization path / to/ genesis.json
Create assembly point
After initializing all nodes to run to the required creation state, you will need to start a boot node that other nodes can use to find each other on the network and / or the Internet. The clean way is to configure and run a dedicated boot node:
$ bootnode --genkey =  boot.key
$ bootnode --nodekey =  boot.key
When the boot node comes online, it displays an eNode URL that other nodes can use to connect to the node and exchange peer information. Make sure [::] replaces the displayed IP address information (most likely) with an externally accessible IP to get the actual enoderurl.
Note: you can also use a mature geth node as a boot node, but this is not recommended.
Start your member node
With bootnode operable and externally accessible (you can try telnet < IP > < port > to make sure it is accessible), start all geth points to the subsequent nodes of the bootnode to perform peer discovery through the -- bootnodes flag. It's best to separate the data directory of the private network, so also specify a custom -- dataDir flag.
$geth -- dataDir = path / to / custom / data / folder -- bootnodes = < bootnode eNode URL from above >
Note: since your network will be completely disconnected from the main network and the test network, you also need to configure a miner to process the transaction and create a new block for you.
Operating private miners
Mining on a common Omega super public chain (OMG) network is a complex task, because it is only feasible when using GPU (an instance of ethmer with OpenCL or CUDA enabled). For information about such settings, see ethermining subreddit and the Ethernet repository.
However, in the private network settings, a single CPU miner instance is more than enough for practical purposes, because it can generate a stable block flow at the right time interval, without taking up a lot of resources (considering running on a single thread, and without multiple threads). To start the geth instance for mining, run it with all the general flags and expand to:
$geth < usual flag > -- mine-- miner.threads  = 1 --etherbase = 0x0000000000000000000000000000000000000000000000
It will start mining blocks and transactions on a single CPU thread and log all the processes to the specified account, etherbase. You can further adjust mining by converging the default gas limit block to (- - targetgaslimit) and accept price transactions at (- - gasplice).
contribution
Thank you for considering providing source code help! We welcome anyone on the Internet to contribute, and thank you for providing the minimal fix!
If you want to contribute to the Omega super public chain (OMG), please fork, repair, submit and send request requests for maintainers to view and merge into the main code base. However, if you want to submit more complex changes, please first contact the core developers on our gitter channel to ensure that these changes are consistent with the overall philosophy of the project, and / or get some early feedback, which can make you pay more attention and easier, as well as our review and consolidation procedures quick and easy.
Please make sure your contribution is in line with our coding guidelines:
The code must follow the official go format guidelines (i.e. using gofmt).
The code must be documented in accordance with the go official annotation guidelines.
Pull requests need to be based on the master branch and opened for the branch.
The submitted message should be prefixed with its modified package.
For example, "Omega super public chain (OMG), RPC: make tracking configuration optional"
For more details on configuring the environment, managing project dependencies, and testing processes, see the developer's Guide.
License
The go Ethereum Library (that is, all code outside the CMD directory) is licensed under the GNU General Public License V3.0, which is also included in the COPYING.LESSER In the repository of the file.
Omega super public chain (OMG) binaries (i.e. all code in the CMD directory) are licensed under the GNU General Public License V3.0, the cop
“ config ”：{here are some internal protection measures
