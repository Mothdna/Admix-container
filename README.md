# 祖源计算器（Admix Container）

版本：**v1.0.45**

放进计算器包（DIYDodecad 风格 `.zip`，如 E11 / K47）和原始基因型数据，在浏览器本地跑出祖源成分比例。**所有计算都在本机浏览器内完成，文件不上传、不经过服务器。**

## 目录结构

```
admix-container/
├── index.html              # 单文件应用入口（HTML + CSS + JS 全部内联）
├── assets/
│   └── share-icon.png      # 分享/图标
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
2. 把本目录内的全部文件（`index.html`、`assets/`、`.nojekyll`、`README.md`）上传到仓库根目录，分支用 `main`。
3. 仓库 **Settings → Pages**：
   - **Source** 选 `Deploy from a branch`；
   - **Branch** 选 `main`，目录选 `/ (root)`，保存。
4. 等待 1–10 分钟，访问：

   ```
   https://<你的用户名>.github.io/<仓库名>/
   ```

5. （可选）把 `index.html` 里 `<meta property="og:url">` 的占位地址 `https://YOUR_USERNAME.github.io/YOUR_REPO/` 改成上面的实际地址。

### 后续更新

替换仓库根目录的 `index.html`（和 `assets/`）后提交即可，Pages 会自动重新发布；版本号在页面标题、右上角标签和脚本内三处保持一致。

## 说明

- 纯静态页面，无后端、无数据库、无账号体系。
- 浏览器内存有限，超大批量样本请分批导入；结果可导出 Excel。
- 成分比例为固定参考面板下的监督式混合估计，仅作祖源参考。
