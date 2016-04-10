OBC Mortgage Demo
=================
Contact Andreas Kind @IBM, 2016

Unzip content of "OBC Mortage Demo Sources v09.zip" in YOUR_WWW_PATH  

$ mkdir $GOPATH/src/github.com/openblockchain/obc-peer/openchain/example/chaincode/chaincode_mortgage/  
$ cp chaincode_mortgage.go $GOPATH/src/github.com/openblockchain/obc-peer/openchain/example/chaincode/chaincode_mortgage/  

## Window 0: Start certificate authority
$ cd <WORKSPACE>/obc-dev-env  
$ vagrant ssh  
> cd $GOPATH/src/github.com/openblockchain/obc-peer/obc-ca  
> go build -o obcca-server  
> ./obcca-server  

## Window 1: Start peer
$ cd <WORKSPACE>/obc-dev-env  
$ vagrant ssh  
> cd $GOPATH/src/github.com/openblockchain/obc-peer  
> OPENCHAIN_SECURITY_ENABLED=true OPENCHAIN_SECURITY_PRIVACY=true ./obc-peer peer --peer-chaincodedev  

## Window 2: Run compile, start and validate chaincode
$ cd <WORKSPACE>/obc-dev-env  
$ vagrant ssh  
> cd $GOPATH/src/github.com/openblockchain/obc-peer/openchain/example/chaincode/chaincode_mortgage  
> go build  
> OPENCHAIN_CHAINCODE_ID_NAME=myMortgage OPENCHAIN_PEER_ADDRESS=0.0.0.0:30303 ./chaincode_mortgage  

## Window 3: Start web server
Create file server.js:  
> var connect = require('connect');  
> var serveStatic = require('serve-static');  
> connect().use(serveStatic('YOUR_WWW_PATH')).listen(8080);

node server.js  

## Open mortgage application
Start web browser  
> http://localhost:8080/mortgage_VERSION.html 
