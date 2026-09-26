# 本地源码运行 · v1.7.5

```bash
cd web
python3 server.py
```

浏览器：`http://127.0.0.1:8765/`

局域网访问（本机当服务器）：

```bash
export JUICEPANS_HOST=0.0.0.0
export JUICEPANS_PORT=8765
python3 server.py
```

其它设备打开：`http://<电脑局域网IP>:8765/`

更完整的绿色版/局域网说明见 [deploy-green.md](./deploy-green.md)。引擎与 PanSou 见 [ARCHITECTURE.md](./ARCHITECTURE.md)。
