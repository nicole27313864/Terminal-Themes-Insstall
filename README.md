<!-- markdownlint-disable -->
<p align="center">
  <img
    width="400"
    src="https://raw.githubusercontent.com/jandedobbeleer/oh-my-posh/main/website/static/img/logo.png"
    alt="Oh My Posh – Prompt theme engine for any shell"
  />
</p>

<!-- markdownlint-enable -->

這是基於【[Oh My Posh](https://ohmyposh.dev/)】開源項目的個人安裝筆記。
個人安裝的用意是修改 [Windows](https://www.microsoft.com/zh-tw/windows)、[VScode](https://code.visualstudio.com/) 的 [Terminal](https://apps.microsoft.com/detail/windows-terminal/9N0DX20HK701)主題。
若為其他作業系統可參考 [Oh My Posh](https://ohmyposh.dev/) 官方的[Docs](https://ohmyposh.dev/docs/)。

## Preparatory work | 前置作業

### 安裝新版 [Windows Terminal](https://apps.microsoft.com/detail/windows-terminal/9N0DX20HK701) 終端機
* 微軟載點: https://apps.microsoft.com/detail/windows-terminal/9N0DX20HK701

#### 安裝新版  [PowerShell7](https://learn.microsoft.com/zh-tw/powershell/scripting/install/installing-powershell-on-windows) 紀錄當下版本【PowerShell-7.3.8】;
* 安裝路徑默認 "C:\Program Files\PowerShell\" 以利後續VScode選擇終端機。
* 微軟載點: https://learn.microsoft.com/zh-tw/powershell/scripting/install/installing-powershell-on-windows
* GitHub載點: https://github.com/PowerShell/PowerShell/releases/tag
### 安裝 [FiraCode Nerd Font](https://www.nerdfonts.com/font-downloads) 字體。
* NerdFonts載點: https://www.nerdfonts.com/font-downloads
---
#### 先設置終端機的字體
1. 開啟裝好的終端機(順檢查PowerShell版本為新) > 下拉選項 > 【設定】
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/92d713e8-7308-4091-8b61-6ffeec5e8cee)
2. 在左側列表找到並點選新的 PowerShell > 在右側下滑找到【其他設定】並點選進入【外觀】選項
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/635c1ae8-6cd6-48a8-bd65-cf7e6a36e705)
3. 設置字體 "FiraCode Nerd Font" 並儲存。字體選沒有Mono的，帶Mono的icon顯示會比較小。
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/83d6d093-6338-420c-ada4-040ae295f2a8)

## Installation | 安裝
### Step-1 開始安裝 OhMyPosh
開啟 PowerShell 並執行以下命令：
```
winget install JanDeDobbeleer.OhMyPosh -s winget
```
這會安裝一些東西：
* `oh-my-posh.exe` - Windows執行檔
* `themes`- 最新的 Oh My Posh[主題](https://ohmyposh.dev/docs/themes)

預期安裝完成結果: (如下圖)
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/57f54346-2ef2-496d-8e6d-5ab57c312bf1)

順利安裝完成後，為了確保加載`PATH` 環境變數，請重新開啟 PowerShell。

### Step-2 驗證功能加載正常、更新套件、安裝套件
在 PowerShell 輸入以下命令驗證是否正常
```
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\montys.omp.json" | Invoke-Expression
```
預期結果
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/dd2d8e2f-b448-47b3-b6b8-db1c904d7138)


在 PowerShell 依序輸入以下命令安裝/更新套件
若沒有在使用Git可免裝第二項`posh-git`
```=
Install-Module PSReadLine -Force
Install-Module posh-git -Force
Install-Module Terminal-icons -Force
```

在 PowerShell 依序輸入以下命令驗證 Terminal-icons 套件
預期輸入第一遍`ls`成功顯示當前路徑下文件/檔案
預期輸入第二遍`ls`成功顯示當前路徑下文件/檔案，且Name欄位成功顯示icon圖示
```=
ls
Import-Module Terminal-icons
ls
```

在 PowerShell 輸入以下命，看OhMyPosh主題
```
Get-PoshThemes
```
上面都會有 Theme: 主題的名稱，找到喜歡的並再次輸入以下命令找到想替換的主題
※請將`montys.omp.json `代碼中的`montys`替換為要看的Theme主題
```
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\montys.omp.json" | Invoke-Expression
```

### Step-3 找到要替換的主題後，開始設置環境
※若不設置每次都需要重新加載一遍OhMyPosh主題
先在 PowerShell 輸入以下命令，確保創建 `Microsoft.PowerShell_profile.ps1` 檔案
```
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
```
若電腦有裝VScode的話則在 PowerShell 輸入以下命令後會開啟一個名為 `Microsoft.PowerShell_profile.ps1` 檔案
```
code $PROFILE
```
若沒有VScode則在 PowerShell 輸入以下命令
```
notepad $PROFILE
```

並在 `Microsoft.PowerShell_profile.ps1` 檔案中輸入以下內容並保存關閉
檔案保存關閉後重新開啟 PowerShell 確認是否正常。
若沒有在使用Git 該段`Import-Module posh-git`可移除
```
# Improt-Module
Import-Module Terminal-icons
Import-Module posh-git #若無使用Git該段可移除

# PSReadLine
Set-PSReadLineOption -PredictionSource History
Set-PSReadLineOption -PredictionViewStyle InLineView

# oh-my-posh
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\montys.omp.json" | Invoke-Expression

# Variable
SET-VARIABLE ll ls
```

最後至VScode開啟終端機查看是否為修改後的
若不是可在VScode `CTRL`+`SHIFT`+`P` 輸入 `Terminal Select Default Profile`
![image](https://github.com/nicole27313864/Terminal-Themes-Insstall/assets/39577035/0facaef2-2136-48e2-9347-49dd6e0ef13f)

或在Setting.json中增加以下代碼
```
"terminal.integrated.defaultProfile.windows": "PowerShell",
```
若終端機主題加載正常但icon顯示亂碼，則在設置終端機的字體
Setting.json中增加以下代碼
```
"terminal.integrated.fontFamily": "'FiraCode Nerd Font','微軟正黑體'"
```
---
