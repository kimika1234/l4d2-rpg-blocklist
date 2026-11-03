# L4D2 RPG 服务器屏蔽名单

求生之路 2（L4D2）RPG / 技能 / 修仙类服务器屏蔽名单，**按 `IP:端口` 精确屏蔽**——同一个 IP 上同时存在正常服务器时，正常服不受影响。

本名单由 [橘服社区](https://kimika.bbroot.com) 长期维护，供 [BlockL4D2RPG 屏蔽工具](https://kimika.bbroot.com/download) 与任何自写脚本消费。

## 名单格式

```json
{
  "version": 1,
  "updated_at": "2026-11-03 08:00",
  "whitelist": ["103.91.210.16"],   // 永不屏蔽的自用/合作 IP（工具强制排除）
  "entries": [
    { "target": "1.2.3.4:27015", "note": "服务器名" },
    { "target": "5.6.7.8",       "note": "整 IP（该 IP 无正常服时才用）" }
  ]
}
```

`target` 支持：`ip:port`（推荐）/ `ip`（整 IP）/ CIDR / `1.2.3.*` 通配。

## 消费方式

- **一键工具（推荐玩家）**：Windows 防火墙出站 UDP 拦截，双击即用，从 155 或本仓库拉最新名单。
- **自写脚本**：直接 GET 本仓库的 `rpg-blocklist.json`（或国内镜像 `https://kimika.bbroot.com/jufu-dist/rpg-blocklist.json`）。

## 维护流程（社区维护者）

1. `python _seed_rpglist.py --apply` —— 用 Steam Web API 拉全量 L4D2 服务器，按 RPG 名称关键词（来自 [yxnan/block-l4d2-rpg-servers](https://github.com/yxnan/block-l4d2-rpg-servers)）匹配，输出草稿；自动排除白名单 IP 与「拒绝RPG/拒绝修仙」类否定式误伤。
2. 人工核对草稿 → 更新 `version` / `updated_at`。
3. 同时发布到：本仓库（`git push`）+ 155 服务器（`/var/www/jufu-dist/rpg-blocklist.json`）。

## 免责声明

- 名单基于服务器名称自动识别 + 人工抽查，可能存在个别误伤；如需申诉请在 issue 里留言。
- 屏蔽逻辑只影响本机出站连接，不涉及任何攻击性行为。
