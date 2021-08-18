
## Docker 编译

* 镜像名称 paritytech/ci-linux:974ba3ac-20201006
* 运行方式
  docker run --rm -v $(PWD):/builds paritytech/ci-linux:3d4ca6a9-20210708 bash -c "cargo build --release"

## 链启动
```asm

./target/debug/substrate build-spec --chain staging --disable-default-bootnode > my-staging.json
./target/debug/substrate build-spec --chain staging --raw  --disable-default-bootnode > my-staging-raw.json

```

##  Start your bootnodes, node key can be generate with command 
```asm
./target/debug/substrate key generate-node-key
```

### 返回：
```asm

12D3KooWGuNM14pnggJogJSUtJ8u1Quw9CuqwR6j5dr9SbFF57kP
62c32b50d59b5a1b3ef71789be121dd636040a403495335c7a44ccd1824f0f1d%  

```
## 启动 bootnodes 
```arm

./target/debug/substrate \
    --ws-external \
    --rpc-external \
    --rpc-cors=all \
    --rpc-methods=Unsafe \
    --node-key 62c32b50d59b5a1b3ef71789be121dd636040a403495335c7a44ccd1824f0f1d \
    --base-path /tmp/bootnode1 \
    --chain my-staging-raw.json \
    --name bootnode1
    --validator 
```

## 启动验证人节点 1
```asm
./target/debug/substrate \
    --base-path  /tmp/validator1 \
    --chain my-staging-raw.json \
    --bootnodes  /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWGuNM14pnggJogJSUtJ8u1Quw9CuqwR6j5dr9SbFF57kP \
    --port 30336 \
    --ws-port 9947 \
    --rpc-port 9936 \
    --name  validator1 \
    --validator 
```


## 启动验证人节点 2
```asm
./target/debug/substrate \
    --base-path  /tmp/validator2 \
    --chain   my-staging-raw.json \
    --bootnodes  /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWGuNM14pnggJogJSUtJ8u1Quw9CuqwR6j5dr9SbFF57kP \
    --port 30337 \
    --ws-port 9948 \
    --rpc-port 9937 \
    --name  validator2 \
    --validator 
```

## 启动验证人节点 3
```asm
./target/debug/substrate \
    --base-path  /tmp/validator3 \
    --chain   my-staging-raw.json \
    --bootnodes  /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWGuNM14pnggJogJSUtJ8u1Quw9CuqwR6j5dr9SbFF57kP \
    --port 30338 \
    --ws-port 9949 \
    --rpc-port 9938 \
    --name  validator3 \
    --validator 
```

# 给每个验证人设置 Session Keys
``` babe session
curl http://localhost:9933  -H "Content-Type:application/json;charset=utf-8" -d "@babe1.curl"
curl http://localhost:9936  -H "Content-Type:application/json;charset=utf-8" -d "@babe2.curl"
curl http://localhost:9937  -H "Content-Type:application/json;charset=utf-8" -d "@babe3.curl"
curl http://localhost:9938  -H "Content-Type:application/json;charset=utf-8" -d "@babe4.curl"
```

```grandpa session
curl http://localhost:9933  -H "Content-Type:application/json;charset=utf-8" -d "@gran1.curl"
curl http://localhost:9936  -H "Content-Type:application/json;charset=utf-8" -d "@gran2.curl"
curl http://localhost:9937  -H "Content-Type:application/json;charset=utf-8" -d "@gran3.curl"
curl http://localhost:9938  -H "Content-Type:application/json;charset=utf-8" -d "@gran4.curl"
```

```imonline session
curl http://localhost:9933  -H "Content-Type:application/json;charset=utf-8" -d "@imonline1.curl"
curl http://localhost:9936  -H "Content-Type:application/json;charset=utf-8" -d "@imonline2.curl"
curl http://localhost:9937  -H "Content-Type:application/json;charset=utf-8" -d "@imonline3.curl"
curl http://localhost:9938  -H "Content-Type:application/json;charset=utf-8" -d "@imonline4.curl"
```

## 生成账户：

// for i in 1 2 3 4; do for j in stash controller; do subkey inspect "$SECRET//$i//$j"; done; done
// for i in 1 2 3 4; do for j in babe; do subkey --sr25519 inspect "$SECRET//$i//$j"; done; done
// for i in 1 2 3 4; do for j in grandpa; do subkey --ed25519 inspect "$SECRET//$i//$j"; done; done
// for i in 1 2 3 4; do for j in im_online; do subkey --sr25519 inspect "$SECRET//$i//$j"; done; done


subkey inspect 

## subkey generate 
`./account-gen.sh 执行`

### KEY: blur pioneer frown science banana impose avoid law act strategy have bronze
``` 
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//stash` is account:
  Secret seed:      0xca48b1421d35b9ccc59d5304d74dee95304470571c7a118a860d00e7cf075338
  Public key (hex): 0x70214e02fb2ec155a4c7bb8c122864b3b03f58c4ac59e8d83af7dc29851df657
  Account ID:       0x70214e02fb2ec155a4c7bb8c122864b3b03f58c4ac59e8d83af7dc29851df657
  SS58 Address:     5Ebj7Z9DUSUjHUaqQGsH15iFe83GWbznJgWKbyLCWPoVMbWK
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//controller` is account:
  Secret seed:      0xf7a139713338804e7d9384809dc7324895a1e292b3d4b402160b5d2b1931b42b
  Public key (hex): 0xaaf0c45982a423036601dcacc67854b38b854690d8e15bf1543e9a00e660e019
  Account ID:       0xaaf0c45982a423036601dcacc67854b38b854690d8e15bf1543e9a00e660e019
  SS58 Address:     5FvqX8XdznMZajt4oiGqmm87p1tW48yksTU6mPwtDFdcviQh
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//babe` is account:
  Secret seed:      0x1b25bbdf6259f031b4b79f7c784e2c47f550d6815e8adf7b5bf77da98654b3a1
  Public key (hex): 0x1e876fa1b4bbb82785ea5670b7ce0976beaf7536b6a0cc05deba7a54ab709421
  Account ID:       0x1e876fa1b4bbb82785ea5670b7ce0976beaf7536b6a0cc05deba7a54ab709421
  SS58 Address:     5CkjXVnejasckXZPqNZRnfrUx4kSLrZhbzJJcU4ZVJ63VuoL
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//grandpa --scheme Ed25519` is account:
  Secret seed:      0xb94da9fe7c67e5d2b6d97a067cede6b0e808025b9effe0881fc4b62ba23fecc5
  Public key (hex): 0xf8ca55b0a401e6f2663e800d4ae8673da69a4db1765e561bb9b422808a6a4528
  Account ID:       0xf8ca55b0a401e6f2663e800d4ae8673da69a4db1765e561bb9b422808a6a4528
  SS58 Address:     5Hguqb634syw4sYRteQv7MxJMV1ZDgtbkYnK18e7FVmYw2gW
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//im_online --scheme Sr25519` is account:
  Secret seed:      0x6a2ab20b3bd8c86835fb5f46de0af4680e6df688c02eb51779a98ca6f9632d53
  Public key (hex): 0xf869c49195a98b83db3ea3822a12ab70d43e83cc765cb5f68e82debff0d6a410
  Account ID:       0xf869c49195a98b83db3ea3822a12ab70d43e83cc765cb5f68e82debff0d6a410
  SS58 Address:     5HgR9nBseKtj8rNxiuJ7HkBHF3CHbBcr2nF86TbKE2gHFvh9
  
``` 
``` 
  
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//stash` is account:
  Secret seed:      0xa0f62f99e6f931f4c36993b380b0662c389bf7079b9146afc56bcd8343093eff
  Public key (hex): 0xc82c3780d981812be804345618d27228680f61bb06a22689dcacf32b9be8815a
  Account ID:       0xc82c3780d981812be804345618d27228680f61bb06a22689dcacf32b9be8815a
  SS58 Address:     5GbAZyAiXR9xPWjRRV9txrCCh9CpxUBmGm5grXAGdReCzShY
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//controller` is account:
  Secret seed:      0x0849103b629ca44786025cc2758be58a4dd70d42e4334d8f99eba6a4b485fb01
  Public key (hex): 0x74a173a22757ddc9790ed388953a1ed8a5933a421858533411b36ebd41d74165
  Account ID:       0x74a173a22757ddc9790ed388953a1ed8a5933a421858533411b36ebd41d74165
  SS58 Address:     5EhdNat32kdbSSfgwwyHMfMX27sFeDdmgSh665LdhisxugB2
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//babe` is account:
  Secret seed:      0xec6c7b1a2f176f9b9fd68ce3163c49448748d544202a3b3523bde99f61133a15
  Public key (hex): 0xd25900272b16897ec18a04b7d7d704954e6bdc35ae5a09305aa2e0cc2bf10e5c
  Account ID:       0xd25900272b16897ec18a04b7d7d704954e6bdc35ae5a09305aa2e0cc2bf10e5c
  SS58 Address:     5GpWMMCTjhZcZPEMgei3RXQdBKMo4L8dPoM2BeXrNcoPvQGG
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//grandpa --scheme Ed25519` is account:
  Secret seed:      0x186d1d130f31f1955dff7ff60a622dcc0a9e199380f0b0b4585aceb76a40c4b4
  Public key (hex): 0xb202808490659485097b958609b638bfe000fd30634576ff80fab486533abc26
  Account ID:       0xb202808490659485097b958609b638bfe000fd30634576ff80fab486533abc26
  SS58 Address:     5G67892puhVJBXVNLBW2XpwzJJufr68WJ5jnJKdk3vzonba9
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//im_online --scheme Sr25519` is account:
  Secret seed:      0x6afd0996b153e69edb810290c3884be6db5e9ff32cc4ca3b6d81f330527246df
  Public key (hex): 0x3ce3a879a90d74921c5002d39f22223a84e415260c6d95f252178ed42fe2eb34
  Account ID:       0x3ce3a879a90d74921c5002d39f22223a84e415260c6d95f252178ed42fe2eb34
  SS58 Address:     5DSYMmLz8FVnwktf4CDeafw1NCmRf5V4hEV41t2QCwyt5dnB
``` 
``` 
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//stash` is account:
  Secret seed:      0x79dfe07b165324dbc7c48d76ea0f8f69981f619ecccbab30ee4ca1cd9a72414c
  Public key (hex): 0xacad76a1f273ab3b8e453d630d347668f1cfa9b01605800dab7126a494c04c7c
  Account ID:       0xacad76a1f273ab3b8e453d630d347668f1cfa9b01605800dab7126a494c04c7c
  SS58 Address:     5Fy7d56q8apQciKoex9EfBrGQGguQGaFHJYR9UGkYMn56PuX
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//controller` is account:
  Secret seed:      0x7190df989b4f7fbbde79eb878d5e370bb76e9f063ae777a79bdf12e3772ec303
  Public key (hex): 0x9e55f821f7b3484f15942af308001c32f113f31444f420a77422702907510669
  Account ID:       0x9e55f821f7b3484f15942af308001c32f113f31444f420a77422702907510669
  SS58 Address:     5FeJxhZhmfED6PqRge9SpMzsJi33JxnZWoBNeg6aEPx3jC2d
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//babe` is account:
  Secret seed:      0x35ffa16438daeb83cccebe1552fbe40af3190e279938cf2cc60e802cc7869874
  Public key (hex): 0xb4879945ce4ef0b387857026c2b6fc8b15dec3386ad13b7bf7d978e484080a18
  Account ID:       0xb4879945ce4ef0b387857026c2b6fc8b15dec3386ad13b7bf7d978e484080a18
  SS58 Address:     5G9Qktxa1ee2RCWeHZY1itHZaTMagCHeNVWHoJhvknJBbuQS
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//grandpa --scheme Ed25519` is account:
  Secret seed:      0xfc6365923a45f6a698a7705a0d33ad05817910bcf4f09917cb6d255e070d2182
  Public key (hex): 0x5851417796f6a978ed3cf50e324a78b515a498fd29b782286972baedc1702e76
  Account ID:       0x5851417796f6a978ed3cf50e324a78b515a498fd29b782286972baedc1702e76
  SS58 Address:     5E4WD5MhkrGYNr3PUWnJ8Uhff4eSmbVyNxJwfux4Chjxikt8
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//im_online --scheme Sr25519` is account:
  Secret seed:      0xd4511fc2ffcbf057cd04a052282829539e45d1b15f04b6fcf4de08b58e165373
  Public key (hex): 0x4cb333308579feb12a1f766e5cfe0f68d441a6fefecd2208775ff253f6f98228
  Account ID:       0x4cb333308579feb12a1f766e5cfe0f68d441a6fefecd2208775ff253f6f98228
  SS58 Address:     5DoGjHeu3tL3vzyLf1csx3uGM4BWqRZbTJw7TpWYcEmG8NxC
``` 
``` 
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//stash` is account:
  Secret seed:      0xf9630215b8a31686ed14bc660210512bf773b91b582d99d402a5d2de7bdef6d5
  Public key (hex): 0x4aa6e0eeed2e3d1f35a8eb1cd650451327ad378fb8975dbf5747016ff3be2460
  Account ID:       0x4aa6e0eeed2e3d1f35a8eb1cd650451327ad378fb8975dbf5747016ff3be2460
  SS58 Address:     5DkaySbFDzQ8RwNa6JnMdEFFdB8LpMuGCQGYfmUGZbZuPGW6
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//controller` is account:
  Secret seed:      0x12f45e727fa7404997b9211ea66a76f63bc57848ce63d8062a3f280738f12ed3
  Public key (hex): 0x587bae319ecaee13ce2dbdedfc6d66eb189e5af427666b21b4d4a08c7af0671c
  Account ID:       0x587bae319ecaee13ce2dbdedfc6d66eb189e5af427666b21b4d4a08c7af0671c
  SS58 Address:     5E4ip35pxFHj3JSYhaLcDZNnFYdqserEg9imnwL5ssM1WzHy
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//babe` is account:
  Secret seed:      0xaeab26a6b6f9b328875545f44f7e0f65705e319591d55435893653ccd3549883
  Public key (hex): 0x126bae3dea6a6a6e346bc0dc2beb4e1c9e54aaf1c0732bf67ff03d772f6a6208
  Account ID:       0x126bae3dea6a6a6e346bc0dc2beb4e1c9e54aaf1c0732bf67ff03d772f6a6208
  SS58 Address:     5CUrhxK8xSwiyUBHtBdEGCuqhNe9At646hdpQBbrdG1bRb4B
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//grandpa --scheme Ed25519` is account:
  Secret seed:      0x2cdae18899f336f25b3fa1a39d5cb28a2f6a4e7cefa34107985c32cfa6bd107e
  Public key (hex): 0xfe9417ed8d26b212bf937adbd29152aa1b2645d384ad694364b591e4c9f72a7c
  Account ID:       0xfe9417ed8d26b212bf937adbd29152aa1b2645d384ad694364b591e4c9f72a7c
  SS58 Address:     5HpW1hPu33DjsAmmdpgaWatd96b1LBkVV4hxX3DNSeznDCLK
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//im_online --scheme Sr25519` is account:
  Secret seed:      0x877ae9b4ab0c303430142a0bf71c3333bdd6e6067f36945db1716a323a8d4047
  Public key (hex): 0x0ec96712118ebca534f2082a59a9b70fc2185b4fd537a11b3792e4b3f12a0453
  Account ID:       0x0ec96712118ebca534f2082a59a9b70fc2185b4fd537a11b3792e4b3f12a0453
  SS58 Address:     5CQ6MdvjHUFnhdrdYAn7AzQ8TjE1z6BPMmYDZRBXBn8pV7pW
  
```


