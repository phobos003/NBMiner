# NBMiner
Nvidia GPU Miner for `Bytom(BTM)`, `Ethereum(ETH)`, `Monero(XMR)` mining.

Previously named `BTMiner_NebuTech`.

## 中文说明

[查看中文说明](/readme_zh.md)

## Download

[Download here](https://github.com/NebuTech/BTMiner_NebuTech/releases)

## Features：

* Support Bytom (BTM) mining, tensority algorithm.
  * Hashrate under default frequency: P106  1900H/s, 1070ti  3400H/s
  * Support Nvidia 10xx & 20xx GPUs.
* Support Ethereum (ETH) mining.
  * Highest profit on mining pools.
  * Support mining pools using ethproxy protocol.
* Support Monero(XMR) mining.
* Support Windows & Linux.
* Support backup mining pool configuration.
* Support SSL connection to mining pools.
* Dev Fee: BTM 2%, ETH 0.65%, XMR 0.65%

## Usage：

- **Driver version: Windows >= 397 , Linux >= 396**.
- BTM Mining:
  - Edit `start_btm.bat`, modify mining pool url after `-o` and username or wallet address after `-u`. 
- ETH Mining:
  - Edit `start_eth.bat`, modify mining pool url after `-o` and username or wallet address after `-u`. 
  - For users using 1080, 1080ti, 1060-5X cards, which equiped with GDDR5X memory, remember to start `OhGodAnETHlargementPill-r2.exe`  patch before mining and keep it running background.
- XMR Mining:
  - For windows users, the time-consume kernel used in XMR mining will cause TDR issue. Run `modify_tdr_delay.reg` and reboot windows for the first time you mine XMR.
  - Edit `start_xmr.bat`, modify mining pool url after `-o` and username or wallet address after `-u`. 

## CMD options：

**Typical usage** ：

- BTM: nbminer -a tensority -o stratum+tcp://btm.f2pool.com:9221 -u bm1xxxxxxxxxxxx.worker
- ETH: nbminer -a ethash -o **ethproxy**+tcp://eth.f2pool.com:8008 -u 0xxxxxxxxxx.worker
- XMR: nbminer -a cryptonightv8 -o -o stratum+tcp://xmr-jp1.nanopool.org:14444 -u 4xxxxxxxxx.worker

Options：

  * -h, --help    Displays this help.
  * -v, --version    Displays version information.
  * -c, --config \<config file path>    Use config file rather than cmd line options.
  * -a, --algo \<algo>    Select algorithm, `tensority` for BTM, `ethash` for ETH, `cryptonightv8` for XMR.
  * --api  \<host:port>    The endpoint for serving REST API.
  * -o, --url \<url>    Mining pool url.
    - BTM: stratum+tcp://btm.f2pool.com:9221
    - BTM with SSL: stratum+ssl://btm.f2pool.com:9443
    - ETH: ethproxy+tcp://eth.f2pool.com:8008
    - XMR: stratum+tcp://xmr.f2pool.com:13531
  * -u, --user \<user>    User used in Mining pool, wallet address or username.
      * Format: [username|wallet].workername:password
      * Example: bm1xxxxxx.worker      myusername.worker:password
  * -o1, --url1 \<url> url for backup mining pool 1.
  * -u1, --user1 \<user> username for backup mining pool 1.
  * -o2, --url2 \<url> url for backup mining pool 2.
* -u2, --user2 \<user> username for backup mining pool 2.
  * -d, --devices \<devices>    Specify GPU list to use. Format: "-d 0,1,2,3" to use first 4 GPU.
  * --strict-ssl    Check validity of certificate when use SSL connection.
  * --log    Generate log file named `log_<timestamp>.txt`.
  * --long-format    Use 'yyyy-MM-dd HH:mm:ss,zzz' for log time format.

## GPU Tuning

Bytom mining performance depend heavily on GPU core, instead of GPU memory.

Miner can gain beffer hashrate if tuning down GPU memory frequency.

For example, using MSI Afterburner to turn down GPU memory to -500.

## API Reference

### Web Monitor

Open http://api_host:port/ in your browser to use web monitor.

### Request

GET http://api_host:port/api/v1/status

### Response

``` json
{
    "miner": {
        "devices": [{
            "core_clock": 1556,
            "core_utilization": 100,
            "fan": 36,
            "hashrate": 1499,
            "id": 0,
            "info": "GeForce GTX 1080 Ti 11178 MB",
            "power": 182,
            "temperature": 65
        }, {
            "core_clock": 1518,
            "core_utilization": 100,
            "fan": 34,
            "hashrate": 1490,
            "id": 1,
            "info": "GeForce GTX 1080 Ti 11178 MB",
            "power": 172,
            "temperature": 62
        }],
        "total_hashrate": 2989,
        "total_power_consume": 354
    },
    "start_time": 1532482659,
    "stratum": {
        "accepted_share_rate": 0.99,
        "accepted_shares": 99,
        "password": "",
        "rejected_share_rate": 0.01,
        "rejected_shares": 1,
        "url": "btm.pool.zhizhu.top:3859",
        "use_ssl": false,
        "user": "bmxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.test",
        "difficulty": "0003ffff",
        "latency": 65
    },
    "version": "v10.0"
}
```

## Thanks

@earthGavinLee

## Change Log

#### v11.0(2018-12-12)

- Improve BTM hashrate.
- Add support for ETH and XMR mining.
- Optimize handle for new job, increase profit on mining pool.
- Colorful output on console.
- Add support for backup mining pools.
- Decrease dev fee of BTM to 2%.

#### v10.0(2018-10-03)

- Improve hashrate

#### v9.0(2018-08-28)

- Improve hashrate ~30%
- Improve stability

#### v8.0(2018-08-17)

- Improve hashrate 10% - 15%
- Lower skipped share rate, increase actual hashrate on mining pool.
- Added display for mining pool latency.
- Added display for mining pool difficulty.
- Improve API web monitor.
