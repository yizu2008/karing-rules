# karing-rules

Karing 远程分流规则集（sing-box source 格式，`version: 2`），可在 Karing 里当 Rule Set 线上导入。

## 规则

| 文件 | 说明 | Raw 链接 |
| --- | --- | --- |
| `Safari_Karing.json` | Safari / Apple 服务 + Safari 常访境外站，走美国节点 | https://raw.githubusercontent.com/yizu2008/karing-rules/main/Safari_Karing.json |

## 在 Karing 里用

1. 新建自定义分流组，备注写 `Safari`，加 `Rule Set`，填上面 Safari 的 Raw 链接。
2. 回到 `分流规则`，把 `Safari` 组动作改成你的具体美国节点，不要选自动选择。
3. 回首页断开、重连，Safari 打开 `ip.sb` 验证是不是美国 IP。

## 格式

和 `Whatsapp_Karing.json` 同款：

```json
{
  "version": 2,
  "rules": [
    { "domain": ["..."] },
    { "domain_suffix": ["..."] },
    { "domain_keyword": ["..."] },
    { "ip_cidr": ["..."] }
  ]
}
```
