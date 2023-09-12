+++
title = "Anonymising crypto transactions wih Tor and Rust"
date = "2023-05-12"
description = "A guide to setting up a Tor proxy for all your RPC requests"

[taxonomies]
tags = ["privacy", "rust", "crypto", "tor"]

+++

In light of all the recent privacy disclosure from major RPC providers like Infura and Alchemy, I decided to build a simple Tor proxy that routes RPC requests through the Tor network.

## Umm but why?

Well, it's kind of annoying that Consensys *actually* records all your IPs. They claim its for analytics purposes but its upto them how they use it analytically. They're only a subpeonead away from giving up their mappings from crypto address to IP. 

That and the fact that metamsk doesn't allow you to change your primary RPC url was the last straw to ditch its shitty UI and jump on the Frame train. (Beautiful UI/UX)

I was surpised like most ppl but should we really be? I mean you can't verify their claim, you can only trust it. 

## Show me the money

The code consists of a Tor client to connect through Tor and the Axum library to act as a proxy. 

Usually, one has to run a Tor node separately and then connect to it via a SOCK5 proxy. I came upon this exciting Tor client library `Arti` written in Rust, that allows me to setup a Tor connection via a *function call* in code!
Now I package and run both these components from a single binary. Neat stuff. 

## Demo time

I already have the code hosted on shuttle. 

Just prefix your RPC url with `anonmyrpc.xyz` and boom, you'll be fending off snooping RPC providers.

Privacy should be convenient.

## Up next

Couple of things left to focus on

- Switch up the circuit every T period
- How do we run a different circuit for each transaction and make it faster?
- Proof-of-code so that people trust the endpoint

It was a fun little concept and I've made this my daily driver. I'm going to add some tests for security to make sure it's all good.
