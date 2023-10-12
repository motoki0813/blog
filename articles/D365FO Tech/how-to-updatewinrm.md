---
title: クラウドホスト環境でWinRM 証明書をアップデートする方法
date: 2023-10-12
tags:
  - D365FO Tech
  - LCS
  - WinRM
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートチームの佐藤です。

Dynamics 365 Finance and Operations のクラウドホスト環境でシークレットの入れ替えを実施した際に、  
WinRM SSL 証明書の有効期限が切れている旨のエラーが出ることがありますので、WinRM SSL 証明書の有効期限をアップデートする方法を紹介します。  

<!-- more -->
## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.36
Platform version: PU60

## シークレットの入れ替え方法
プロジェクトオーナーまたは環境管理者は、LCSからシークレットを入れ替えることが可能です。  
シークレットの入れ替えを行うには、LCS にて対象プロジェクト > [対象の環境] > [管理] > [シークレットの入れ替え] を選択します。  
エラーが出なければ、本Blogの[履歴の確認](#履歴の確認)の操作にて、[シークレットの入れ替え] の完了が確認できます。  


## 前提条件
クラウドホスト環境のWinRM SSL 証明書の有効期限は、環境が構築された日から 1 年です。  


## WinRM SSL 証明書の有効期限の確認方法
1. リモートデスクトップで環境にログインする
2. Windows検索にて "certmgr" と入力してCertificate Managerを開く
3. Local Machine / Personal / Certificates に遷移する  
WinRM SSL証明書の名前は、デプロイされたVMの名前と同じになります。  
![](./how-to-updatewinrm/how-to-updatewinrm1.jpg)


## WinRM SSL 証明書の有効期限が切れている際の対処法
既に環境構築から1年以上経過し、WinRM SSL証明書の有効期限が切れている場合、[シークレットの入れ替え] にて、WinRM SSL証明書のエラーが出る場合があります。  
![](./how-to-updatewinrm/how-to-updatewinrm0.jpg)

このWinRM SSL証明書の有効期限は以下の手順にて更新することができます。  

## WinRM SSL証明書の更新手順 (手元のPCで操作します)
1. LCSを開く
2. LCSのプロジェクト選択画面にて、右部の「共有アセットライブラリ」のパネルをクリックする
4. 資産タイプにて「モデル」を選択する
5. 「Renew WinRM certificate」ファイルをダウンロードする
6. RenewWinRMcertificate.zip ファイルをローカルフォルダで解凍する（2022/07/現在）
   ![](./how-to-updatewinrm/how-to-updatewinrm2.png)

7. フォルダ内のREADME.txtに記載されている手順に従う

## README.txtの内容（2022/07/現在, 日本語訳）  
1. ZIPパッケージからファイルをダウンロードし、解凍する  
2. 管理者としてPowerShellを開く  
3. 解凍したファイルがあるフォルダを選択する  
4. 最新の Azure PowerShell がインストールされていることを確認し、次の手順に従います。  
   Azure PowerShellのインストール手順は以下のリンクにあります。    
   （README.txt記載のURLのリンクが切れているため、別のURLを下記に記載しています）  

　　https://docs.microsoft.com/ja-jp/powershell/azure/azurerm/install-azurerm-ps?view=azurermps-6.13.0

5. PowerShell のスクリプトを実行するための入力データを準備する。  
   a. VM が配置されている Azure Subscription ID  
   b. VM が配置されているリソースグループ名  
6. PowerShell ウィンドウで以下のコマンドを実行し、サブスクリプション ID とリソースグループ名を指定します  
   .\RenewWinRMCertificate.ps1 -AzureSubscriptionId <SubscriptionId> -ResourceGroupNameForVM <ResourceGroupName>  

上記手順にてWinRM SSL 証明書の有効期限が作業日から1年後に設定されます。  
WinRM SSL 証明書が正しく入れ替えられたことを確認するには、[有効期限の確認方法](#有効期限の確認方法)を参照ください。  
WinRM SSL 証明書の有効期限が切れていない状態になった後、[シークレットの入れ替え方法](#シークレットの入れ替え方法)にてシークレットを入れ替えることが可能です。

## 履歴の確認
[シークレットの入れ替え]が完了すると、環境の履歴が更新されます。履歴は、環境の詳細ページで [履歴] > [環境の変更] をクリックすると表示されます。  
   ![](./how-to-updatewinrm/how-to-updatewinrm3.png)

（関連情報）  
[シークレットの入れ替え](https://cloudblogs.microsoft.com/dynamics365/it/2018/04/22/rotate-the-expired-or-nearly-expired-ssl-certificate-on-your-subscriptions-one-box-environments)  
[WinRM SSL証明書の更新方法](https://cloudblogs.microsoft.com/dynamics365/it/2018/05/02/how-to-update-the-winrm-ssl-certificate-on-environments-deployed-in-your-subscription/?source=lcs)

## 既知のエラーと対処策
“dynamicssupportsa” という名前がストレージアカウント名として使用できない場合、下記のエラーが発生します。
```javascript
The storage account named dynamicssupportsa is already taken.
```
その場合は、RenewWinRMCertificate フォルダにある、RenewWinRMCertificate.ps1 ファイルをメモ帳等で開き、
$storageAccountNameForScript の項目を以下のように任意の名前に変更すると、処理が成功します。
任意の名前に変更する箇所は、$storageAccountNameForScript行のみとなります。

   ![](./how-to-updatewinrm/how-to-updatewinrm4.png)



---
## おわりに  

Dynamics 365 Finance and Operations のクラウドホスト環境でシークレットの入れ替えを実施した際に、  
WinRM SSL 証明書の有効期限が切れている旨のエラーが出ることがありますので、WinRM SSL 証明書の有効期限をアップデートする方法を紹介しました。  
もし、お困りのこと等がございましたら、弊社までお問い合わせ頂きますようお願いいたします。  
