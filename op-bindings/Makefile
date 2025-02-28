SHELL := /bin/bash

pkg := bindings

all: version mkdir bindings more

bindings: l1block-bindings \
	l1-cross-domain-messenger-bindings \
  	l1-standard-bridge-bindings \
	l2-to-l1-message-passer-bindings \
	optimism-portal-bindings \
	l2-output-oracle-bindings \
	gas-price-oracle-bindings \
	address-manager-bindings \
	l2-cross-domain-messenger-bindings \
	l2-standard-bridge-bindings \
	sequencer-fee-vault-bindings \
	optimism-mintable-erc20-factory-bindings \
	optimism-mintable-erc20-bindings \
	proxy-bindings \
	proxy-admin-bindings \
	erc20-bindings \
	weth9-bindings \
	deployer-whitelist-bindings

version:
	forge --version

compile:
	cd ../packages/contracts-bedrock/ && \
		yarn clean && \
		npx hardhat compile

l1-cross-domain-messenger-bindings: compile
	./gen_bindings.sh contracts/L1/L1CrossDomainMessenger.sol:L1CrossDomainMessenger $(pkg)

l1-standard-bridge-bindings: compile
	./gen_bindings.sh contracts/L1/L1StandardBridge.sol:L1StandardBridge $(pkg)

optimism-portal-bindings: compile
	./gen_bindings.sh contracts/L1/OptimismPortal.sol:OptimismPortal $(pkg)

l2-output-oracle-bindings: compile
	./gen_bindings.sh contracts/L1/L2OutputOracle.sol:L2OutputOracle $(pkg)

address-manager-bindings: compile
	./gen_bindings.sh contracts/legacy/AddressManager.sol:AddressManager $(pkg)

l1block-bindings: compile
	./gen_bindings.sh contracts/L2/L1Block.sol:L1Block $(pkg)

l2-to-l1-message-passer-bindings: compile
	./gen_bindings.sh contracts/L2/L2ToL1MessagePasser.sol:L2ToL1MessagePasser $(pkg)

gas-price-oracle-bindings: compile
	./gen_bindings.sh contracts/L2/GasPriceOracle.sol:GasPriceOracle $(pkg)

l2-cross-domain-messenger-bindings: compile
	./gen_bindings.sh contracts/L2/L2CrossDomainMessenger.sol:L2CrossDomainMessenger $(pkg)

l2-standard-bridge-bindings: compile
	./gen_bindings.sh contracts/L2/L2StandardBridge.sol:L2StandardBridge $(pkg)

sequencer-fee-vault-bindings: compile
	./gen_bindings.sh contracts/L2/SequencerFeeVault.sol:SequencerFeeVault $(pkg)

optimism-mintable-erc20-factory-bindings: compile
	./gen_bindings.sh contracts/universal/OptimismMintableERC20Factory.sol:OptimismMintableERC20Factory $(pkg)

optimism-mintable-erc20-bindings: compile
	./gen_bindings.sh contracts/universal/OptimismMintableERC20.sol:OptimismMintableERC20 $(pkg)

proxy-bindings: compile
	./gen_bindings.sh contracts/universal/Proxy.sol:Proxy $(pkg)

proxy-admin-bindings: compile
	./gen_bindings.sh contracts/universal/ProxyAdmin.sol:ProxyAdmin $(pkg)

erc20-bindings: compile
	./gen_bindings.sh node_modules/@openzeppelin/contracts/token/ERC20/ERC20.sol:ERC20 $(pkg)

weth9-bindings: compile
	./gen_bindings.sh contracts/vendor/WETH9.sol:WETH9 $(pkg)

deployer-whitelist-bindings: compile
	./gen_bindings.sh contracts/legacy/DeployerWhitelist.sol:DeployerWhitelist $(pkg)

l1-blocknumber-bindings: compile
	./gen_bindings.sh contracts/legacy/L1BlockNumber.sol:L1BlockNumber $(pkg)

more:
	go run ./gen/main.go \
		-artifacts ../packages/contracts-bedrock/artifacts \
		-out ./bindings \
		-contracts OptimismMintableERC20Factory,L2StandardBridge,L1BlockNumber,DeployerWhitelist,Proxy,OptimismPortal,L2ToL1MessagePasser,L2CrossDomainMessenger,GasPriceOracle,SequencerFeeVault,L1Block,LegacyERC20ETH,WETH9,GovernanceToken,L1CrossDomainMessenger \
		-package bindings

mkdir:
	mkdir -p bin $(pkg)

clean:
	rm -rf bin $(pkg)

test:
	go test ./...
