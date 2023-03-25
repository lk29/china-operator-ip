# Chinese operator IP address database
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fgaoyifan%2Fchina-operator-ip.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fgaoyifan%2Fchina-operator-ip?ref=badge_shield)


IP address database classified according to Chinese network operators

## Why create this project

In China, there is only one commercial service for BGP/ASN data analysis [ipip.net](https://www.ipip.net), which is currently the service provider with the highest accuracy of the operator's IP database. I don't think there is one.

With the increase of the scale of the Internet, in order to process a large amount of routing data, the Border Gateway Protocol (BGP, the same below) came into being and is one of the basic protocols of the Internet. In order to ensure the reachability of global network routes, any IP (segment) that needs to be registered on the Internet needs to be announced externally with the help of the BGP protocol, so that other autonomous domains in the Internet can learn the routing information of this address, and other hosts In order to successfully access this IP (segment). Therefore, it can be said that BGP data is one of the most suitable data sources for analyzing the IP addresses of operators.

However, at present, most IP databases in China use [WHOIS database](https://ftp.apnic.net/apnic/whois/apnic.db.inetnum.gz) as the basic data source. WHOIS data only indicates which organization an IP is registered by, but there is no way to know where the IP is used, which leads to the inability to correctly classify many IP addresses registered by non-operators themselves. ipip.net is one of the earliest companies that started to analyze BGP/ASN data, and the accuracy of the data is several blocks away from other databases. But it is a pity that, as a commercial company, ipip.net charges for most of the high-quality IP data, and the price is not cheap.

Since I need to process BGP data when doing other projects, in the spirit of open source, I repackaged this part of the code and created this project. As for how to use it, everyone can use their imagination. For example: [@ustclug](https://github.com/ustclug) uses it on the authoritative DNS server for domain resolution; I use this IP library to make a multi-exit gateway, when accessing different operators Take a different route (if they don't match, go to a foreign vps, you understand the reason).

However, due to limited personal energy, the coverage rate of the IP library is not as good as ipip.net, especially the addresses of some backbone network nodes. These addresses are often the addresses hosted by core routing equipment or enterprises to operators, and have little impact on ordinary users.

If you have any suggestions or questions, please submit an issue.

## Included operators

* China Telecom (chinanet)
* China Mobile (cmcc)
* China Unicom (unicom)
* ~~China Railcom (tietong)~~<will be obsolete>
* Education Network (cernet)
* Technology Network (cstnet)
* Dr. Peng (drpeng) <experimental phase>
* Google China (googlecn) <experimental phase>

*P.S. Since China Mobile and Tietong have been merged, Tietong collection will be deprecated soon, see [issue #10](https://github.com/gaoyifan/china-operator-ip/issues/10) for details. In consideration of compatibility, China Railcom's pre-generated data is currently the same as that of China Mobile, and China Railcom will be removed at an appropriate time in the future. *

*P.S. The IP addresses of Dr. Peng Group (including: Dr. Peng Data, Beijing Telecom, Great Wall Broadband, and Broadband) are not all announced by independent autonomous domains. At present, most of the addresses are still announced by China Telecom, China Unicom, and Science and Technology Network. Therefore, the addresses in the [list](https://github.com/gaoyifan/china-operator-ip/blob/ip-lists/drpeng.txt) are only part of the IP addresses owned by Dr. Peng, and these IPs also have telecommunications , China Unicom two superior exits. See [issue #2](https://github.com/gaoyifan/china-operator-ip/issues/2) for details.*

*P.S. If you need a collection of all domestic addresses, please refer to [chnroutes2](https://github.com/misakaio/chnroutes2) project*

## How to get data

### Use pregenerated results

The IP list (CIDR format) is saved in the [ip-lists branch](https://gaoyifan.github.io/china-operator-ip/index.html) of the warehouse, and GitHub Actions is automatically updated daily.

```sh
git clone -b ip-lists https://github.com/gaoyifan/china-operator-ip.git
```

P.S. [stat file](https://github.com/gaoyifan/china-operator-ip/blob/ip-lists/stat) records the statistics of the number of IPs of each operator.

### Generated from BGP data

#### Install dependencies

* [bgptools](https://github.com/gaoyifan/bgptools) (`cargo install bgptools`)
* [bgpdump](https://bitbucket.org/ripencc/bgpdump-hg/wiki/Home) (`apt install bgpdump`)
* [cidr-merger](https://github.com/zhanhb/cidr-merger) (`go get github.com/zhanhb/cidr-merger`)

#### Generate IP list

```shell
./generate.sh
```

#### Count the number of IPs

```shell
./stat.sh
```
## Acknowledgments

* Thanks to brother [boj](https://ring0.me) for the [design suggestion](https://github.com/ustclug/discussions/issues/79#issuecomment-267958775)
* Thanks to [University of Oregon Route Views Archive Project](http://archive.routeviews.org) project for providing BGP data source
* Thanks to [Travis CI](https://travis-ci.org) for providing an excellent continuous integration platform
* Thanks to [GitHub](https://github.com/features/actions) for providing computing resources
* Thanks to the [cidr-merger](https://github.com/zhanhb/cidr-merger) project for providing an efficient IP address merging tool
* Thanks to [bgpdump](https://bitbucket.org/ripencc/bgpdump/wiki/Home) project for providing rib data reading tools

## protocol

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fgaoyifan%2Fchina-operator-ip.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fgaoyifan%2Fchina-operator-ip?ref=badge_large)
