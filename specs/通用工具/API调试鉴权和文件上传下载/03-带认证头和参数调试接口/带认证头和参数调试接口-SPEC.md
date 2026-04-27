# 带认证头和参数调试接口 SPEC

- 明确区分 query、header 和 body
- 对 token 和认证头先检查拼写和前缀
- 返回异常时先回退到最小请求逐项加回
