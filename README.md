# Hackathon-Resources
Hackathon resources to get started with the Wyre API as fast as possible.

* Sandbox Environment is [here](https://www.testwyre.com/sign-up).

* Test keys are different from prod keys. Testwyre accounts are different to SendWyre.com

* Bitcoin - testnet3.

* Ethereum - Kovan.

* If you're awaiting account verification, reach out directly via Intercom, or email us (support@sendwyre.com).

* We're currently upgrading from v2 to v3 of our API. **Payment Methods are still on v2.**

* Getting in touch with us
- Intercom chat - On our site.

- Discord chat - https://sendwyre.com/discord

- Email support@sendwyre.com

- Twitter @sendwyre

- Call us - (415)-374-7356.


## Hackathon Example

**Tools From Wyre**

- Widget Onramp - [Metamask-Quickstart](https://beta-docs.sendwyre.com/docs/widget-developer-guide#metamask-on-ramp-quickstart).

Fiat on/off ramp for web3 enabled users.

- Widget Onramp - [Non-web3 users](https://beta-docs.sendwyre.com/docs/widget-developer-guide#metamask-on-ramp-quickstart).

Fiat on/off ramp for both web3 and non-web3 enabled users. Can be used in incognito browsers, all mobile browsers, and still compatible for the web3 browsers wallets. Without additional software installation, helping our partners create sustainable businesses, and reach 

In this example, we're going to do the following.

- Create an account and compliantly verify a US customer to the standard of an MSB.
- Connect their bank account to their Wyre account.
- Debit their bank $100 US Dollars and pay it into their non-custodial wallet.
- Convert funds between various currencies.



## 🔐 Getting Keys & Where To Find Us 🔐

* Sandbox Environment is [here](https://www.testwyre.com/sign-up).

1) Create your account.

2) Verification happens relatively quickly, if you're experiencing delays, just ping us:

3) Login to your account [here](https://www.testwyre.com/sign-in).

4) Top right corner - Click "Your Account" and select "API Keys".

5) Option to whitelist IP addresses for security purposes etc...

6) Copy your keys and put a description. Don't lose them.

** If you care about your test account, remember activate MFA.

## 🏗 First Authenticated API Request - GET/accounts 🏗

📑 Official Docs - [Authentication](https://beta-docs.sendwyre.com/docs/code-examples)

1) Update the example requests with the following.
- Make sure you're on the right version (v3).
- Make sure you've added your API keys that we just created.
- Make sure you're on the test URL. Your requests should be hitting https://api.testwyre.com

2) Grab your Account ID from "Your Account" [here](https://www.testwyre.com/settings/basic-info). Your account ID should look like *AC-XXXXXXXXXXX*.

3) Paste this into the request, and let's run it and see what it returns.
- Your response should look something like the below. You can hold multiple currencies, but it'll only show ones that have a balance. More information on currency pairs available in the documentation.

```
{
  "id": "AC-XZ4XMR2R6GL",
  "status": "APPROVED",
  "type": "INDIVIDUAL",
  "country": "US",
  "createdAt": 1548256854000,
  "depositAddresses": {
    "ETH": "0xfa6f2a0c659316b94be5d93872b3f39ec38b1147", // DAI, ETH, WETH - All goes to this address FYI.
    "BTC": "mwXxZZFGUqLa3gVHpgPKSsespZKPkqaKtX" // BTC only (obviously).
  },
  
  // Transactions that are PENDING are included.
  "totalBalances": {
    "USD": 1000
  },
  
  // Does not include PENDING transactions (e.g. awaiting confirmations, etc...)
  "availableBalances": {
    "USD": 1000
  },
  "profileFields": [
    {
      "fieldId": "individualCellphoneNumber", // fieldId
      "fieldType": "CELLPHONE", // type
      "value": "+1111111111", // value
      "note": null, // Usually a way for Wyre to communicate the reason for the status. E.g. Cell-phone
      "status": "APPROVED"
    },
    {
      "fieldId": "individualEmail",
      "fieldType": "EMAIL",
      "value": "michael+coinlist@sendwyre.com",
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualLegalName",
      "fieldType": "STRING",
      "value": "Coinlist Hackathon",
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualSsn",
      "fieldType": "STRING",
      "value": "REDACTED",
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualDateOfBirth",
      "fieldType": "DATE",
      "value": "1980-02-02",
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualResidenceAddress",
      "fieldType": "ADDRESS",
      "value": {
        "street1": "1550 Bryant St",
        "street2": null,
        "city": "San Francisco",
        "state": "CA",
        "postalCode": "94103",
        "country": "US"
      },
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualGovernmentId",
      "fieldType": "DOCUMENT",
      "value": [
        "DO-TGV97LFMW9E"
      ],
      "note": null,
      "status": "APPROVED"
    },
    {
      "fieldId": "individualSourceOfFunds",
      "fieldType": "PAYMENT_METHOD",
      "value": null,
      "note": null,
      "status": "APPROVED"
    }
  ]
}
```
4) Cool. That's our account. Created, and mine looks like it's verified!

When I created my account, I opted in to receive a [ERC-721](https://kovan.etherscan.io/tx/0x14305db9b7baa3c057300d679125ca08b038a49919634a649d9d7e7f3ffb7252) token to that wallet I control. This token acts similarly to a blue check mark on Twitter. It's a verified account, from a regulated MSB. It aims to minimize compliance overheads for new entrepreneurs, streamline UX, and put the users privacy/sensitivie information as the number one priority.

Our standard account format has verified the required information to meet the standards from Fincen. Wyre is a registered MSB federally, as well as on a state by state level. Compliance is really hard, and resource intensive. Our hope is to share our hard work like a public utility for teams to get to market and iterate faster while avoiding the costs with legal opinions and compliance audits, etc...

More information on our ERC-721 initiative [here](https://blog.sendwyre.com/community-driven-on-chain-compliance-d334e0f5962b).

## 🏦Connect Bank Account - POST/paymentMethods 🏦

📑 Official Docs - [Connect Bank](https://beta-docs.sendwyre.com/docs/create-ach-payment-method).

**Mentioned earlier, but this is v2 API. So change the version if needed, etc...**

Wyre works with Plaid who you're likely familiar with. It's a simplified UX to authenticate your ownership of an account to us, and the account details that we should pay out your USD to if needed.

1) For demonstration, here's the payment method widget on [jsFiddle](https://jsfiddle.net/8dq52ufy/).
Sanxbox Bank login creds:
* Username: *user_good*

* Password: *pass_good*

** Note on `WyrePMWidget` the environment,`env` is set to test. Update that to `prod` if you're using it in production.

```html
<html>
<head>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.3/jquery.min.js"></script>
  <script src="https://cdn.plaid.com/link/v2/stable/link-initialize.js"></script>
  <script src="https://verify.sendwyre.com/js/pm-widget-init.js"></script>
  <script type="text/javascript">
    var handler = new WyrePmWidget({
      env: "test",
      onLoad: function(){
        // In this example we open the modal immediately on load. More typically you might have the handler.open() invocation attached to a button.
        handler.open();
      },
      onSuccess: function(result){
        // Here you would forward the publicToken back to your server in order to  be shipped to the Wyre API
        console.log(result.publicToken);
//      window.alert(result.publicToken); // Obnoxious reminder for my demo
      },
      onExit: function(err){
        if (err != null) {
          // The user encountered an error prior to exiting the module
        }
        console.log("Thingo exited:", err);
      }
    });
    
  </script>
</head>
<body>

</body>
</html>
```

2) We're going to grab the result from this. Right click and inspect element to look at the console, or if you're on the jsFiddle it'll give a window alert from my demo.

```public-sandbox-07f1fa0b-1ba9-49df-8311-1f2b65de1dd2|M5d4eQJwVGI63lEgmp5vc1PxKrvoNDF9AvNNw```

3) Now let's add it to our account.

* POST URL - https://api.testwyre.com/v2/paymentMethods

```json
"publicToken":"public-sandbox-07f1fa0b-1ba9-49df-8311-1f2b65de1dd2|M5d4eQJwVGI63lEgmp5vc1PxKrvoNDF9AvNNw",
"paymentMethodType":"LOCAL_TRANSFER",
"country": "US"
```

4) If successful, it'll return details on it for us. Here's the response I got:
```
{
  "id": "PA-M6YW788BCWN",
  "owner": "account:AC-XZ4XMR2R6GL",
  "createdAt": 1548262133744,
  "name": "Plaid Saving 1111",
  "defaultCurrency": "USD",
  "status": "PENDING",
  "statusMessage": null,
  "waitingPrompts": [],
  "linkType": "LOCAL_TRANSFER",
  "beneficiaryType": "UNKNOWN",
  "supportsDeposit": true,
  "nameOnMethod": null,
  "last4Digits": "1111",
  "brand": null,
  "expirationDisplay": null,
  "countryCode": "US",
  "nickname": null,
  "rejectionMessage": null,
  "disabled": false,
  "supportsPayment": true,
  "chargeableCurrencies": [
    "USD"
  ],
  "depositableCurrencies": [
    "USD"
  ],
  "chargeFeeSchedule": null,
  "depositFeeSchedule": null,
  "minCharge": null,
  "maxCharge": null,
  "minDeposit": null,
  "maxDeposit": null,
  "documents": [],
  "srn": "paymentmethod:PA-M6YW788BCWN"
}
```

* The srn is your bread and butter for the next section, transfers. Be mindful that the status is currently `PENDING`. You'll need it to be showing as `APPROVED` before you can start debiting from it, etc... Easy oversight if new to our API. I know this because it happened to me as I was putting this example together. :fp:

## 🛫 💵 Fiat On/Off Ramps 💵 🛬 - POST/transfers

📑 Official Docs - [Transfers](https://beta-docs.sendwyre.com/docs/create-transfer).

* Transfers are going from one source to a destination. So the term transfers covers sending/receiving, but it also covers buying/selling. Buying ETH with my bank account is technically just a `transfer` from my bank account to my ETH wallet.

Let's make a request to add some funds from our bank account to our non-custodial wallet, converting them on the go so that they show up as ETH in my non-custodial wallet.

All the transfers on our system operate like RFQ's (Request For Quote) do. This means you request the quote for the transfer you want (whether that is exchanging within your Wyre account, or if it's going from fiat to crypto like this example). If you're happy then you confirm.

Most platforms will save the extra back and forth, and set `"autoConfirm" : true` 

1) The response above (when adding connecting our bank account) shows that bank (payment method) as `"srn": "paymentmethod:PA-M6YW788BCWN"`. We'll debit the bank $100 USD and send it to our non-custodial wallet. 

2) Let's put that into our transfer request, and run it.

```{
  "source": "paymentmethod:PA-M6YW788BCWN:ach", // note the :ach on the end of the payment method.
  "dest": "ethereum:AC-XX38VYXUA84",
  "sourceCurrency":"USD",
  "destCurrency":"USD",
  "sourceAmount": "100",
  "amountIncludeFees": true,
  "autoConfirm": true
}
```

There's a number of really helpful paraemeters that you can include in a transfer. customId's, amountIncludeFees, preview (for cleaner end-user experience), etc... You'll notice these in our response below.

3) If you're successful, you should receive a response giving details of the transfer request that was made. Below is the request that I made just above.

```{
  "status": "PENDING",
  "sourceAmount": 100.87,
  "dest": "ethereum:0x72867Ae42Cd662Beaa4d237694061BD1c7a6Ec02",
  "destAmount": 0.862746079387066,
  "destCurrency": "ETH",
  "sourceCurrency": "USD",
  "customId": null,
  "exchangeRate": 0.00862746079387066,
  "fees": {
    "ETH": 0.001,
    "USD": 0.75
  },
  "createdAt": 1548278142000,
  "totalFees": 0.87,
  "completedAt": null,
  "cancelledAt": null,
  "failureReason": null,
  "expiresAt": 1548278442000,
  "updatedAt": null,
  "blockchainTx": null,
  "reversingSubStatus": null,
  "reversalReason": null,
  "pendingSubStatus": "PROCESSING_EXCHANGE",
  "statusHistories": [
    {
      "id": "ZXQ9NTHY99E",
      "transferId": "TF-LJZA3RXC6UA",
      "createdAt": 1548278143000,
      "type": "OUTGOING",
      "statusOrder": 0,
      "statusDetail": "Initiating Transfer",
      "state": "INITIATED",
      "failedState": null
    },
    {
      "id": "9Z9F9MG4BD6",
      "transferId": "TF-LJZA3RXC6UA",
      "createdAt": 1548278144000,
      "type": "OUTGOING",
      "statusOrder": 200,
      "statusDetail": "Processing Exchange",
      "state": "PENDING",
      "failedState": null
    },
    {
      "id": "VGJ2ENUWY3N",
      "transferId": "TF-LJZA3RXC6UA",
      "createdAt": 1548278144000,
      "type": "OUTGOING",
      "statusOrder": 400,
      "statusDetail": "Processing Deposit",
      "state": "PENDING",
      "failedState": null
    }
  ],
  "source": "paymentmethod:PA-M6YW788BCWN:ach",
  "owner": "account:AC-XZ4XMR2R6GL",
  "message": "C0xnlist Hackathon",
  "id": "TF-LJZA3RXC6UA"
}
```
There's various states that a transaction goes through, and you can always use the transferId. Mine is `TF-LJZA3RXC6UA`. Another neat thing for people is our "UPS Tracker" - Watch the transfer or share it with others, etc... Have a look at mine [here](https://www.testwyre.com/track/TF-LJZA3RXC6UA).

Hopefully
