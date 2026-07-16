# 建立持久 SSH 通道和 crawlerctl 入口

用一个长期存活的 SSH 本地转发消除每次调用的握手开销，再用 crawlerctl 把连接、鉴权、常用任务和原生 API 透传收敛成稳定入口。

这一步不需要 MCP。CLI 负责确定性执行，后续 Skill 只负责让 AI 正确选择命令。
