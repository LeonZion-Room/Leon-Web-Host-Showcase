# Leon-Web-Host-Showcase

Leon-Web-Host 托管 21 个项目的**静态只读镜像**官方仓库。页面为展示站 + Wiki 使用说明的静态快照，经 GitHub → Cloudflare Pages 对外发布。

## 在线地址

待接入 Cloudflare Pages 后更新。

## 结构

```
index.html            21 项目分组导航首页
<project>/index.html  各项目展示站（外网跳转按钮已烧录）
<project>/wiki/       Wiki 使用说明预渲染静态页
.export-info.json     导出清单（时间戳/项目/wiki 页数）
```

## 重新生成

70 机（TK-Server，192.168.11.70）执行：

```bash
cd /home/leonzion/Desktop/Leon-TK-Station/Leon-Web-Host
venv/bin/python showcase_export.py /tmp/showcase-deploy
rsync -a --delete /tmp/showcase-deploy/ /tmp/showcase-repo/
cd /tmp/showcase-repo
git add -A && git commit -m "deploy: $(date +%Y-%m-%d %H:%M)" && git push origin main
```

## 说明

- 自动剔除：meta.json（含项目 Token）、ACCESS.md、备份/版本残留文件
- runtime 占位符（{{ rt.* }}）重跑时冻结为当时快照
- 原平台（编辑/管理/实时）仍运行于 http://119.145.17.34:5070/