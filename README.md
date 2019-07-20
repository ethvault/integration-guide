# Ethvault Integration Guide

Integrating with Ethvault is simple and takes 1-2 hours to complete, depending on the depth of integration that you want to add to your DAPP.

## Step 1: Create an issue in this repository. (1 minute)

Create an issue in this repository to track the integration. This will be where you can easily request changes to Ethvault to support your integration. It will be referenced when updating https://ethvault.xyz to include your site.

## Step 2: Add the Web3 provider to your DAPP (10 - 30 minutes)

You have two options-you can either drop in the [polyfill provider](https://github.com/ethvault/iframe-provider-polyfill) (e.g. https://github.com/kendricktan/heiswap-dapp/pull/13) and your site will support all iframe web3 providers (via `window.web3` and `window.ethereum`), or use the [iframe-provider](https://github.com/ethvault/iframe-provider) directly from your code.

## Step 3: Update your `Content-Security-Policy` and `X-Frame-Options` headers. (10 - 30 minutes)

In order to be embed your DAPP in an iframe hosted at https://ethvault.xyz, your web servers need to send the correct HTTP headers. `X-Frame-Options` is superceded by `Content-Security-Policy`, but you should set both headers for the best security.

### `Content-Security-Policy`

You must send the directive `frame-ancestors` in this header with the value of `https://ethvault.xyz` (recommended) or `'*'`. This tells the user agent that your site may be embedded in an iframe as long as all the parent windows have the specified origin. A wildcard indicates your site may be embedded in any iframe.

See [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) for more information.

### `X-Frame-Options`

You must send the value `allow-from https://ethvault.xyz` or omit this header entirely to allow it to be embedded in an iframe.

See [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) for more information.

## Step 4: Test the app. (10 - 30 minutes)

Visit `https://ethvault.xyz/browse#https://my-site-url.com` to try your site out. You should be able to sign in and interact with the website using your Ethvault wallet.

## Step 5: Close the ticket. (1 minute)

Once you have completed integration, close your ticket to let Ethvault know to update the homepage with your site.
