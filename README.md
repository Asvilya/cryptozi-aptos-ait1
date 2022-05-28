Hey all, congratulation on getting selected as validator node for AIT1! Please follow the instructions here (https://aptos.dev/tutorials/validator-node/connect-to-testnet/) to setup your node and connect to testnet, you have 24 hours to finish this operation to be eligible for token rewards.
- The docker image tag to use is `testnet_317f80bb`
- Sha256 for the docker image is `5184f637f15a9c071475c5bfb3050777c04aa410e9d43c7ff5e7c4a99a55a252`
- Sha 256 for genesis blob is `2dae3f54512d5be1a9697c26c2676b8f878a8023c2b6b453154df11598a548a6`
- Waypoint is `0:fe8425ffc2351c5ef6995d3e595e21d0634a4d41c1bda4fc86ba6b121baad95d`
- Aptos node peer ID is `d9b628e9` if you want to check your connection.

Let us know if you have any questions, and looking forward to see your node coming online!

How to Update?
Update guide for docker guys:

Stop Node:
- docker-compose down

- cd /root/.aptos
- docker-compose down --volumes
- vi docker-compose.yaml

find 2 row and replace with new tag:
- image: "${VALIDATOR_IMAGE_REPO:-aptoslab/validator}:${IMAGE_TAG:-testnet_317f80bb}"
:wq!

- rm -rf genesis.blob
- rm -rf waypoint.txt

# download new file
- wget https://raw.githubusercontent.com/aptos-labs/aptos-ait1/main/genesis.blob
- wget https://github.com/aptos-labs/aptos-ait1/blob/main/waypoint.txt

Sart Node
- docker compose up -d

Test command:
- curl 127.0.0.1:9101/metrics 2> /dev/null | grep "aptos_connections{.*\"Validator\".*}"
- curl 127.0.0.1:9101/metrics 2> /dev/null | grep "aptos_network_peer_connected{.*remote_peer_id=\"d9b628e9\".*}"
- curl 127.0.0.1:9101/metrics 2> /dev/null | grep "aptos_consensus_current_round"
- curl 127.0.0.1:9101/metrics 2> /dev/null | grep "aptos_connections"
- sha256sum genesis.blob 


