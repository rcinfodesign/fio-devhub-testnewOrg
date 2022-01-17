---
title: Using delegated permissions
description: Using delegated permissions
---

# Using delegated permissions

## Overview

Delegated permissions may be needed if a wallet or exchange wants to enable users to register FIO Crypto Handles on their domain, but does not want to make their domain public and does not want to share the private key that owns the domain. In these cases a new, secondary, account may be given permissions to register FIO Crypto Handles on the private domain. 

For example, delegated account permissions may be needed when using the FIO Registration Site. In these cases a wallet may register a FIO Domain and want to keep it as private. But, the wallet wants to enable users to register Free FIO Crypto Handles on their domain using the FIO Registration Site. In these cases a second permission is created that can be used by the Registration Site without compromising the privacy of the original public/private key pair.

## Example of a delegated permissions

The following is an example of a delegated permission. In this case the `fo44zffcsyme` account owns the **domainwithpermissions** FIO Domain. This domain is private, but the wallet that owns **domainwithpermissions** wants to enable their users to get free FIO Crypto Handles on the FIO Registration site. So, a second account `y2khj2vtcfhq` is given active permissions on the account. In this case you may have permssions that look like the following:

![Image]({{ site.baseurl }}/assets/img/permissions.png)

In this example, even though `fo44zffcsyme` account owns the **domainwithpermissions** domain,  `y2khj2vtcfhq` can now call regaddress with `fo44zffcsyme` permissions. 

```javascript
const { Fio } = require('@fioprotocol/fiojs');
const { TextEncoder, TextDecoder } = require('text-encoding');
const fetch = require('node-fetch');

const httpEndpoint = 'https://fiotestnet.blockpane.com'

const privateKey = 'privatekey'   // Private key for 4t2x5ac21rbg account

const fiojsRegaddress = async () => {
  info = await (await fetch(httpEndpoint + '/v1/chain/get_info')).json();
  blockInfo = await (await fetch(httpEndpoint + '/v1/chain/get_block', {body: `{"block_num_or_id": ${info.last_irreversible_block_num}}`, method: 'POST'})).json()
  chainId = info.chain_id;
  currentDate = new Date();
  timePlusTen = currentDate.getTime() + 10000;
  timeInISOString = (new Date(timePlusTen)).toISOString();
  expiration = timeInISOString.substr(0, timeInISOString.length - 1);
  
  transaction = {
    expiration,
    ref_block_num: blockInfo.block_num & 0xffff,
    ref_block_prefix: blockInfo.ref_block_prefix,
    actions: [{
      account: 'fio.address',
      name: 'regaddress',
      authorization: [{
        actor: 'fo44zffcsyme',
        permission: 'active',
      }],
      data: {
        fio_address: 'test@domainwithpermissions',
        owner_fio_public_key: 'FIO-Public-Key-of-new-crypto-handle-owner',
        max_fee: 100000000000,
        tpid: '',
        actor: 'y2khj2vtcfhq'
      },
    }]
  };

  abiMap = new Map()
  tokenRawAbi = await (await fetch(httpEndpoint + '/v1/chain/get_raw_abi', {body: `{"account_name": "fio.address"}`, method: 'POST'})).json()
  abiMap.set('fio.address', tokenRawAbi)
 
  var privateKeys = [privateKey];
  
  const tx = await Fio.prepareTransaction({
    transaction,
    chainId,
    privateKeys,
    abiMap,
    textDecoder: new TextDecoder(),
    textEncoder: new TextEncoder()
  });

  pushResult = await fetch(httpEndpoint + '/v1/chain/register_fio_address', {
      body: JSON.stringify(tx),
      method: 'POST',
  });
  
  json = await pushResult.json();

  if (json.type) {
    console.log('Error: ', json.fields[0].error);
  } else {
    console.log('Success. Transaction ID: ', json.transaction_id)
  }
   
};

fiojsRegaddress();
```