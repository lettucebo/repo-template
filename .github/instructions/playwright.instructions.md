---
applyTo: "**/playwright*.{ts,js,config.ts,config.js}"
description: "Playwright 測試中正確顯示繁體中文字型的指引"
name: "Playwright 繁體中文字型支援"
---

# Playwright 繁體中文字型支援

當使用 Playwright 進行截圖測試時，請確保能正確顯示繁體中文字型。

## 在 CI/CD 環境中的設定

在 GitHub Actions 或其他 CI 環境中執行 Playwright 測試時，需要安裝中文字型：

```yaml
- name: Install Chinese fonts
  run: |
    sudo apt-get update
    sudo apt-get install -y fonts-noto-cjk fonts-noto-cjk-extra
```

## 在 Playwright 配置中指定字型

在 `playwright.config.ts` 或測試文件中，可以這樣設定：

```typescript
import { defineConfig } from '@playwright/test';

export default defineConfig({
  use: {
    // 設定中文字型
    locale: 'zh-TW',
    timezoneId: 'Asia/Taipei',
    // 確保截圖時使用系統字型
    screenshot: 'only-on-failure',
  },
});
```

## Docker 環境中的設定

如果在 Docker 容器中執行，請在 Dockerfile 中加入：

```dockerfile
RUN apt-get update && apt-get install -y \
    fonts-noto-cjk \
    fonts-noto-cjk-extra \
    && rm -rf /var/lib/apt/lists/*
```

## 測試前安裝字型

在執行 Playwright 測試之前，始終確保：
1. 安裝 `fonts-noto-cjk` 或 `fonts-noto-cjk-extra` 套件
2. 設定正確的 locale (`zh-TW`)
3. 在截圖前確認字型已載入

## 範例：完整的 GitHub Actions Workflow

```yaml
- name: Setup Playwright
  run: |
    sudo apt-get update
    sudo apt-get install -y fonts-noto-cjk fonts-noto-cjk-extra
    npx playwright install --with-deps

- name: Run Playwright tests
  run: npm run test:e2e
```

## 注意事項

- Noto Sans CJK 是 Google 開發的開源字型，支援繁體中文、簡體中文、日文和韓文
- 在本地開發時，macOS 和 Windows 通常已經包含中文字型，但 Linux 環境需要額外安裝
- 使用 Google Fonts 時，可以透過 `fonts.googleapis.com` 和 `fonts.gstatic.com` 載入中文字型
