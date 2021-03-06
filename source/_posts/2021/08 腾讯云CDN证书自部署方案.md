---
title: 腾讯云 CDN 证书自部署方案
seo_title: 腾讯云 CDN 证书自部署方案
toc: true
indent: true
tag:
  - CDN
  - SSL
categories: 资料
date: '2021-08-20 21:38'
updated: '2021-08-20 22:35'
hideTitle: false
headimg: ../../img/article/腾讯云CDN证书自部署方案/main.webp
description: 利用腾讯云 SDK 自动更新内容分发的域名所使用的证书。
abbrlink: 6b3511b1
---

{% p center logo large, 腾讯云 CDN 证书自部署方案 %}

全球各大证书权威签发机构已停止签发有效期超过 1 年的 SSL 证书，而腾讯云的内容分发不支持对域名证书自动续期，所以如果更新证书变得有那么一丝丝的麻烦。而另外一个原因则是商用泛域名证书太贵了，免费的泛域名证书目前仅 {% span logo  red, Let's Encrypt %} 一家，而它更需要频繁更新证书^[一般一年制证书为 398 天，Let's Encrypt 的证书为 90 天。]。

幸运的是腾讯云几乎所有的操作都有可供调用的 Api，更新内容分发的 CDN 证书也是不在话下。

## 泛域名证书获取

有两种方案：一是利用宝塔面板的 SSL 证书模块，自助组合泛域名证书，申请成功后通过定时任务定期检查更新；另一个是利用 acme.sh ，独立的进行证书申请，这里着重记录下它 *（以下操作仅在 Linux 系统测试）*。

### 应用安装

此处使用 Git 方式安装：

```sh 克隆仓库
git clone https://github.com/acmesh-official/acme.sh.git && cd acme.sh
```

```sh 安装 acme.sh
./acme.sh --install  \
--home ~/myacme \
--accountemail  "my@example.com"
```

### 生成证书

`DP_ID` DNSPod 的 Api ID ； `DP_KEY` DNSPod 的 Api Key 。

`--force` 覆盖已有文件；`--dnssleep 0` 跳过 DNS 校验 *（太慢）* 。

```sh 生成泛域名证书 *.inkss.cn
export DP_Id="1234"
export DP_Key="sADDsdasdgdsf"
acme.sh --issue --dns dns_dp -d "*.inkss.cn" --force --dnssleep 0
```

### 部署证书

按照 Nginx 证书格式导出到 `/opt/ssl/inkss.cn` 目录。

```sh
acme.sh --install-cert -d "*.inkss.cn" \                         
--key-file /opt/ssl/inkss.cn/privkey.pem \
--fullchain-file /opt/ssl/inkss.cn/fullchain.pem
```

## 泛域名证书部署

接下来就需要部署证书至腾讯云 CDN，此部分采用 Node 版本。

{% folding cyan open, TecentCDN %}

{% tabs CDN-SSL %}

<!-- tab package.json -->
```json
{
  "dependencies": {
    "silly-datetime": "^0.1.2",
    "tencentcloud-sdk-nodejs": "^4.0.184"
  }
}
```
<!-- endtab -->

<!-- tab index.js -->
```js
const fs = require("fs");
const date = require("silly-datetime");
const CdnClient = require("tencentcloud-sdk-nodejs").cdn.v20180606.Client;

const Client = new CdnClient({
  credential: {
    secretId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    secretKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  },
  region: "ap-shanghai",
  profile: {
    httpProfile: {
      endpoint: "cdn.tencentcloudapi.com"
    }
  }
});
const GlobalData = {
  domain: ["inkss.cn"],
  template: {
    "Domain": "",
    "Https": {
      "Switch": "on",
      "Http2": "on",
      "OcspStapling": "on",
      "Hsts": {
        "Switch": "on",
        "MaxAge": 31536000
      },
      "CertInfo": {
        "Certificate": "",
        "PrivateKey": "",
        "Message": "更新日期：" + date.format(new Date(), 'YYYY-MM-DD HH:mm')
      }
    }
  }
};

/**
 * 根据域名生成对应配置
 * @param domain 域名
 */
function genParam(domain) {
  let cert, key;
  const temp = GlobalData.template;
  if (domain.includes('inkss.cn')) {
    cert = fs.readFileSync("/opt/ssl/inkss.cn/fullchain.pem", 'utf-8');
    key = fs.readFileSync("/opt/ssl/inkss.cn/privkey.pem", 'utf-8');
  } else {
    return null;
  }
  temp.Domain = domain;
  temp.Https.CertInfo.Certificate = cert;
  temp.Https.CertInfo.PrivateKey = key;
  return temp;
}

/**
 * 部署证书
 */
Client.DescribeDomains({}).then((data) => {
  const domainList = [];
  if (data['Domains']) data['Domains'].forEach(item => {
    if (item['Domain']) domainList.push(item['Domain'])
  })
  domainList.forEach(domain => {
    setTimeout(() => {
      Client.UpdateDomainConfig(genParam(domain)).then(
        () => {
          console.log(`域名 【${domain}】 更新证书完成。`);
        }, err => {
          console.error(`域名 【${domain}】 更新失败： ${err}`);
        }
      )
    }, 100)
  })
}, (err) => {
  console.error("CDN 域名查询失败：", err);
})
```
<!-- endtab -->

{% endtabs %}

{% endfolding %}
