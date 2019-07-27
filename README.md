# DDON-BGM-DECRYPTOR
DDONのBGMファイルを復号するよ

## 手順
1. [SNGW-DEC](http://www.sb-online.org/maluc/index.php?did=sngwdec) をダウンロードして適当なフォルダーに展開する

1. 下記のスクリプトを適当なテキストエディターにコピーする 
    ```powershell
    $src = "F:\CAPCOM\Dragon's Dogma Online\nativePC\sound\stream\bgm"
    $dst = "E:\ddon-music"
    $decryptor = "E:\sngw.exe"

    dir $src -Recurse -Filter "*.sngw" | %{
        $dd = Join-Path $dst ($_.DirectoryName.Remove(0,$src.Length))
        $dn = Join-Path $dd ([System.IO.Path]::ChangeExtension($_.Name, ".ogg"))
        md $dd -Force | Out-Null
        copy $_.FullName $dn -Force | Out-Null
        $dn
        &$decryptor "$dn"
    }
    trap {break}
    ```
1. 1行目にある`$src`にDDONのインストール先の中にある`bgm`フォルダーのパスを指定する

1. 2行目にある`$dst`に復号したファイルを出力するフォルダーを指定する

1. 3行目にある`$decryptor`に`sngw.exe`のパスを指定する

1. PowerShellを起動する

1. 先ほど書き換えたスクリプトをPowerShellにコピペしてエンター

1. 指定した出力先のフォルダーに復号されたBGMファイルが出来ているよ

出力されるファイルは全部で 1.3GB/291ファイルの .ogg ファイルだよ
