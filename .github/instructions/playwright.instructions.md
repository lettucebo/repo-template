---
applyTo: "**/playwright*.{ts,js,config.ts,config.js}"
description: "Playwright 測試中正確顯示繁體中文字型的指引"
name: "Playwright 繁體中文字型支援"
---

# Playwright 繁體中文字型支援

## 必要需求

- CI/CD 環境（如 GitHub Actions）必須安裝繁體中文字型支援套件（如 Noto CJK 字型）
- Docker 環境同樣需要安裝中文字型套件

## Playwright 配置

設定 locale 為 `zh-TW`，時區為 `Asia/Taipei`