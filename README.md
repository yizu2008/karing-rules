# karing-rules

Karing 远程分流规则集（sing-box source 格式，`version: 2`），可在 Karing 里当 Rule Set 线上导入。

原则：规则文件里只写域名，不写死节点。节点跟你所选节点走——在 Karing 里把各组的动作都设成「当前选择 / currentSelected」，不要设成某个具体节点。以后在首页换节点，各组就都跟着换。

## 规则

| 文件 | 说明 | 条数 | Raw 链接 |
| --- | --- | --- | --- |
| `Safari_Karing.json` | Safari / Apple 服务 + Safari 常访境外站 + Muse 后端 | 65 | https://raw.githubusercontent.com/yizu2008/karing-rules/main/Safari_Karing.json |
| `Whatsapp_Karing.json` | WhatsApp 服务域名/IP + Muse 后端虚拟机 | 33 | https://raw.githubusercontent.com/yizu2008/karing-rules/main/Whatsapp_Karing.json |
| `Muse_Karing.json` | Muse / Meta AI + 后端虚拟机 | 11 | https://raw.githubusercontent.com/yizu2008/karing-rules/main/Muse_Karing.json |
| `follow-selected-diversion.json` | 直接导入的分流规则，全部 outbound currentSelected，跟随所选节点 | 4 条规则 | https://raw.githubusercontent.com/yizu2008/karing-rules/main/follow-selected-diversion.json |

## 在 Karing 里用

### Rule Set 方式（Safari / WhatsApp / Muse）

1. 新建自定义分流组，备注写 `Safari` / `WhatsApp` / `Muse`，加 `Rule Set`，填上面对应的 Raw 链接。
2. 回到 `分流规则`，把对应组动作改成「当前选择 / currentSelected」，不要选具体节点，也不要选自动选择。
3. 回首页断开、重连，验证是否生效。改规则后要在 Rule Set 里点更新/刷新，再断开重连。

### 直接导入方式（跟随所选，防漏网）

1. `设置 → 分流 → 分流规则 → 编辑 → 导入`，选 `follow-selected-diversion.json` 的 Raw 链接导入。
2. 把它移到最上面，里面 3 条原来是 Muse 后端、Muse、WhatsApp，另有 1 条 Safari，全部都是 `currentSelected`。
3. 断开、重连，`hatch.metaaivm.com`、`muse.ai`、`api.whatsapp.net` 这些就都跟你首页选的节点走了，不会再掉到 `final` 自动选择。

## 格式

Rule Set 文件：

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

直接导入文件：

```json
{
  "rules": [
    { "name": "...", "outbound": "currentSelected", "switch": true, "or": true, "domain_suffix": ["..."] }
  ]
}
```
