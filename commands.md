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
command     | description                    |
----------------------------------------------
help        | Get help on commands           |
----------------------------------------------
version     | Version of the peer binary     |
----------------------------------------------     
node        | start/ status                  |
----------------------------------------------  
logging     | get/set/revert log levels      |
---------------------------------------------- 
channel     | Carry out channel operations   |
----------------------------------------------
chaincode   | Carry out chaincode operations |


