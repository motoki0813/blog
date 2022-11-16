---
title: D365FO のブラウザーセッションID の取得方法
date: 2022-11-16
tags:
  - D365FO
  - Tech
  - tips
  - 10.0.31
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートチームです。  
この記事では、 Dynamics 365 Finance and Operations のブラウザーセッションID の取得方法をご紹介します。
もし、D365FO のUI 上にてエラー等が発生した際に、ブラウザーセッションID を弊社に提供して頂けますと、そのID を基にし、サーバー残っておりますログを弊社にて調査できる場合がございますので、トラブルシューティングをより効果的に行うことができます。もし、お問い合わせの中で弊社サポートエンジニアより、ブラウザーセッションID の取得を依頼されましたら、こちらの手順により取得して頂けますと幸いです。

<!-- more -->

注意点としまして、Web ブラウザーのページを更新しますと、ブラウザーセッションID は変わってしまいますので、事象の再現時および、ブラウザーセッションID の取得時にはWeb ブラウザーのページを更新しないようにお願いします。

## 検証に用いた製品・バージョン
Dynamics 365 Finance and Operations      
Application version: 10.0.31  
Platform version: PU55  



## Dynamics 365 Finance and Operations のブラウザーセッションID の取得方法

1. D365FO の右上の? ボタン > フィードバック をクリックします。

    <img src="./image1.png" style="border: 1px black solid;">

2. フィードバック画面が開きますので、下部のセッション情報をコピーし、弊社にご提供して頂けますと幸いです。

    <img src="./image2.png" style="border: 1px black solid;">


---
## おわりに  

以上、 Dynamics 365 Finance and Operations のブラウザーセッションID の取得方法についてご紹介しました。
より詳細な情報が必要な場合、弊社テクニカルサポート, Customer Success Account Manager (CSAM), Customer Engineer (CE) までお問い合わせください。
