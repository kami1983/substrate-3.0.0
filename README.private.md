
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
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//grandpa` is account:
  Secret seed:      0xbc1db4e400a1c79dd377c9b1c9b4ac3616a35f738bf5cd971b85f8f2ccb1e623
  Public key (hex): 0x3b7345bd36fb53c50be544a7c2847b9673984fa587af0c27108d3d464183e94f
  Account ID:       0x3b7345bd36fb53c50be544a7c2847b9673984fa587af0c27108d3d464183e94f
  SS58 Address:     5DQevdMyhfto9mME5BQoWTFySM21KsViJeTS21hSLjkqMMv7
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//1//im_online` is account:
  Secret seed:      0xf54304551c47dded0cf337a5a15d20035344f3df12456bd9028db47194802867
  Public key (hex): 0x94ff4a3dcd40926a375e9ebd640972598f7cf372e745fc5727a8020864bcb850
  Account ID:       0x94ff4a3dcd40926a375e9ebd640972598f7cf372e745fc5727a8020864bcb850
  SS58 Address:     5FS4nFmakmC7xydzUcsU14H51E2HEpmrdAym2hfEDihY9Vyp

  
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
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//grandpa` is account:
  Secret seed:      0xacbb1a1a8eb914d07e64605d623e3b6bab9016d786eea5f80c63d079472fc7b5
  Public key (hex): 0xa16c71b78c13cbd73e09cc348be1e8521ec2ce4c2615d4f2cf0e8148ba454a05
  Account ID:       0xa16c71b78c13cbd73e09cc348be1e8521ec2ce4c2615d4f2cf0e8148ba454a05
  SS58 Address:     5FiMnGQ7soNQe6kCh8LhoD6Za4eEMLbxKXDB5MDCsYixcpHG
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//2//im_online` is account:
  Secret seed:      0x8595f1595e8feb8f98b367e43f4faa9ea33defa0ee9bab431e8e85822d39123c
  Public key (hex): 0x6e6e4fd9c9ec79c902245ae1571d765ab24ff746620d138c2f2a0e3120634317
  Account ID:       0x6e6e4fd9c9ec79c902245ae1571d765ab24ff746620d138c2f2a0e3120634317
  SS58 Address:     5EZVtoYNs91WyfPUZCDbH8zWhA3eMz3x4qzr4mUETF8ijv7p
  
  
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
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//grandpa` is account:
  Secret seed:      0x608ee3b66f03b5c8b8c1fb9bc29fc6e4c942ea69e873e902d90804583fed3bc1
  Public key (hex): 0x2ce72e098beb0bc8ed6c812099bed8c7c60ae8208c94abf4212d7fdeaf11bab3
  Account ID:       0x2ce72e098beb0bc8ed6c812099bed8c7c60ae8208c94abf4212d7fdeaf11bab3
  SS58 Address:     5D5ae1KVDr3U8X5fFwKzGkzNJKW4dmC2iSAHQ9ZTfMer5EbM
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//3//im_online` is account:
  Secret seed:      0x7afb42072c55733c46ff1a4f8c005e9f2adbf29f02e88828d7229c3f0c908033
  Public key (hex): 0xbaaac69d2f30aeafcddd0fc43d23129aed7dde874cabb98efc3ab5b18fffa277
  Account ID:       0xbaaac69d2f30aeafcddd0fc43d23129aed7dde874cabb98efc3ab5b18fffa277
  SS58 Address:     5GHTVeYT1AYQyjLdUaAxGUCJR3SUkFEVZ9PdwPuXuAVaWrKq

  
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
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//grandpa` is account:
  Secret seed:      0x482c7058a677e608ce4a8776dd0b3c6474c0593fe948d62998002874031e2424
  Public key (hex): 0xb200d0328d26f7cbb67223c179ab14a2152d7afb6689f07b618fda33695d5fd4
  Account ID:       0xb200d0328d26f7cbb67223c179ab14a2152d7afb6689f07b618fda33695d5fd4
  SS58 Address:     5G66d3SAkfaBfDz7h5vRTMpsHMiNirNFkt1HrmQcCDJWehDk
Secret Key URI `blur pioneer frown science banana impose avoid law act strategy have bronze//4//im_online` is account:
  Secret seed:      0xf34286d301b8ce1ac2ca9b1f54f45f9d7a8022a0c2a62d88f205896de45f97c7
  Public key (hex): 0xb84e6cddf2b6e1ff5c76b8a71361e3f7a52c76605dbd2cfc069cec8975e12e1b
  Account ID:       0xb84e6cddf2b6e1ff5c76b8a71361e3f7a52c76605dbd2cfc069cec8975e12e1b
  SS58 Address:     5GEMxvuB7Kvs7JXUMiP8u7oLK8uUFqAfb25wn7nj1dNjm1WN




  
```

