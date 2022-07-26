# SNARK verifiers

## Trusted setup:

- 'test' circuits: https://gateway.pinata.cloud/ipfs/Qmbi3nqjBwANPMk5BRyKjCJ4QSHK6WNp7v9NLLo4uwrG1f
- 'medium' circuits: https://gateway.pinata.cloud/ipfs/QmRzp3vkFPNHPpXiu7iKpPqVnZB97wq7gyih2mp6pa5bmD
- 'x32' circuits: https://gateway.pinata.cloud/ipfs/QmWSxPBNYDtsK23KwYdMtcDaJg3gWS3LBsqMnENrVG6nmc
- 'batch64' circuits: https://gateway.pinata.cloud/ipfs/QmbVzVWqNTjEv5S3Vvyq7NkLVkpqWuA9DGMRibZYJXKJqy


## Generating circuits
Instead of downloading the above circuits from the ipfs, they can be generated using the MACI scripts.  For example, to build the x32 circuits on linux Ubuntu 22.04 + Node v16.13.2:

```
# Clone the MACI repo and switch to version v0.10.1:
git clone https://github.com/privacy-scaling-explorations/maci.git
cd maci/
git checkout v0.10.1

# install deps
sudo apt-get install build-essential libgmp-dev libsodium-dev nasm git

# recompile binaries (takes time: ~5min to ~10min), the output files are in ./params folder
cd circuits
./scripts/buildSnarks32.sh

```


### Generating batch64 circuits
The batch64 circuits can be generated using the [buildCustomSnarks.sh](https://github.com/privacy-scaling-explorations/maci/blob/master/circuits/scripts/buildCustomSnarks.sh) as follow:

```
./scripts/buildCustomSnarks.sh -s 32 -m 32 -v 3 -i 6 -b 64
```

After generating the files, set the c binaries with executable permission and rename files as follow so they can be used with the tally scripts as described [here](../../../docs/tally-verify.md)

```
mv batchUstCustom batchUst32
mv batchUstCustom.r1cs batchUst32.r1cs
mv batchUstCustom.params batchUst32.params
mv batchUstCustom.dat batchUst32.dat
mv batchUstCustom.sym batchUst32.sym
mv qvtCustom qvt32
mv qvtCircuitCustom.r1cs qvtCircuit32.r1cs
mv qvtCustom.params qvt32.params
mv qvtCustom.dat qvt32.dat
mv qvtCustom.sym qvt32.sym
chmod u+x batchUst32 qvt32
```
