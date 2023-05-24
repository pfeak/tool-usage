# Prometheus 搭建与使用

Github：https://github.com/prometheus/prometheus

Github Release：https://github.com/prometheus/prometheus/releases

## 安装与使用

1. 在 Github Release 页面下载对应架构版本 prometheus 压缩包并解压
2. cd 到解压后根目录
3. 执行 `./prometheus --config.file ./prometheus.yml`
4. 访问 `0.0.0.0:9090` 可以看到 prometheus 已经运行
5. 点击 Status -> Targets 可以看到已监测目标，访问 `[http://localhost:9090/metrics]` 可查看指标

>可以在 [Prometheus exporter](http://www.coderdocument.com/docs/prometheus/v2.14/instrumenting/exporters_and_integrations.html) 找到一些三方指标 exporter。