## Windows Terminal で Git Bash を使えるように設定する

### 事前インストール

Windows Terminal と Git は、事前にインストールしておく。

``` console
winget install -e --id Microsoft.WindowsTerminal
```

``` console
winget install -e --id Git.Git
```

### GUID を生成する

Powershell で次のコマンドを実行して GUID を生成する。

``` console
[Guid]::NewGuid()
```

`実行結果`
``` console
Guid
----
00000000-0000-0000-0000-000000000000
```

### Windows Terminal の settings.json に追記

Windows Terminal のタブに下向きの矢印 v をクリックして、メニューから「設定」を選択。

左サイドバーから「JSON ファイルを開く」を選択。

すると、settings.json が開くので以下の箇所に Git Bash の設定を追記する。

`settings.json`
``` json
{
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "defaultProfile": "{00000000-0000-0000-0000-000000000000}",
    "profiles": {
        "defaults": {},
        "list": [
            {
                "guid": "{00000000-0000-0000-0000-000000000000}",
                "name": "Windows PowerShell",
                "commandline": "powershell.exe",
                "hidden": false
            },
            {
                "guid": "{00000000-0000-0000-0000-000000000000}",
                "name": "コマンド プロンプト",
                "commandline": "cmd.exe",
                "hidden": false
            },
            {
                "guid": "{00000000-0000-0000-0000-000000000000}",
                "name": "Ubuntu-20.04",
                "source": "Windows.Terminal.Wsl"
            },
            {
                "guid": "{00000000-0000-0000-0000-000000000000}",
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            }
            // <-- ここの Git Bash の設定を追記する
        ]
    },
    "schemes": []
}
```

追記する Git Bash の設定例は以下の通り。

ユーザーは以下のパスが含まれる場合は、ユーザーホームのパスを %USERPROFILE% で指定すること。

`Git Bash の設定例`
``` json
{
    "acrylicOpacity": 1.0,
    "closeOnExit": "graceful",
    "colorScheme": "Campbell",
    // 自分の環境にインストールされている Git の bash.exe のパスを指定する
    "commandline": "\"C:\\Program Files\\Git\\bin\\bash.exe\" --login -i -l", 
    "cursorColor": "#FFFFFF",
    "cursorShape": "bar",
    "fontFace": "Consolas",
    "fontSize": 12,
    "guid": "{83d9a4e0-7540-4884-a3a9-d1bb03e9167d}",
    "historySize": 9001,
    // 自分の環境に格納されている git-for-windows.ico のパスを指定する
    "icon": "C:\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico",
    "name": "Git Bash",
    "padding": "10, 0, 10, 0",
    "snapOnInput": true,
    "startingDirectory": "%USERPROFILE%"
}
```

### 「既定のプロファイル」の設定

最後に、Windows Terminal の設定 > スタートアップ > 既定のプロファイルから「Git Bash」を選択しておく。
