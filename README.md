# CloudPuff-Vite
本專案使用 **Vite + Bootstrap 5 + SCSS + EJS** 作為前端開發框架，並整合 GitHub Pages 進行自動化部署。

---

## Node.js 版本
- 專案的 Node.js 版本需為 v18 以上  
- 查看自己版本指令：`node -v`

---

## 📌 指令列表
```bash
npm install          # 安裝專案所需套件（第一次下載專案必須執行）
npm run dev          # 啟動開發模式
# 若沒有自動開啟瀏覽器，可手動輸入：
# http://localhost:5173/<專案名稱>/pages/index.html

npm run build        # 編譯專案，輸出靜態檔案到 docs/（不會開啟瀏覽器）
npm run deploy       # 自動化部署到 GitHub Pages
```

---

## 📂 專案結構
```
CloudPuff-Vite/
│── README.md                 # 專案說明文件
│── package.json              # 專案設定與套件資訊
│── vite.config.js            # Vite 設定檔
│── docs/                     # build 出來的靜態檔 (部署用)
│── .gitignore                # Git 忽略清單
│
├─ assets/                    # 靜態資源
│   ├─ images/                # 圖片資源
│   │    ├─ git-branch.png
│   │    └─ deploy-flow.png
│   │
│   └─ scss/                  # SCSS 樣式
│        ├─ _variables.scss   # 全域變數
│        ├─ _header.scss      # 頁首樣式
│        ├─ _footer.scss      # 頁尾樣式
│        ├─ _product.scss     # 商品列表樣式
│        ├─ _productdetail.scss # 商品詳情樣式
│        └─ _all.scss         # 主入口 (匯入所有 scss)
│
├─ layout/                    # ejs 模板
│   ├─ header.ejs             # 頁首區塊
│   └─ footer.ejs             # 頁尾區塊
│
├─ pages/                     # 各獨立頁面
│   ├─ index.html             # 首頁
│   ├─ product.html           # 商品列表
│   ├─ productdetail.html     # 商品詳情
│   ├─ cart.html              # 購物車
│   ├─ pay.html               # 結帳 / 付款
│   ├─ purchase.html          # 購買結果
│   ├─ login.html             # 登入
│   ├─ register.html          # 註冊
│   └─ account.html           # 個人帳號 / 資料頁 / 購買清單
│
├─ src/                       # JavaScript 原始碼
│   └─ main.js                # 主程式入口
```

---

## 📥 專案下載
```bash
cd /d
git clone https://github.com/Rubio83/CloudPuff-Vite.git
```

---

## 📌 開發上線部署流程說明
![Git Branch Flow](./assets/images/git-branch.png)  
![Deploy Flow](./assets/images/deploy-flow.png)

---

## 🚀 開發上線部署流程 (feature → develop → main → GitHub Pages/Server)

### 1. 開發流程（feature → develop）
```bash
# 先回到 develop 並取新
git branch                       # 檢查目前分支所屬
git checkout develop
git pull origin develop

# 建立自己的功能分支 (-b = 建立新分支)
git checkout -b feature/<task>

# 在 feature 分支開發並提交
git add .
git commit -m "feat: <summary>"
git push -u origin feature/<task>  # 第一次用 -u 建立追蹤，之後可直接 git push

# 功能完成後 → 合併至 develop
git checkout develop
git pull origin develop            # 先同步最新版本，降低衝突機率
git merge feature/<task>
git push origin develop

# Double check develop 確保合併正常
git pull origin develop            # 拉到本地確認測試 OK

# 清理 feature 分支（可選）
git branch -d feature/<task>               # 刪掉本地
git push origin --delete feature/<task>    # 刪掉遠端
```

---

### 2. 上線流程（develop → main）
```bash
# 切換到 main
git checkout main
git pull origin main

# 合併 develop
git merge origin/develop -m "release: merge develop into main"
git push origin main
```

---

### 3. 部署流程（main → GitHub Pages）
```bash
# 建置，輸出到 docs/
npm run build

# 提交 docs 到 main
git add docs
git commit -m "build(docs): publish"
git push origin main
```
