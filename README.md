
# olca2tidas

将 openLCA 导出的 JSON-LD 一键转换为 **TIDAS / eILCD** 风格 JSON（便于导入天工数据库）、并输出认证清单。    本工具已封装为 `pip` 可安装、带 CLI、支持日志输出。具体使用指南如下：


---

## 1) 安装

###Windows（PowerShell）
```
py -m pip install -U olca2tidas
```
###macOS / Linux
```
python3 -m pip install -U olca2tidas
```

或者从源码安装：

```bash
git clone https://github.com/Kirin-Ciao/olca2tidas.git
cd olca2tidas
pip install -e .
```

## 2) 快速开始

### 方式 A：使用包装后的命令 `olca2tidas`（推荐）
```bash
# Windows 示例（注意路径需要引号）
olca2tidas -- --src "E:\openLCA\tiangong\<your-file>" --out "E:\openLCA\tiangong\Result"

# 同时把控制台输出保存到日志文件：
olca2tidas --log-file logs/run-$(date +%Y%m%d-%H%M%S).log -- --src "C:\data\JSON-LD" --out "C:\data\Result"
```

> `--` 之后的参数将**原样转发**给您的转换脚本（位于 `olca2tidas.converter`）。    > 需要查看底层脚本的帮助时，运行： `olca2tidas -- --help`

### 方式 B：直接调用底层脚本（开发/调试）
```bash
python -m olca2tidas.converter --src "/path/to/JSON-LD" --out "/path/to/Result"
```

## 3) 常见参数

- `--log-file <path>`：将控制台输出同时写入该日志文件（wrapper 提供）。
- `--log-level {DEBUG,INFO,WARNING,ERROR}`：调整 wrapper 日志等级（默认 `INFO`）。
- `-- --help`：查看底层转换脚本自己的 `--help` 说明（由脚本的 `argparse` 提供）。

> 底层脚本支持参数（示例）：`--src`、`--out`、`--version`、`--edge_dir`、`--locale`、`--no-cert` 等。

## 4) 输出

转换完成后，会在输出目录生成：
- `data/flows/*.json`, `data/processes/*.json`, `data/lifecyclemodels/*.json`（覆盖保存后的 ILCD/TIDAS JSON）
- `convert_manifest.json`：包含转换数量、SHA256 校验与结构验证结果


## 5) 许可

MIT License © Qilin Cao
