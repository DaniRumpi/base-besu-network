# base-besu-network

El repo está configurado para lanzar los comandosde generacion de claves, moverlas donde toca y generar una red de 4 nodos (1 bootnode y 3 validadores). No está dockerizado.

## Prerequisitos

- [Hyperledger Besu](https://besu.hyperledger.org/en/stable/private-networks/get-started/install/binary-distribution/)
- [Curl](https://curl.haxx.se/download.html)

Para instalar Besu en tu máquina sigue [este tutorial](https://besu.hyperledger.org/en/stable/private-networks/get-started/install/binary-distribution/#install-or-upgrade-using-homebrew)

## Generación de las claves de los nodos.

Ejecutar el siguiente comando:

```bash
besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key
```

Una vez generadas las claves vamos a copiar la key y la key.pub dentro de cada uno de los Nodos en la ruta NodeN/data.

ahora hay que levantar los nodos. Para ello vamos tirar el siguiente comando:

### Node1

```
besu --data-path=data --genesis-file=../genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all"
```

### Node2 y siguientes

Modificar Node1 por el enode del Node1 y cambiar el puerto por 30304, 30305 y 30306

```
besu --data-path=data --genesis-file=../genesis.json --bootnodes=<Node-1 Enode URL> --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546
```
