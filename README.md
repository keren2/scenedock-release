# SceneDock Release（安装包仓库）

这个仓库专门存放 SceneDock 的 Windows 安装包。帽子云（maozi.io）从这个 GitHub 仓库自动拉取文件，通过国内 CDN 分发，用户最终下载走的是帽子云 CDN，不是 GitHub。

## 目录结构

```
scenedock-release/
├── index.html                              # 占位首页，让帽子云识别为静态网站
├── README.md                               # 本文件
└── SceneDock-x.x.x-win-x64-setup.exe       # Windows 安装包（版本号按实际改）
```

当前直链格式：
```
https://scenedock-10i3z3fb.maozi.io/SceneDock-x.x.x-win-x64-setup.exe
```

## 更新安装包（版本号变了，比如 0.3.0 → 0.4.0）

在 PowerShell 执行：

```powershell
# 1. 进入仓库目录
cd E:\scenedock-release

# 2. 删除旧安装包
Remove-Item SceneDock-0.3.0-win-x64-setup.exe

# 3. 把新安装包复制进来（把下面文件名改成实际的新文件名）
Copy-Item "你打包输出的路径\SceneDock-0.4.0-win-x64-setup.exe" .

# 4. 提交并推送
git add .
git commit -m "v0.4.0 win-x64 installer"
git push
```

push 成功后，帽子云会在 1-2 分钟内自动重新部署，新直链立刻生效，无需登录帽子云手动操作。

## 注意事项

- 安装包命名必须和直链里的文件名一致，建议格式：`SceneDock-主版本.次版本.修订-win-x64-setup.exe`
- GitHub 单文件硬限制 100MB，当前 64MB 远低于限制，正常 push 即可（push 时会有超过 50MB 的 warning，忽略即可）。
- 不要删除 `index.html`，否则帽子云会报"未知服务类型：非 static 应用"。
- 更新完安装包后，还需要去 `E:\SceneDockWeb\` 改网页上的版本号文案和下载链接，详见那边的 README。
