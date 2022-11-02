# Launch Blockchain using ignite command


Using environment varialbe you setup chain name ( and later chain ID).
```
export proj=iochain
export chainid=327
```

Following commands need to be execute on Coordinator/Master Node

```
gh repo create mytestlab123/${proj} --public --description 'IO Chain'
time ignite s chain github.com/mytestlab123/$proj
cd $proj
git add -A
git commit -am "init"
git remote add origin https://github.com/mytestlab123/$proj.git
git remote -v
git push -u origin master
time ignite n chain publish github.com/mytestlab123/${proj} --chain-id $proj 
```

On Validator node, run following commands ( Here we have 3 different validators )
```
ignite n chain init ${chainid}
ignite n chain join ${chainid} --amount 95000000stake
```

On Coordinator node:
```
ignite n request list ${chainid}

ignite n request approve ${chainid} 3-4
ignite n request approve ${chainid} 5-6
ignite n request approve ${chainid} 6-7

ignite n request list ${chainid}
```

Once all validators are approve then *Launch the chain* on Coordinator node:
```
ignite n chain launch $chainid

# Check info details of the chain
ignite n chain show info $chainid

# Check the chain genesis file
ignite n chain show genesis $chainid

# Check all vesting and genesis accounts of the chain
ignite n chain show accounts $chainid

# Check all validators of the chain
ignite n chain show validators $chainid

# Check peers list of the chain
ignite n chain show peers $chainid
```


Once the chain is launched on Coordinator node then run following commands to join the blockchain network:
```
ignite n chain prepare $chainid
${proj}d start --home ${HOME}/spn/$chainid
```

Details for Blockchain ID 327

![Details for Blockchain ID 327](https://user-images.githubusercontent.com/1894622/199388435-b324406d-751c-4aab-ab0a-a61c2c1b2139.png)

