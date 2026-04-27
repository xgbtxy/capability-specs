# 筛出异常连接重传和错误

## 目标

筛这些信号：

- TCP retransmission
- RST
- 异常关闭
- 时间上反复抖动的会话
