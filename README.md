# Ethvault Integration Guide

## Step 0: What is Ethvault?

Ethvault is a browser based Ethereum wallet and dApp browser.

Integration means making your dApp compatible with the Ethvault dApp browser. Unlike other dApp browsers that inject `web3` and `ethereum` directly into the `window`, Ethvault embeds your dApp in an iframe and cannot set variables on the `window` object. Ethvault offers many advantages for your users, allowing them to sign in and access your dApp using their Ethereum accounts from any device.

Integrating with Ethvault is simple and is estimated to take anywhere from 1 minute to 2 hours to complete, depending on the depth of integration that you want to add to your dApp.

## Step 1 (Optional): Create an issue in this repository (1 minute)

Create an issue in this repository to track the integration. This will be where you can easily request changes to Ethvault to support your integration. It will be referenced when updating https://ethvault.xyz to include your site.

## Step 2: Add the Web3 provider to your dApp (10 - 30 minutes)

You have two options for accessing the Ethvault wallet from your dApp

- Add the [iframe-polyfill-provider](https://github.com/ethvault/iframe-provider-polyfill) (e.g. [ensdomains/ens-app/pull/405](https://github.com/ensdomains/ens-app/pull/405), [kendricktan/heiswap-dapp/pull/13](https://github.com/kendricktan/heiswap-dapp/pull/13)) and your site will support all iframe based dApp browsers (via `window.web3` and `window.ethereum`)

- Detect the iframe context and add an option to use the [iframe-provider](https://github.com/ethvault/iframe-provider) directly from your code

## Step 3: Update your `Content-Security-Policy` and `X-Frame-Options` headers (10 - 30 minutes)

In order to be embed your dApp in any iframe, your web servers need to send the correct HTTP headers. `X-Frame-Options` is superceded by `Content-Security-Policy`, but you should set both headers for compatibility with older browsers.

### Update `Content-Security-Policy`

You must send the directive `frame-ancestors` in this header with the value of `https://ethvault.xyz` (recommended) or the wildcard `'*'`. This allows the user agent to embed your dApp in an iframe as long as all the parent windows have the specified origin. A wildcard for this directive indicates your site may be embedded in any iframe.

See [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) for more information.

### (Optional) Update `X-Frame-Options`

You must send the value `allow-from https://ethvault.xyz` or omit this header to allow it to be embedded in an iframe. Many browsers including Chrome do not support `allow-from` for this header and will notify you of the invalid headers in the console. Thus setting this header is optional.

See [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) for more information.

## Step 4: Test the app (10 - 30 minutes)

Visit `https://ethvault.xyz/browse#https://my-site-url.com` to try your site out. You should be able to sign in and interact with the website using your Ethvault wallet. Note that `https://ethvault.xyz` only allows embedding sites with the https protocol. Check the console to see logs of the communication between the dApp and Ethvault. Everything should just work so this step is optional.

## Step 5: Close the ticket (1 minute)

If you created a ticket, close your ticket to let Ethvault know to update the homepage with your integration. Otherwise [ping Ethvault](mailto:moody@ethvault.xyz).

## FAQ

### Is it safe to allow iframe embedding for my dApp?

Because most dApps are stateless interfaces for interacting with Ethereum contracts, i.e. do not use cookies or store user credentials, allowing iframe embedding does not incur the usual [clickjacking](https://en.wikipedia.org/wiki/Clickjacking) risk.

### How should I announce the integration?

Ethvault is in early alpha, but will launch offering Ether and a free ENS subdomain to each sign up in August 2019. Please [ping Ethvault](mailto:moody.salem@gmail.com) to coordinate an announcement.
