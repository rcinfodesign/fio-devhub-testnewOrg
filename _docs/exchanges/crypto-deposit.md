---
layout: page-int
title: Deposit Crypto using FIO Crypto Handles
description: Deposit Crypto using FIO Crypto Handles
redirect_from:
    - /docs/exchanges/exchange-token-deposit
---

# Deposit Crypto using FIO Crypto Handles & FIO Requests

[FIO Crypto Handles]({{site.baseurl}}/docs/fio-protocol/fio-address) (aka FIO Addresses) are human-readable wallet identifiers (such as john@edge or alice@gold) which eliminate the need to see, or even know of, blockchain public addresses. Enabling deposits using [FIO Crypto Handles]({{site.baseurl}}/docs/fio-protocol/fio-address) give exchange users friendly interwallet operability, making deposits easy and near error-free, dramatically reducing support tickets.

As a first step, **Exchanges should register a custom [FIO Domain]({{site.baseurl}}/docs/fio-protocol/fio-address#fio-domains) (e.g., @myexchange)**. Exchange users will then be able to register FIO Crypto Handles on that custom domain (e.g., alice@myexchange).

---
## Using a unique FIO Crypto Handle for each user

To accept crypto deposits using FIO Crypto Handles, an exchange may [register a unique FIO Crypto Handle for each user]({{site.baseurl}}/docs/how-to/registration) of the exchange, and display it in their deposit area, e.g. alice@myexchange.

To deposit tokens of any supported cryptocurrency to their account the user would simply send tokens from a FIO-enabled wallet to their FIO Crypto Handle (e.g. alice@myexchange) and would not have to deal with Public Keys, memo fields, or even having to log into the exchange.

Each [FIO Crypto Handle may be mapped]({{site.baseurl}}/docs/how-to/mapping) using the [`addaddress`]({{site.baseurl}}/pages/api/fio-api/#options-addaddress) action to either the same crypto public address for all users, or a unique crypto public address for each user.

---
## Using the same FIO Crypto Handle for all users

An exchange may [register a single deposit FIO Crypto Handle]({{site.baseurl}}/docs/how-to/registration) for all users of the exchange, and display it their deposit area (e.g. deposits@myexchange).

To deposit any supported token to their account the user would simply send tokens from a FIO-enabled wallet to the Deposit FIO Crypto Handle, e.g. deposits@myexchange. To properly identify the inbound transaction, the user would have to either include a [FIO Data memo]({{site.baseurl}}/docs/how-to/fio-data) which includes their exchange account, or provide the exchange, ahead of time, with a list of FIO Crypto Handles which the user owns.

The Deposit FIO Crypto Handle would be mapped using [`addaddress`]({{site.baseurl}}/pages/api/fio-api/#options-addaddress) to a single FIO Public Key.

The inbound transaction can be identified by reading the OBT Data using [/get_obt_data]({{site.baseurl}}/pages/api/fio-api/#post-/get_obt_data). The data is [encrypted]({{site.baseurl}}/docs/how-to/encryption). Once decrypted, the memo or FIO Crypto Handle of Payee can be used to uniquely identify the user, and the obt_id will contain native chain transaction ID of the corresponding deposit.

#### Transaction memo for FIO token transfer

The [`trnsfiopubky`]({{site.baseurl}}/pages/api/fio-api/#options-trnsfiopubky) action does not accept a memo field. To [attach a FIO Data memo]({{site.baseurl}}/docs/how-to/fio-data) to a FIO token transfer, a [`recordobt`]({{site.baseurl}}/pages/api/fio-api/#options-recordobt) transaction should be sent after the tokens are transferred and include the token transfer transaction id. [`recordobt`]({{site.baseurl}}/pages/api/fio-api/#options-recordobt) requires that both payer and payee have a FIO Crypto Handle. **If either party does not have a FIO Crypto Handle then transfer of memo is not supported**.

---
## Using a FIO Request

If users of the exchange were assigned unique [FIO Crypto Handles]({{site.baseurl}}/docs/fio-protocol/fio-address#fio-addresses), they could send a [FIO Request]({{site.baseurl}}/docs/how-to/fio-request) from the exchange to a FIO Crypto Handle of a FIO-integrated wallet or exchange. (e.g., `alice@mywallet`). The user would then login to the wallet and approve the FIO Request. Once approved, the wallet would execute the transfer on the native chain.
