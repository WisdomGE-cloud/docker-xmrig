# docker-xmrig（xmrig的docker镜像）
[![xmr](http://dockeri.co/image/wisdomclouds/xmrig)](https://hub.docker.com/r/wisdomclouds/xmrig)

docker images for xmrig、monero

xmrig版本: xmrig-6.18.0-c3pool

## Docker安装

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

systemctl start docker 
systemctl enable docker
```

## 使用教程
1. 复制[config.json](https://github.com/WisdomGE-cloud/docker-xmrig/blob/master/config/config.json)到服务器目录/etc/xmrig/config.json下.
```bash
        wget -P /etc/xmrig/ https://raw.githubusercontent.com/WisdomGE-cloud/docker-xmrig/master/config/config.json
```

2. 编辑/etc/xmrig/config.json.
```bash
        vim /etc/xmrig/config.json
```
   当然也可以选择其他编辑器，按个人习惯.
```bash
        "url": "mine.c3pool.com:13333",
        "user": "你的门罗币地址",
        "pass": "矿工名:电子邮件地址",
```
   例：
```bash
        "url": "mine.c3pool.com:13333",
        "user": "41rbVjedxGN8azw3gZsVYTJhgQEY4xvRtBFQ6i3wbdPAY5fGqtMVG9iZ8usf8ema2P5XXZkvLPtGRJf1mRw51SwfQoUJYmh",
        "pass": "x:xxx@gmail.com",
```

* url: 门罗币矿池地址，默认猫池，你也可以选[其他矿池](https://monero.org/services/mining-pools/)
* user: 你的门罗币地址
* pass: 矿工名:电子邮件地址

3. 在你的服务器中运行docker镜像.

```bash
docker run --restart=always --network host -d -v /etc/xmrig/config.json:/etc/xmrig/config.json --name xmr wisdomclouds/xmrig
```

默认开启限制CPU为百分之90，当然你可以更改参数CPU_USAGE.[0 - 100]，[0 - 100]为相应百分比，例如：CPU_USAGE=50，即限制单核百分之50运行。

例：

```bash
docker run --restart=always --network host -d -v /etc/xmrig/config.json:/etc/xmrig/config.json -e CPU_USAGE=100 --name xmr wisdomclouds/xmrig
```

## 查看日志

查看命令：

```bash
docker logs -f xmr
```

日志输出：

```bash
# docker logs -f xmr
 * ABOUT        XMRig/6.12.2-C3Pool gcc/9.3.0
 * LIBS         libuv/1.41.0 OpenSSL/1.1.1k hwloc/2.4.1
 * HUGE PAGES   supported
 * 1GB PAGES    supported
 * CPU          AMD Ryzen 9 3900X 12-Core Processor (1) 64-bit AES VM
                L2:0.5 MB L3:16.0 MB 1C/1T NUMA:1
 * MEMORY       0.4/0.5 GB (75%)
 * DONATE       0%
 * ASSEMBLY     auto:ryzen
 * POOL #1      mine.c3pool.com:13333 algo auto
 * COMMANDS     hashrate, pause, resume, results, connection
[2021-06-08 01:13:42.120]  config   configuration saved to: "/etc/xmrig/config.json"
[2021-06-08 01:13:42.120]  benchmk   STARTING ALGO PERFORMANCE CALIBRATION (with 20 seconds round) 
[2021-06-08 01:13:42.120]  benchmk   Algo cn/r Preparation 
[2021-06-08 01:13:42.120]  cpu      use profile  cn  (1 thread) scratchpad 2048 KB
[2021-06-08 01:13:42.556]  cpu      READY threads 1/1 (1) huge pages 0% 0/1 memory 2048 KB (436 ms)
[2021-06-08 01:13:42.648]  benchmk   Algo cn/r Starting test 
[2021-06-08 01:14:02.888]  benchmk   Algo cn/r hashrate: 70.188362 
[2021-06-08 01:14:02.888]  benchmk   Algo cn-lite/1 Preparation 
[2021-06-08 01:14:02.888]  cpu      stopped (0 ms)
[2021-06-08 01:14:02.888]  cpu      use profile  cn-lite  (1 thread) scratchpad 1024 KB
[2021-06-08 01:14:02.902]  cpu      READY threads 1/1 (1) huge pages 0% 0/1 memory 1024 KB (14 ms)
[2021-06-08 01:14:02.996]  benchmk   Algo cn-lite/1 Starting test 
[2021-06-08 01:14:23.010]  benchmk   Algo cn-lite/1 hashrate: 175.368421 
[2021-06-08 01:14:23.010]  benchmk   Algo cn-heavy/xhv Preparation 
[2021-06-08 01:14:23.013]  msr      msr kernel module is not available
[2021-06-08 01:14:23.013]  msr      FAILED TO APPLY MSR MOD, HASHRATE WILL BE LOW
[2021-06-08 01:14:23.017]  cpu      stopped (4 ms)
[2021-06-08 01:14:23.017]  cpu      use profile  cn-heavy  (1 thread) scratchpad 4096 KB
[2021-06-08 01:14:23.063]  cpu      READY threads 1/1 (1) huge pages 0% 0/2 memory 4096 KB (46 ms)
[2021-06-08 01:14:23.332]  benchmk   Algo cn-heavy/xhv Starting test 
[2021-06-08 01:14:42.134]  miner    speed 10s/60s/15m 69.54 n/a n/a H/s max 70.05 H/s
[2021-06-08 01:14:43.511]  benchmk   Algo cn-heavy/xhv hashrate: 70.173593 
[2021-06-08 01:14:43.511]  benchmk   Algo cn-pico Preparation 
[2021-06-08 01:14:43.512]  cpu      stopped (0 ms)
[2021-06-08 01:14:43.512]  cpu      use profile  cn-pico  (1 thread) scratchpad 256 KB
[2021-06-08 01:14:43.516]  cpu      READY threads 1/1 (2) huge pages 0% 0/1 memory 512 KB (4 ms)
[2021-06-08 01:14:43.523]  benchmk   Algo cn-pico Starting test 
```

## 友情链接

[![vultr](https://www.vultr.com/media/banners/banner_728x90.png)](https://www.vultr.com/?ref=8777656-6G)

[![bandwagonhost](https://bwh88.net/templates/organicbandwagon/images/banner1.jpg)](https://bwh88.net/aff.php?aff=60603)

## 欢迎捐赠

我的门罗币地址:

41rbVjedxGN8azw3gZsVYTJhgQEY4xvRtBFQ6i3wbdPAY5fGqtMVG9iZ8usf8ema2P5XXZkvLPtGRJf1mRw51SwfQoUJYmh

## 参考链接

1. [monero](https://web.getmonero.org/)
1. [c3pool](https://c3pool.com/#/dashboard)
1. [cpulimit](https://github.com/opsengine/cpulimit/)
1. [snowdream/docker-xmr](https://github.com/snowdream/docker-xmr)
