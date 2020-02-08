# TN <-> Waves Platform Gateway Framework

Inspired by Hawky's Waves-ERC20 Gateway: https://github.com/PyWaves/Waves-ERC20-Gateway
But rewritten to be published under FOSS license.

This framework allows to easily establish a gateway between any Waves token and the
TN Platform.
## Installation
Clone this repository and edit the config.json file according to your needs. Install the following dependencies:
```
pycwaves
fastapi[all]
jinja2
aiofiles
```
via pip and run the gateway by
```
python start.py
```
## Configuration of the config file
The config.json file includes all necessary settings that need to be configured in order to run a proper gateway:
```
{
    "main": {
        "port": <portnumber to run the webinterface on>,
        "name": "Tokenname",
        "company": "Gateways Ltd",
        "contact-email": "info@contact.us",
        "contact-telegram": "https://t.me/TurtleNetwork",
        "recovery_amount": <minimum recovery amount>,
        "recovery_fee": <recovery fee in %>,
        "admin-username": "admin",
        "admin-password": "admin"
    },
    "waves": {
        "gatewayAddress": "<Waves address of the gateway>",
        "gatewaySeed": "<seed of the above devined address>",
        "seedenvname": "<the ENV name to store your seed instead of the field above>",
        "fee": <the fee you want to collect on the gateway, calculated in the proxy token, e.g., 0.1>,
        "gateway_fee": <the gatewway part of the fee calculated in the proxy token, e.g., 0.1>,
        "network_fee": <the tx part of the fee calculated in the proxy token, e.g., 0.1>,
        "assetId": "<the asset id of the proxy token on the Waves platform>",
        "decimals": <number of decimals of the token>,
        "network": "<Waves network you want to connect to (testnet|stagenent|mainnet)>",
        "node": "<the waves node you want to connect to>",
        "timeInBetweenChecks": <seconds in between a check for a new block>,
        "confirmations": <number of confirmations necessary in order to accept a transaction>
    },
    "tn": {
        "gatewayAddress": "<TN address of the gateway>",
        "gatewaySeed": "<seed of the above devined address>",
        "seedenvname": "<the ENV name to store your seed instead of the field above>",
        "fee": <the fee you want to collect on the gateway, calculated in the proxy token, e.g., 0.1>,
        "gateway_fee": <the gatewway part of the fee calculated in the proxy token, e.g., 0.1>,
        "network_fee": <the tx part of the fee calculated in the proxy token, e.g., 0.1>,
        "assetId": "<the asset id of the proxy token on the TN platform>",
        "decimals": <number of decimals of the token>,
        "network": "<Waves network you want to connect to (testnet|mainnet)>",
        "node": "<the TN node you want to connect to>",
        "timeInBetweenChecks": <seconds in between a check for a new block>,
        "confirmations": <number of confirmations necessary in order to accept a transaction>
    }
}
```

### Example config.json
```
{
    "main": {
        "port": 5060,
        "name": "TrueUSD",
        "company": "Gateways Ltd",
        "contact-email": "info@contact.us",
        "contact-telegram": "https://t.me/TurtleNetwork",
        "recovery_amount": 2000,
        "recovery_fee": 15,
        "admin-username": "admin",
        "admin-password": "admin"
    },
    "erc20": {
        "node": "https://mainnet.infura.io/v3/353492101df944c5a9328be0e999999",
        "contract": {
            "address": "0x0000000000085d4780B73119b644AE5ecd22b376",
            "decimals": 18
        },
        "fee": 0.4,
        "gateway_fee": 0.2,
        "network_fee": 0.2,
        "gatewayAddress": "0xC05182ecd39C34b00B6Dae8F8ea53AEE33123456",
        "privateKey": "0x12346578913654987srg132654987sfdg654sg654sfg654sdfg645",
        "seedenvname" : "",
        "timeInBetweenChecks": 10,
        "confirmations": 5
    },
    "tn": {
        "gatewayAddress": "3Jejtjd55onPw1Zous7WxFdxMCTw1wRvymL",
        "gatewaySeed": "sneaky sneaky",
        "seedenvname" : "",
        "fee": 0.4,
        "gateway_fee": 0.2,
        "network_fee": 0.2,
        "assetId": "C2684nYZQtWufWMn7f8ogAmwZ1fZZ5vUQC28PdHuZLMp",
        "decimals": 2,
        "network": "turtlenetwork",
        "node": "https://privatenode2.blackturtle.eu",
        "timeInBetweenChecks": 10,
        "confirmations": 5
    }
}
```

## Running the gateway
After starting the gateway, it will provide a webpage on the port set in config.json.

## Usage of the gateway
This is a simple gateway for TN tokens to the Waves Platform and vice versa. For sending tokens from the Waves Platform to the TN blockchain, just add the TN address that should receive the tokens as the description of the transfer and send the tokens to the Waves address of the gateway.

For sending tokens from the TN Platform to the Waves blockchain, just add the Waves address that should receive the tokens as the description of the transfer and send the tokens to the TN address of the gateway.

## Management interface
After starting the gateway, there are also a couple of management interfaces which are secured by the admin-username and admin-password fields in the config.json:
```
    /errors: This will show an overview of detected errors during processing of blocks or transferring funds
```

# Disclaimer
USE THIS FRAMEWORK AT YOUR OWN RISK!!! FULL RESPONSIBILITY FOR THE SECURITY AND RELIABILITY OF THE FUNDS TRANSFERRED IS WITH THE OWNER OF THE GATEWAY!!!
