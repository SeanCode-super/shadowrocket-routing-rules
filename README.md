# Shadowrocket 分流规则

仅公开分流规则，不提供代理节点或订阅。更新日期：2026-10-09。

## 内容与使用

[`rules.conf`](rules.conf) 只含 `[Rule]` 段，共 4,901 条有效规则。它不是完整的小火箭配置，不能作为包含节点的订阅使用，也不建议直接替换正在工作的完整配置。

备份现有配置后，将本文件的 `[Rule]` 内容合并到现有配置中。`DIRECT` 表示直连；`PROXY` 表示代理策略，使用自定义策略组时请将其替换为自己的策略组名。文件不选择出口国家，也不提供节点。

规则按顺序首次匹配：

1. Google、Meta、ChatGPT / OpenAI、Claude、X / Twitter、Grok / xAI、海外 TikTok 等已收录域名优先走代理。
2. 中国抖音、QQ / 微信及已收录的国内应用域名直连。
3. 局域网、回环和链路本地等保留地址直连。
4. 其余中国大陆 IP 由 `GEOIP,CN,DIRECT` 直连；剩余目标由 `FINAL,PROXY` 走代理。

抖音与 TikTok 的共享域名不作全量直连；部分共享域名仍交由 GeoIP 和最终规则判断。GeoIP 准确性取决于客户端数据库。本文件不修改 DNS、IPv6、WebRTC、证书、脚本或系统代理设置，不保证消除所有泄漏，也不改变 IP 信誉或账号地区。

当前内容是经过规则语法、顺序和典型域名匹配检查的静态快照，不代表所有应用、网络和未来新增域名都经过实机验证。仓库未设置自动更新。

## 隐私边界

仓库不包含 `[Proxy]`、`[Proxy Group]`、`[General]`、`[Host]`，不包含个人服务器地址、端口、节点名、密码、UUID、密钥、订阅地址或浏览器数据。原有私人策略组名已统一替换为 `PROXY`。IP 段规则仅包含通用保留地址范围。

只在独立目录中发布规则及必要的说明、许可证；`.gitignore` 默认忽略未列入白名单的文件。仍请在每次提交前检查暂存区，切勿将完整个人配置提交到公开仓库。

## 来源、修改与许可证

本仓库包含以下公开项目规则的筛选、转换和补充，不是这些项目的官方发布：

- [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community/tree/e84921279c9142434b43cb84ec6c17f987e025df)：固定版本 `e84921279c9142434b43cb84ec6c17f987e025df`，用于海外服务及抖音域名来源。原 MIT 版权和许可证保留于 [`LICENSES/v2fly-MIT.txt`](LICENSES/v2fly-MIT.txt)。
- [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script/tree/036c097eb26c6a52c4f04ebcb6633043cb942669/rule/Shadowrocket)：固定版本 `036c097eb26c6a52c4f04ebcb6633043cb942669`，GPL-2.0。国内应用补充仅选取域名规则，排除了宽泛 IP / ASN、脚本及不适合当前分流目标的共享海外域名。

2026-10-09 的修改包括：规则筛选与去重、域名格式转换、海外规则优先排序、抖音 / TikTok 区分、国内应用域名补充、仅导出规则段、将私人策略名替换为 `PROXY`。原始来源注释保留在规则文件内。

本仓库的组合及修改版按 [GNU GPL v2](LICENSE) 发布，上游各自的版权声明继续保留。按现状提供，不附带任何担保。
