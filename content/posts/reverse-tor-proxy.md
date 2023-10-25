+++
title = "Anonymising crypto transactions wih Tor and Rust"
date = "2023-05-12"
description = "A guide to setting up a Tor proxy for all your RPC requests"

[taxonomies]
tags = ["privacy", "rust", "crypto", "tor"]

+++

In light of all the recent privacy disclosures from major RPC providers like Infura and Alchemy, I decided to build a simple Tor proxy that routes RPC requests through the Tor network.

## Umm but why?

Well, it's kind of annoying that Consensys *actually* records all your IPs. They claim its for analytical purposes but its upto them how they really use it. Also they're only a subpeonea away from giving up their crypto address-to-IP mappings to the authorities.

That and the fact that Metamask doesn't allow one to change their primary RPC url was the last straw to ditch its shitty UI and jump on the Frame train. (Beautiful UI/UX btw)

The fact that we just need to *trust* these providers to keep our identity safe is well, not crypto-esque. Verfiy don't trust right? I think we can do better.

## Anon My RPC

Anon My RPC consists of a Tor client to connect through Tor and Rust's Axum library to act as a proxy server.

Usually, one has to run a Tor node separately and then have the proxy server connect to it via a SOCK5 port. I found this exciting Tor client library `Arti` that allows one to bootsrrap a Tor connection via a *function call* in code!


Now I can package and run both these components from a single binary. Neat stuff.

## Demo time

I already have the code hosted on shuttle.

All you need to do is prefix your RPC url with `anonmyrpc.xyz` and boom, you'll be fending off snooping RPC providers.
// Insert GIF here

Here's the [proof-of-code](https://github.com/LeverCapital/anon-my-rpc) for the proxy server. You can also run it locally if you don't trust the hosted endpoint.

Privacy should be convenient.

## Up next

- Add support for more RPC providers.
- Refresh the Tor circuit after a certain number of requests.
- Integrate with [Helios](https://github.com/a16z/helios) to provide provably correct and private RPC calls!

It was a fun little concept and I've made this my daily driver. I hope you find it useful too!
