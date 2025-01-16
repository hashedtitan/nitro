## Fairblock Fork of Nitro

This is a fork of the [Arbitrum Nitro repo](https://github.com/Layr-Labs/nitro). It is purely for educational purposes. This repo is currently being used with the Fairblock `orbit-setup-script` repo to showcase the deployment of an EVM chain with precompiles in an Orbit Chain. The methods used to incorporate the Fairblock precompiles into this EVM are the same to be used for any other EVM. Simply modify the `contracts.go` with the Fairblock precompiles and ensure that other dependencies are installed.

When setting up this repo following the Fairblock `orbit-setup-script` repo quickstart, make sure you go through the following steps. These steps are outlined in the Fairblock `orbit-setup-script` repo quickstart, but are also placed here for convenience.

1. Run the docker container for the modified nitro node so it running persistently on your local machine.

## Dependencies

At the root, run the following command to install the dependencies.

```shell
git submodule sync
git submodule update --init --recursive --force
```

Find a folder called `quickstart`. Within this folder, you will find a version of `contracts.go` that has the FairBlock pre-compiles already added in.

Move the `contracts.go` to the path `go-ethereum/core/vm`, replacing the `contracts.go` file already there.

With that in place, run the following command to regenerate your `nitro-node` docker image locally:

```bash
make docker
```

<!-- TODO: troubleshoot this setup, because I think there is a part in the nitros repo setup where the nodeConfig.json is needed -->

Next, you are going to run do the following:

- Create a nitro node local docker container running in the background until it is closed.
- Expose it via port 8449
- Tag the docker container under the name `nitro-node-dev`

To do this, run the following command:

```bash
docker run --rm -it -v $(pwd)/config:/home/user/.arbitrum -p 8449:8449 nitro-node-dev --conf.file /home/user/.arbitrum/nodeConfig.json
```

Now you have your nitro node running locally. You can now setup your Orbit chain and run tests with a sealed bid auction example on said chain. Jump back to the Fairblock `orbit-setup-script` repo quickstart.

If you'd like to read up on the Arbitrum Nitro original repo, check out the toggle below.

<details>
<summary>Arbitrum Nitro Original README</summary>

## About Arbitrum Nitro

<img src="https://arbitrum.io/assets/arbitrum/logo_color.png" alt="Logo" width="80" height="80">

Nitro is the latest iteration of the Arbitrum technology. It is a fully integrated, complete
layer 2 optimistic rollup system, including fraud proofs, the sequencer, the token bridges,
advanced calldata compression, and more.

See the live docs-site [here](https://developer.arbitrum.io/) (or [here](https://github.com/OffchainLabs/arbitrum-docs) for markdown docs source.)

See [here](https://docs.arbitrum.io/audit-reports) for security audit reports.

The Nitro stack is built on several innovations. At its core is a new prover, which can do Arbitrum’s classic
interactive fraud proofs over WASM code. That means the L2 Arbitrum engine can be written and compiled using
standard languages and tools, replacing the custom-designed language and compiler used in previous Arbitrum
versions. In normal execution,
validators and nodes run the Nitro engine compiled to native code, switching to WASM if a fraud proof is needed.
We compile the core of Geth, the EVM engine that practically defines the Ethereum standard, right into Arbitrum.
So the previous custom-built EVM emulator is replaced by Geth, the most popular and well-supported Ethereum client.

The last piece of the stack is a slimmed-down version of our ArbOS component, rewritten in Go, which provides the
rest of what’s needed to run an L2 chain: things like cross-chain communication, and a new and improved batching
and compression system to minimize L1 costs.

Essentially, Nitro runs Geth at layer 2 on top of Ethereum, and can prove fraud over the core engine of Geth
compiled to WASM.

Arbitrum One successfully migrated from the Classic Arbitrum stack onto Nitro on 8/31/22. (See [state migration](https://developer.arbitrum.io/migration/state-migration) and [dapp migration](https://developer.arbitrum.io/migration/dapp_migration) for more info).

## License

Nitro is currently licensed under a [Business Source License](./LICENSE.md), similar to our friends at Uniswap and Aave, with an "Additional Use Grant" to ensure that everyone can have full comfort using and running nodes on all public Arbitrum chains.

The Additional Use Grant also permits the deployment of the Nitro software, in a permissionless fashion and without cost, as a new blockchain provided that the chain settles to either Arbitrum One or Arbitrum Nova.

For those that prefer to deploy the Nitro software either directly on Ethereum (i.e. an L2) or have it settle to another Layer-2 on top of Ethereum, the [Arbitrum Expansion Program (the "AEP")](https://docs.arbitrum.foundation/assets/files/Arbitrum%20Expansion%20Program%20Jan182024-4f08b0c2cb476a55dc153380fa3e64b0.pdf) was recently established. The AEP allows for the permissionless deployment in the aforementioned fashion provided that 10% of net revenue (as more fully described in the AEP) is contributed back to the Arbitrum community in accordance with the requirements of the AEP.

## Contact

Discord - [Arbitrum](https://discord.com/invite/5KE54JwyTs)

Twitter: [Arbitrum](https://twitter.com/arbitrum)


</details>



