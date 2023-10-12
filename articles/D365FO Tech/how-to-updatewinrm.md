---
title: クラウド ホスト環境で WinRM 証明書をアップデートする方法
date: 2023-10-12
tags:
  - D365FO Tech
  - LCS
  - WinRM
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポート チームの佐藤です。

Dynamics 365 Finance and Operations のクラウド ホスト環境でシークレットの入れ替えを実施した際に、  
WinRM SSL 証明書の有効期限が切れている旨のエラーが出ることがありますので、WinRM SSL 証明書の有効期限をアップデートする方法を紹介します。  

<!-- more -->
## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.36
Platform version: PU60

## シークレットの入れ替え方法
プロジェクト オーナーまたは環境管理者は、LCS からシークレットを入れ替えることが可能です。  
シークレットの入れ替えを行うには、LCS にて対象プロジェクト > [対象の環境] > [管理] > [シークレットの入れ替え] を選択します。  
エラーが出なければ、本 Blog の[履歴の確認](#履歴の確認)の操作にて、[シークレットの入れ替え] の完了が確認できます。  


## 前提条件
クラウド ホスト環境の WinRM SSL 証明書の有効期限は、環境が構築された日から 1 年です。  


## WinRM SSL 証明書の有効期限の確認方法
1. リモート デスクトップで環境にログインする
2. Windows 検索にて "certmgr" と入力して Certificate Manager を開く
3. Local Machine / Personal / Certificates に遷移する  
WinRM SSL 証明書の名前は、デプロイされた VM の名前と同じになります。  
![](./how-to-updatewinrm/how-to-updatewinrm1.jpg)


## WinRM SSL 証明書の有効期限が切れている際の対処法
既に環境構築から 1 年以上経過し、WinRM SSL 証明書の有効期限が切れている場合、[シークレットの入れ替え] にて、WinRM SSL 証明書のエラーが出る場合があります。  
![](./how-to-updatewinrm/how-to-updatewinrm0.jpg)

この WinRM SSL 証明書の有効期限は以下の手順にて更新することができます。  

## WinRM SSL 証明書の更新手順 (手元の PC で操作します)
1. LCS を開く
2. LCS のプロジェクト選択画面にて、右部の「共有アセット ライブラリ」のパネルをクリックする
4. 資産タイプにて「モデル」を選択する
5. 「Renew WinRM certificate」ファイルをダウンロードする
6. RenewWinRMcertificate.zip ファイルをローカル フォルダで解凍する (2022/07 現在)
   ![](./how-to-updatewinrm/how-to-updatewinrm2.png)

7. フォルダ内の README.txt に記載されている手順に従う

## README.txt の内容（2022/07 現在 日本語訳）  
1. ZIP ファイルからファイルをダウンロードし、解凍する  
2. 管理者として PowerShell を開く  
3. 解凍したファイルがあるフォルダを選択する  
4. 最新の Azure PowerShell がインストールされていることを確認し、次の手順に従います。  
   Azure PowerShell のインストール手順は以下のリンクにあります。    
   (README.txt 記載のURLのリンクが切れているため、別のURLを下記に記載しています)  

　　https://learn.microsoft.com/ja-jp/powershell/azure/azurerm/install-azurerm-ps?view=azurermps-6.13.0

5. PowerShell のスクリプトを実行するための入力データを準備する。  
   a. VM が配置されている Azure Subscription ID  
   b. VM が配置されているリソースグループ名  
6. PowerShell ウィンドウで以下のコマンドを実行し、サブスクリプション ID とリソースグループ名を指定します  
   .\RenewWinRMCertificate.ps1 -AzureSubscriptionId <SubscriptionId> -ResourceGroupNameForVM <ResourceGroupName>  

上記手順にて WinRM SSL 証明書の有効期限が作業日から 1 年後に設定されます。  
WinRM SSL 証明書が正しく入れ替えられたことを確認するには、[有効期限の確認方法](#有効期限の確認方法)を参照ください。  
WinRM SSL 証明書の有効期限が切れていない状態になった後、[シークレットの入れ替え方法](#シークレットの入れ替え方法)にてシークレットを入れ替えることが可能です。

## 履歴の確認
[シークレットの入れ替え]が完了すると、環境の履歴が更新されます。履歴は、環境の詳細ページで [履歴] > [環境の変更] をクリックすると表示されます。  
   ![](./how-to-updatewinrm/how-to-updatewinrm3.png)

(関連情報)  
[シークレットの入れ替え](https://cloudblogs.microsoft.com/dynamics365/it/2018/04/22/rotate-the-expired-or-nearly-expired-ssl-certificate-on-your-subscriptions-one-box-environments)  
[WinRM SSL証明書の更新方法](https://cloudblogs.microsoft.com/dynamics365/it/2018/05/02/how-to-update-the-winrm-ssl-certificate-on-environments-deployed-in-your-subscription/?source=lcs)

## 既知のエラーと対処策
“dynamicssupportsa” という名前がストレージ アカウント名として使用できない場合、下記のエラーが発生します。
```javascript
The storage account named dynamicssupportsa is already taken.
```
その場合は、RenewWinRMCertificate フォルダにある、RenewWinRMCertificate.ps1 ファイルをメモ帳等で開き、
$storageAccountNameForScript の項目を以下のように任意の名前に変更すると、処理が成功します。
任意の名前に変更する箇所は、$storageAccountNameForScript 行のみとなります。

   ![](./how-to-updatewinrm/how-to-updatewinrm4.png)



---
## おわりに  

Dynamics 365 Finance and Operations のクラウド ホスト環境でシークレットの入れ替えを実施した際に、  
WinRM SSL 証明書の有効期限が切れている旨のエラーが出ることがありますので、WinRM SSL 証明書の有効期限をアップデートする方法を紹介しました。  
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。  
