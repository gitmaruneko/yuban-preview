# 育伴開發預覽站

預覽網址：https://gitmaruneko.github.io/yuban-preview/
正式網址：https://gitmaruneko.github.io/yuban/

## 修改與發布

1. 在 `gitmaruneko/yuban` 的 `develop` 分支修改並推送程式碼。
2. 本 repository 每 10 分鐘排程檢查一次來源版本；GitHub 排程可能延遲。若版本未變更則跳過部署。
3. 有新版時執行 Python、JavaScript 測試與資源索引驗證，全部通過才發布 `website/`。
4. 需要立即更新時，開啟 Actions → Deploy develop preview → Run workflow，使用本 repository 的 `main`；來源仍固定為 `yuban` 的 `develop`。
5. 確認預覽後，在 `yuban` 建立 base `main`、compare `develop` 的 Pull Request，合併後由原有正式部署流程更新正式站。

本 repository 只維護預覽工作流程，網站原始碼仍在 `yuban`。不需要個人存取權杖或跨 repository 寫入金鑰；工作流程讀取公開來源並只部署本 repository 的 Pages。

## 預覽識別

預覽頁顯示 develop 與來源 commit 的前七碼，並提供回到正式站的連結。`preview-version.txt` 記錄完整來源 commit。預覽內容加入 noindex 標記與 robots.txt；這不是存取控制，網址仍公開可見。

測試失敗時不發布，保留先前預覽。部署後檢查首頁、學習素材頁、資源 JSON 與版本檔；失敗會在 Actions 標示，沒有自動回復機制。正式站不受此流程影響。

GitHub 可能在公開 repository 長期沒有活動後停用排程（目前為 60 天）；必要時到 Actions 重新啟用或手動執行。
