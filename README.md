# clash-rules-academic

用于在 Clash / 其他分流工具中对学术网站与服务进行分类的规则集集合，便于根据站点属性选择 DIRECT（直连）或 proxy（代理）策略，从而提高访问稳定性与速度。

## 规则集说明

- AcademicCN  
  收录在国内可以直接访问的学术站点与服务（例如一些国内期刊、镜像站点、学校内网服务等）。推荐使用 `DIRECT`，因为走代理可能导致延迟增加或连接不稳定。

- AcademicProxy  
  收录需要通过代理才能可靠访问的学术站点与服务（如部分国外学术网站或受限资源）。推荐使用 `proxy`（替换为你的代理策略名），以确保访问速度和稳定性。

- AcademicDatabase  
  收录付费或机构订阅类学术数据库（例如学校/图书馆购买的数据库）。  
  - 如果你的机构已订阅并在同一网络环境（如 VPN / 校内网）下，建议设置为 `DIRECT`，以确保机构认证与访问策略正常生效。  
  - 如果未通过机构订阅访问或机构网络有访问限制，使用 `proxy` 可能更快。具体取舍请根据个人/机构实际情况决定。

- AcademicGlobal  
  收录在国内外均可访问的学术站点（对访问方式影响不大）。可以统一按个人偏好或策略设置为 `DIRECT` 或 `proxy`。

## 使用建议

- 将不同规则集映射到不同的策略（例如：`DIRECT`、`Proxy`、或你的自定义代理组），根据网络和权限需求灵活调整。
- 优先考虑机构订阅与认证需求：对需机构认证的资源优先直连，避免走代理导致无法通过认证或资源被误判。
- 若遇到某个站点访问速度慢或不稳定，可临时切换该站点到另一策略并观察效果，必要时将其加入本地自定义规则。

## 示例（Clash 配置片段）

下面是一个示例，演示如何在 Clash 的 rule 中引用这些规则集（请根据实际规则名与策略名修改）：

```yaml
rules:
  # AcademicCN 中的域名走直连
  - RULE-SET,AcademicCN,DIRECT

  # AcademicProxy 中的域名走代理
  - RULE-SET,AcademicProxy,Proxy

  # AcademicDatabase 根据是否在校园网/机构网络切换
  - RULE-SET,AcademicDatabase,DIRECT

  # AcademicGlobal 统一设置为直连（或改为 Proxy）
  - RULE-SET,AcademicGlobal,DIRECT

  # 其他默认规则
  - GEOIP,cn,DIRECT
  - MATCH,Proxy
