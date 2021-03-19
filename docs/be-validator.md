# How to become a Legends Chain Validaotr

## You must have a server running debian / or ubuntu
You can buy it at Cloud Service Provider

## Follow our tutorial

### Download and run
Legends: 
```
https://github.com/differs/Legends/releases/download/v1.0.1/Legends
```
subkey: diffent from substrate's version, this version can generate keys use for our network

```
https://github.com/differs/Legends/releases/download/v1.0.1/subkey
```

### Generate accounts
You can generate keys like this:
```
./subkey generate -n legends 
Secret phrase `siege six magnet law bubble elegant snack addict crack ranch tiger other` is account:
  Secret seed:      0xe77696ff70d1c889669a79263710c2f6548e193921a8c55125c7bda0e7935f02
  Public key (hex): 0xccd8eada87a5cab84bdaa073bc7a8d524b5d3d90f04452d4890d2466c8974d7b
  Account ID:       0xccd8eada87a5cab84bdaa073bc7a8d524b5d3d90f04452d4890d2466c8974d7b
  SS58 Address:     6GZteZWJvZfGNvPMrRT5rGMZNYShrw4pZGpox92m1syGaSqZ
```
and use the some phrase inspect accounts for grandpa,babe,im_online, authority_discovery

```
./subkey inspect -n legends --scheme sr25519 "siege six magnet law bubble elegant snack addict crack ranch tiger other//babe//go"
Secret Key URI `siege six magnet law bubble elegant snack addict crack ranch tiger other//babe//go` is account:
  Secret seed:      0x393852f12ee5a88f3027be8a08cb678b6d10481bdde14f1ed6bfab6d58503bda
  Public key (hex): 0x34987e56c4549e7bef91b44df02dd92c6d0731479d05ac58fd841c19fbd12433
  Account ID:       0x34987e56c4549e7bef91b44df02dd92c6d0731479d05ac58fd841c19fbd12433
  SS58 Address:     6D8GEQrCArFbQEexsgpKF7Q36y99ierfeVnQBYYdCLf3FLMM
```

```
./subkey inspect -n legends --scheme ed25519 "siege six magnet law bubble elegant snack addict crack ranch tiger other//grandpa//go"
Secret Key URI `siege six magnet law bubble elegant snack addict crack ranch tiger other//grandpa//go` is account:
  Secret seed:      0x84d89fb8e1d4f9070ff3b416e71aa21b571e672e776dbb7bd37593b931df55cc
  Public key (hex): 0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06
  Account ID:       0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06
  SS58 Address:     6DaxmQpdMFvB2T6xa2ntYLJgyFdrE9NnZyt3nXLzxtLW4xNd
```

```./subkey inspect -n legends --scheme ed25519 "siege six magnet law bubble elegant snack addict crack ranch tiger other//im_online//go"
Secret Key URI `siege six magnet law bubble elegant snack addict crack ranch tiger other//im_online//go` is account:
  Secret seed:      0x01f4e93986f08c5acea3047ef0f48b88c5b33d618bc34abd2359acebdaf1619a
  Public key (hex): 0x8556567610cf2d47587c9786bc6ef956265e2951799887272d850872c3d79b09
  Account ID:       0x8556567610cf2d47587c9786bc6ef956265e2951799887272d850872c3d79b09
  SS58 Address:     6Ex8TY6RY7VeSeQxZLSu9JdMmh9p6tNGckdJGRyAfBHSUJMb
```

```
./subkey inspect -n legends --scheme sr25519 "siege six magnet law bubble elegant snack addict crack ranch tiger other//authority_discovery//go"
Secret Key URI `siege six magnet law bubble elegant snack addict crack ranch tiger other//authority_discovery//go` is account:
  Secret seed:      0x10c3d78f20e6f01e8760f4d1447d80d4929b39688ea1f48bb9e86729b618b9b8
  Public key (hex): 0xb4d6eba169950a77d7a8eb74fac608aefbc852559c34c73c6130871482e95b6c
  Account ID:       0xb4d6eba169950a77d7a8eb74fac608aefbc852559c34c73c6130871482e95b6c
  SS58 Address:     6G2QuVtL5eAJmiTjKMsxvs1TiP46mcSCii63dvcQUk4ceG4z
```

DON'T USE THESE KEYS, GENERATE YOUR NEW KEYS

### Setting systemd for the Validator Node
```
touch /etc/systemd/system/Legends-validator.service
```
add these code in Legends-validator.service, modify the port, ws-port, rpc-port if needec.
```
[Unit]
Description=Legends Validator

[Service]
ExecStart=/root/data-Legends/Legends -d /root/data-Legends/data-Le/bet-2 --port 30313 --ws-port 9944 --rpc-port 9933 --validator --name "your name by youself"
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```

then run these code:
```
 systemctl daemon-reload 
 systemctl enable Legends-validator.service 
 service Legends-validator start
 ```

 now you can check it's status by
 ```
 service Legends-validator status
 ```

 And Check the node status
 ```
  journalctl -f -u Legends-validator
```


### Insert keys(grandpa,babe,im_online, authority_discovery)

NOTE: these action insert it's Key URI and ACCOUNTID/PUBLICKEY(DONT USE SECRET KEY), IF YOUR RPC PORT NOT 9933, CHANGE IT
curl -H "Content-Type:application/json" -d '{"jsonrpc":"2.0", "id":1, "method":"author_insertKey", "params": [  "gran",  "siege six magnet law bubble elegant snack addict crack ranch tiger other//grandpa//go",  "0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06" ] }' http://localhost:9933

curl -H "Content-Type:application/json" -d '{"jsonrpc":"2.0", "id":1, "method":"author_insertKey", "params": [  "babe",  "siege six magnet law bubble elegant snack addict crack ranch tiger other//babe//go",  "0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06" ] }' http://localhost:9933

curl -H "Content-Type:application/json" -d '{"jsonrpc":"2.0", "id":1, "method":"author_insertKey", "params": [  "imon",  "siege six magnet law bubble elegant snack addict crack ranch tiger other//grandpa//go",  "0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06" ] }' http://localhost:9933

curl -H "Content-Type:application/json" -d '{"jsonrpc":"2.0", "id":1, "method":"author_insertKey", "params": [  "audi",  "siege six magnet law bubble elegant snack addict crack ranch tiger other//authority_discovery//go",  "0x48f5534249665d1453bf36856dfb642308d3431cd197ccb0da4484c0ca203d06" ] }' http://localhost:9933


### generate session key

```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

INSERT SESSION KEY IN THE WALLET STAKING / ACCOUNT ACTION, YOUR VALIDATOR RUNNING