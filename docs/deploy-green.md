# 绿色版（解压即用）使用教程 · v1.7.5

绿色版是把本地 Web 站点打成的便携压缩包：解压 → 启动 → 浏览器搜索。适合不想装 Docker、也不想当 AI Skill 用的同学。

## 下载

到仓库 [juicePans-web Releases](https://github.com/sxsxhhi/juicePans-web/releases) 下载：

`juicePans-v1.7.5-web-green.zip`

## Windows

1. 解压到任意文件夹
2. 确认已安装 **Python 3.8+**（安装时勾选 Add python.exe to PATH）
3. 双击 `start.bat`
4. 浏览器打开 `http://127.0.0.1:8765/`
5. 可展开「盘种与引擎」、打开「检验链接存活」；过慢可「终止」
6. 关掉黑色命令行窗口即停止服务

## macOS / Linux

```bash
unzip juicePans-v1.7.5-web-green.zip
cd juicePans-web-green   # 以实际解压目录名为准
bash start.sh
# 或: python3 server.py
```

浏览器访问 `http://127.0.0.1:8765/`。

## 以本机电脑为服务器（局域网其它设备访问）

让手机 / 平板 / 另一台电脑，在同一局域网通过浏览器使用本机上的果汁搜盘：

**地址格式：** `http://<电脑局域网IP>:8765/`

### 1. 在「服务器电脑」上用 0.0.0.0 启动

必须监听所有网卡；仅 `127.0.0.1` 时其它设备无法访问。

Windows PowerShell（在解压目录）：

```powershell
$env:JUICEPANS_HOST="0.0.0.0"
$env:JUICEPANS_PORT="8765"
python server.py
```

查本机 IPv4：运行 `ipconfig`（Windows）或 `ip addr` / `hostname -I`（Linux），查看当前联网适配器的 IPv4。

macOS / Linux：

```bash
export JUICEPANS_HOST=0.0.0.0
export JUICEPANS_PORT=8765
python3 server.py
```

### 2. 其它设备浏览器打开

`http://<电脑局域网IP>:8765/`

### 注意

- 防火墙需放行入站 TCP `8765`（专用网络）
- 设备需同一局域网；部分「访客 Wi‑Fi」有客户端隔离
- 停止 `server.py` / 关闭窗口后，局域网也无法再访问
- 双击 `start.bat` 通常只服务本机；局域网请用上面的环境变量启动

## 和 Skill / Docker 的区别

| 方式 | 适合谁 | 入口 |
|------|--------|------|
| AI Skill | 对话里安装 skill / CLI | [juicePans](https://github.com/sxsxhhi/juicePans) |
| 绿色版 Web | 浏览器本地搜 | Releases 的 `*-web-green.zip` |
| Docker | 服务器 / NAS 7×24 | [deploy-docker.md](./deploy-docker.md) |
| 源码本地跑 | 开发调试 | [deploy-local.md](./deploy-local.md) |

架构与可选 PanSou 说明见 [ARCHITECTURE.md](./ARCHITECTURE.md)。

## 常见问题

- **start.bat 闪退**：未安装 Python 或未加入 PATH
- **端口被占用**：设置 `JUICEPANS_PORT` 换端口
- **盘搜偏慢**：可只勾选小云 + 海搜；或配置 `PANSOU_URL` 指向自建 PanSou
- **只要转存**：本绿色版只搜索展示，不转存
