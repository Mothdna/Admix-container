# 祖源计算器（Admix Container）

版本：**v1.0.46**

放进计算器包（DIYDodecad 风格 `.zip`，如 E11 / K47）和原始基因型数据，在浏览器本地跑出祖源成分比例。**所有计算都在本机浏览器内完成，文件不上传、不经过服务器。** 单文件自包含，图标已内联，无外部资源依赖。

## 目录结构

```
admix-container/
├── index.html              # 单文件应用入口（HTML + CSS + JS + 图标全部内联）
├── .nojekyll               # 禁止 Jekyll 处理，保证静态资源原样发布
└── README.md
```

## 支持的输入

- 计算器包：DIYDodecad 风格 `.zip`（含频率矩阵、等位基因、成分名），如 E11、K47、K8、K12。
- 原始数据：PLINK `.bed+.bim+.fam` / `.ped+.map`、EIGENSTRAT `.geno+.snp+.ind`、23andMe / WeGene `.txt`、VCF（含 `.vcf.gz`），支持打包成 `.zip` 批量导入。

## 本地预览

直接用浏览器打开 `index.html` 即可；如需本地静态服务器：

```bash
python3 -m http.server 8080
# 浏览器访问 http://localhost:8080/
```

## 上架 GitHub Pages

1. 在 GitHub 新建一个**公开**仓库（私有仓库需要 Pro 套餐才能用 Pages），例如 `admix-container`。
2. 把 `index.html`、`.nojekyll`、`README.md` 上传到仓库根目录，分支用 `main`。本版本无 `assets/` 目录，图标已内联进 HTML。
3. 仓库 **Settings → Pages**：
   - **Source** 选 `Deploy from a branch`；
   - **Branch** 选 `main`，目录选 `/ (root)`，保存。
4. 等待 1–10 分钟，访问：

   ```
   https://<你的用户名>.github.io/<仓库名>/
   ```

5. （可选）把 `index.html` 里 `<meta property="og:url">` 的占位地址 `https://YOUR_USERNAME.github.io/YOUR_REPO/` 改成上面的实际地址。

### 后续更新

替换仓库根目录的 `index.html` 后提交即可，Pages 会自动重新发布；版本号在页面标题、右上角标签、页脚和诊断内置常量四处保持一致。

## 压测结论（v1.0.46）

- 中端安卓等效环境（CPU 4× 节流）20 份样本整批跑完：20/20 成功、0 失败、0 零命中，无页面报错、无横向溢出、结果条形与百分比对齐。
- 计算阶段偶发百毫秒级主线程停顿（完成结果回传后批量刷新卡片时），交互阶段（滚动、切换视图、展开详情、搜索）无掉帧；一次性数据解压/解码阶段有秒级主线程占用，属正常载入开销。
- 浏览器内存有限，超大批量样本请分批导入；结果可导出 Excel。

## 常见问题

- **诊断包里版本号显示旧版**：确认仓库根目录的 `index.html` 是最新构建；页脚、右上角标签、诊断内置版本号应一致。
- 纯静态页面，无后端、无数据库、无账号体系。
- 成分比例为固定参考面板下的监督式混合估计，仅作祖源参考。
