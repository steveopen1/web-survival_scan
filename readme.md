# 一、工具概述
web-SurvivalScan-Magic_Plus 是一款强大的 Web 存活扫描工具，采用 Python 编写，能够帮助用户快速检测目标 URL 的存活状态，并提供详细的扫描结果和报告。它支持多种 HTTP 请求方法，具备智能的请求切换机制，以及丰富的日志和报告生成功能。
# 二、安装与依赖
## （一）安装 Python
确保你的系统已安装 Python 3。如果未安装，可以从[Python 官方网站](https://www.python.org/downloads/)下载并安装。
## （二）安装依赖库
- 工具运行依赖一些 Python 库，可通过以下命令安装：

```python
pip install beautifulsoup4 requests tqdm termcolor argparse
```
## （三）获取工具
你可以从项目的 GitHub 仓库[下载](https://github.com/yourusername/web-SurvivalScan-Magic_Plus)源代码，或直接克隆仓库：
```bash
git clone https://github.com/yourusername/web-SurvivalScan-Magic_Plus.git
```
# 三、使用方法
## （一）准备目标 URL 文件
在运行工具前，需要准备一个包含目标 URL 的文本文件，每行一个 URL。例如，创建一个名为target_urls.txt的文件，内容如下：
```plaintext
http://example1.com
https://example2.net
http://sub.example3.org
```
## （二）基本命令行参数
- 工具通过命令行参数进行配置，主要参数如下：
-l, --list：指定包含目标 URL 的输入文件，这是必填参数。
-p, --proxy：指定代理服务器的 IP 和端口，格式为IP:port，如127.0.0.1:8080。
-H, --user-agent：指定用于 HTTP 请求的 User - Agent。如果不指定，工具会使用默认的 User - Agent 列表。
-X, --method：指定 HTTP 请求方法，可选GET或POST，默认值为GET。
-r, --redirect：指定是否跟踪 302 重定向，可选yes或no，默认值为no。
# （三）运行示例
- 简单扫描：使用默认设置，仅指定目标 URL 文件进行扫描。
```bash
python web-SurvivalScan-Magic_Plus.py -l target_urls.txt
```
- 使用代理扫描：指定代理服务器进行扫描。
```bash
python web-SurvivalScan-Magic_Plus.py -l target_urls.txt -p 127.0.0.1:8080
```
- 自定义 User - Agent 和请求方法：指定自定义 User - Agent 和 POST 请求方法。
```bash
python web-SurvivalScan-Magic_Plus.py -l target_urls.txt -H "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36" -X POST
```
- 跟踪重定向扫描：指定跟踪 302 重定向。
```bash:
python web-SurvivalScan-Magic_Plus.py -l target_urls.txt -r yes
```
# 四、扫描结果查看
## （一）控制台输出
扫描过程中，工具会在控制台实时输出扫描结果，不同状态的 URL 会以不同颜色显示：
存活的 URL（状态码为 200 或 403）以红色显示，包含状态码、URL、页面长度、网页标题和响应字节数等信息。
无法访问的 URL 以黄色显示，包含状态码和 URL。
被目标积极拒绝请求的 URL 以洋红色显示。
## （二）结果文件
- 扫描完成后，会在当前目录下生成一个result文件夹，包含以下文件：
web-SurvivalScan_report.html：HTML 格式的扫描报告，包含所有扫描结果的详细信息，URL 为可点击链接，方便直接访问查看。
200.txt：保存状态码为 200 的 URL。
403.txt：保存状态码为 403 的 URL。
output.txt：保存所有存活的 URL（状态码为 200 或 403）。
outerror.txt：保存扫描过程中出现错误的 URL。
.data/report.json：以 JSON 格式保存的扫描结果数据，便于后续数据分析和处理。
# 五、注意事项
- 代理设置：使用代理时，确保代理服务器可用且配置正确。工具会自动检测代理的可用性，如果代理不可用，扫描将无法正常进行。
字符编码问题：在处理结果文件时，可能会遇到字符编码问题。工具在读取和写入文件时尝试了多种常见编码格式，但如果仍然出现编码错误，请手动检查和转换文件编码。
- 请求频率：避免对目标服务器发送过于频繁的请求，以免造成服务器负载过高或被目标服务器封禁 IP。如果需要扫描大量 URL，建议适当调整扫描速度或使用代理池。
