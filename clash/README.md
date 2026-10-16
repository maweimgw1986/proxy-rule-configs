# Clash Verge 远程分流

远程配置：[clash-verge-98t-remote.yaml](clash-verge-98t-remote.yaml)

订阅地址：

```text
https://raw.githubusercontent.com/maweimgw1986/proxy-rule-configs/main/clash/clash-verge-98t-remote.yaml
```

这份配置沿用当前 98T、AI、Google、DMM、B 站、国内软件及国内直连分流。机场订阅只写在 Clash Verge 本机的**这张远程配置卡片的订阅扩展配置**中；公开仓库没有机场地址。独立导入机场订阅卡片不会自动合并到此配置。

## 首次使用

1. 在 Clash Verge 的「配置」中用上述地址添加远程配置。先保留原配置，暂不切换。
2. 右键新配置卡片，进入「编辑扩展配置」或「订阅扩展配置」，粘贴下面的示例。将两个 `url` 分别替换成自己的机场订阅地址；只用一个机场就删掉 `airport_b` 整段。`name` 和 `path` 不要与其他机场重复。
3. 保存扩展配置，更新这张远程配置卡片，再选中它。到「代理」查看「自动选择」「美国节点」「日本节点」等组是否出现真实节点；确认后再测试 ChatGPT、Gemini、DMM 与国内网站。

```yaml
proxy-providers:
  airport_a:
    type: http
    url: "https://example.invalid/replace-with-your-first-subscription"
    path: ./proxies/airport_a.yaml
    interval: 21600
    override:
      additional-prefix: "A | "
    health-check:
      enable: true
      url: http://www.gstatic.com/generate_204
      interval: 600
  airport_b:
    type: http
    url: "https://example.invalid/replace-with-your-second-subscription"
    path: ./proxies/airport_b.yaml
    interval: 21600
    override:
      additional-prefix: "B | "
    health-check:
      enable: true
      url: http://www.gstatic.com/generate_204
      interval: 600
```

## 后续维护

- **分流修改**：更新这张远程配置卡片，取得 GitHub 上的新版本。
- **添加机场**：只在本机扩展配置的 `proxy-providers` 下增加一段，使用不同名称、`path` 和节点前缀，保存并更新配置。
- **更换机场**：修改对应 `url`，保存并更新配置。
- **删除机场**：删除对应的完整段落，保存并更新配置；确认其他机场仍有可用节点。
- **安全**：真实订阅地址通常含凭据，不要写入本公开仓库、截图或发给他人。

远程配置中的「模板占位_勿选」和各测速组中的 `REJECT` 仅用于让未填写机场时配置可导入，不是可用节点。若地区组只显示 `REJECT`，请检查该地区是否有节点，以及机场订阅是否加载成功。用户原有的 Tailscale 代理端口设置保留在配置中；实际连通性仍需在设备上验证。
