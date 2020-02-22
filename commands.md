# HyperLedger Command Line Utilities

## Cryptogen

```
General format
cryptogen command --flags <args>

Help
cryptogen help
cryptogen command --help or  cryptogen help command

Version
cryptogen version

Check configuration template
cryptogen showtemplate

Generate Certificates
cryptogen generate --config=<<configuration file path>> --output=<<output folder path>>

Extending the present configuration
cryptogen extend --config=<<extension config file>> --input=<<input folder>>
```

## Configtxgen

```
General format
configtxgen  command [flags]

Help
configtxgen -help

Version
configtxgen -version

Genesis block 
configtxgen -outputBlock <<file name>> -profile <<profile name>> -channelID <<channel name>>
configtxgen -inspectBlock <<block file name>>

Channel Transaction
configtxgen -outputCreateChannelTx <<file name>> -profile <<profile name>> -channelID <<channel name>>
configtxgen -inspectChannelCreateTx <<Tx file name>>

Anchor Peer Transaction
configtxgen -outputAnchorPeersUpdate <<file name>> -profile <<profile name>> -channelID <<channel name>> -asOrg <<Organization Name>>
configtxgen -inspectChannelCreateTx

Printing information on Organization
configtxgen -printOrg << Organization Name >>
```

## orderer
```
Start orderer process
orderer
```

## peer
```
General format
peer command subcommand --flags
```
|command     | description                    |
|------------|--------------------------------|
|help        | Get help on commands           |
|version     | Version of the peer binary     |
|node        | start/ status                  |
|logging     | get/set/revert log levels      |
|channel     | Carry out channel operations   |
|chaincode   | Carry out chaincode operations |
```
Help
peer help or peer -h | --help
peer command help

Version
peer version

Node
peer node start | status
killall peer

Logging
peer logging getlevel <<module name>>
peer logging setlevel <<module name>> <<log level>>
peer logging revertlevel

Channel operations
```
|command        | description                                       |
|---------------|---------------------------------------------------|
|create         | Create channel on the network                     |
|join           | Peer joins the specified channel                  |
|list           | Lists the channel that the peer has joined        |
|fetch          | Performs a operation on orderer to fetch a block  |
|getinfo        | Get information on the specified channel          |
|signconfigtx   | For signing the config transaction file           |
|update         | Updating the existing channel config              |

```
peer channel create -o <<orderer address>> -c <<channel name>> -f <<path to create channel transaction>> -t <<Optional timeout>>
peer channel join -o <<orderer address>> -b <<path to block response>>
peer channel list

peer channel getinfo -c <<channelid>> 
peer channel fetch command -o <<orderer address>> -c <<channelid>> -o <<orderer address>> <<optional output file>>
```
|command              | description                                              |
|---------------------|----------------------------------------------------------|
|newest               | Fetches the latest block                                 |
|oldest               | Fetches the oldest block                                 |
|Block Number         | Fetch by block Number                                    |
|config               | Gets the latest config block. Also provides bock number  |
```
peer channel signconfigtx --flags
peer channel signconfigtx -f <<Transaction File>>

peer channel update -f <<signed transaction file>> -c <<channel id>> -o <<orderer url>>

peer chaincode install --flags
```
|flag                 | description                                              |
|---------------------|----------------------------------------------------------|
|-n --name            | Name and version of chaincode being installed            |
|-v --version         | Version: alphabets, numbers, dash, underscore, plus      |
|-l --lang            | golang (default), nodejs                                 |
|-p --path            | Path to code depends on lang specified                   |
```
peer chaincode install -n gocc -v 1.0 -p chaincode_example

peer chaincode instantiate --flags
```
|flag                 | description                                                                          |
|---------------------|--------------------------------------------------------------------------------------|
|-n --name            | Name and version of chaincode being installed                                        |
|-v --version         | Version: alphabets, numbers, dash, underscore, plus                                  |
|-c --ctor            | default{}  constructor parameter in json format                                      |
|-C --channelId       | channel on which chaincode is instantiated                                           |
|-P --policy          | Endorsement policy of chaincode, Default (Any member of org that is part of channel) |
|-E --escc            | Name of the endorsement system chaincode (default: 'escc')                           |
|-V --vscc            | Name of the verification system chaincode (default: 'vscc')                          |

```
peer chaincode instantiate -n gocc -v 1.0 -C org1org2channel -c '{"Args": ["init","a","100","b","200"]}'

peer chaincode list --installed
peer chaincode list --instantiated -C <<channel id>>

peer chaincode upgrade -n gocc -v 2.0 -C org1org2channel -c '{"Args": ["init","a","100","b","200"]}'
Note: instantiate flags are also applied here

peer chaincode query --flags
```
|flag                 | description                                                                          |
|---------------------|--------------------------------------------------------------------------------------|
|-n --name            | Name and version of chaincode being installed                                        |
|-c --ctor            | default{}  constructor parameter in json format                                      |
|-C --channelId       | channel on which chaincode is instantiated                                           |

```
peer chaincode invoke --flags
```
|flag                 | description                                                                          |
|---------------------|--------------------------------------------------------------------------------------|
|-n --name            | Name and version of chaincode being installed                                        |
|-c --ctor            | default{}  constructor parameter in json format                                      |
|-C --channelId       | channel on which chaincode is instantiated                                           |

```
peer chaincode package  --flags <<file name>>
Note: same flags as install command
-i --instantiate-policy } instantiation policy (Still under development)
peer chaincode install <<package file>>
```

## configxlator

2 mode
* Command line interface
* Rest server

* No configuration file for this tool

```
To start as a rest server

configxlator start --hostname localhost --port 7059

Command Line

configxlator command --flags
configxlator help
configxlator command --help
configxlator version
```
|command                 | description                                          |
|------------------------|------------------------------------------------------|
|proto-decode            | protobuf => json                                     |
|proto-encode            | json => protobuf                                     |
|compute_update          | delta between 2 protobuf                             |

|flags       | description                                                                                    |
|------------|------------------------------------------------------------------------------------------------|
|--type      | Type of protobuf structure to encode/decode (common.(Block,Config,Envelope,Configupdate,policy)|
|--input     | protobuf or json                                                                               |
|--output    | protobuf or json                                                                               |
|--origninal | use with compute_update (original config file)                                                 |
|--updated   | use with compute_update (updated config file)                                                  |
|--channel_id| use with compute_update (updated config file)                                                  |

### fabric-ca-server
```
fabric-ca-server command --flags

fabric-ca-server version 
fabric-ca-server init 
fabric-ca-server start
fabric-ca-server --help

fabric-ca-server command --help
```                            
|flag                 | description                                          |
|---------------------|------------------------------------------------------|
|-d --debug           | To enable debug level logging                        |
|-b --boot            | Bootstrap identity                                   |
|--address            | Listening address. Default => 0.0.0.0                |   
|-p                   | Listening port Default => 7054                       |
|-n --ca-name         | Name for the CA                                      |
```
Other related flag domains

Certificate => CA certificate setup
TLs => Transport Layer Security
CSR => Certificate Signing Request
Database => DB config for cluster setup
LDAP => LDAP config for cluster setup
Intermediate CA => ICA configuration

CA server can launch without initializing - Good for testing
fabric-ca-server start -b admin:adminpw

Config can be provided by way of flags | environment | YAML (in order of precedence)
```

### fabric-ca-client
```
fabric-ca-client command --flags

fabric-ca-client version
fabric-ca-client --help
fabric-ca-client command --help
```
|command        | description                             |
|---------------|-----------------------------------------|
|getcainfo      | get CA information                      |
|identity       | Manage the identities                   |
|register       | Register an identity                    |   
|enroll         | Enroll an identity                      |
|reenroll       | Re-Enroll an identity                   |
|affiliation    | Manage affiliation                      |   
|certificate    | Manage certificates                     |
|revoke         | Revoke identity                         |
|gencrl         | Generate certificate revocation req     |
|gencsr         | Generate certificate signing request    |   
