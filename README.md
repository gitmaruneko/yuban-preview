# 育伴開發預覽站

預覽網址：https://gitmaruneko.github.io/yuban-preview/
正式網址：https://gitmaruneko.github.io/yuban/

## 修改與發布

1. 從 `gitmaruneko/yuban` 的最新 `main` 建立 `feature/*` 或 `fix/*` 短期分支，修改後推送該分支。
2. 開啟 Actions → Deploy preview → Run workflow，在 `source_ref` 輸入完整分支名稱，例如 `feature/search-improvement`。
3. 工作流程會執行 Python、JavaScript 測試與資源索引驗證，全部通過才發布 `website/`。
4. 在預覽網址確認結果後，從短期分支建立 targeting `main` 的 Pull Request。
5. Pull Request 檢查通過並合併後，由 `yuban` 的正式部署流程更新正式站；最後刪除短期分支。

本 repository 只維護預覽工作流程，網站原始碼仍在 `yuban`。不需要個人存取權杖或跨 repository 寫入金鑰；工作流程讀取公開來源並只部署本 repository 的 Pages。

## 預覽識別

預覽頁顯示來源分支與 commit 的前七碼，並提供回到正式站的連結。`preview-ref.txt` 記錄來源 ref，`preview-version.txt` 記錄完整來源 commit。預覽內容加入 noindex 標記與 robots.txt；這不是存取控制，網址仍公開可見。

共用預覽網址永遠顯示最近一次成功部署的來源分支。測試或來源 checkout 失敗時不發布，保留先前預覽。部署後檢查首頁、學習素材頁、資源 JSON 與版本檔；失敗會在 Actions 標示，沒有自動回復機制。正式站不受此流程影響。

刪除短期分支不會清除已發布的預覽；下一次成功執行工作流程時才會覆蓋。
