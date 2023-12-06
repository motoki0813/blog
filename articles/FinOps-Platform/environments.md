<<<<<<< HEAD:articles/D365FO Tech/environments.md
---
title: Dynamics 365 for Finance and Operations の環境ごとの違い
date: 2023-09-08
tags:
  - D365FO Tech
  - Tips
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートチームの福原です。
この記事では、 Dynamics 365 Finance and Operations (D365FO) の環境ごとの違いについてご案内します。
クラウドホスト環境、サンドボックス環境、Tier2環境、本番環境等、様々な呼び方の環境があり、また、それぞれの環境で使える機能も異なるので、分かりづらいというお声をいただくことがありますので、そのような場合には本記事をご参考ください。

<!-- more -->




| 環境名                         | 本番環境                 | サンドボックス環境                       | クラウドホスト環境                               | 
| :----------------------------- | :----------------------- | :--------------------------------------- | :----------------------------------------------- | 
| 配置可能なLCSプロジェクト                 | 実装プロジェクト         | 実装プロジェクト                         | 実装プロジェクト<br>  or パートナー試用版プロジェクト | 
| 呼ばれ方例                   | Production 環境 <br> 運用環境 <br> Microsoft-managed 環境 <br> セルフサービス環境  | Sandbox環境 <br> Tier2 ~ Tier5 環境 <br> 非運用環境  <br> Microsoft-managed 環境 <br> セルフサービス環境  | Cloud-hosted環境、<br> 開発環境            | 
| 配置場所                       | Azure                    | Azure                                    | Azure                                            | 
| Azure Subscription (*1)             | Microsoft                | Microsoft                                | 顧客                                             | 
| データベース                   | Azure SQL                | Azure SQL                                | Azure VM 内のオンプレミスSQL Server              | 
| SSMSによる<br> データベースへの接続 | 不可                     | 可 (*2)                                       | 可                                               | 
| RDP接続                        | 不可                     | 不可                                     | 可                                               | 
| フライト有効化方法 (*3)            | Microsoft                | Microsoft                                | 顧客

(*1): 本番環境、サンドボックス環境は、Microsoft 内の Azure Subscription に紐づいて管理されているので、顧客は Azure portal にて環境の情報を見ることができません。クラウドホスト環境は顧客の Azure Subscirption 内で構築されますので、Azure portal にて環境や請求の情報を見ることができます。

> [!NOTE]
> クラウドホスト環境は弊社からアクセスおよびログの取得ができないため、弊社によるトラブルシューティングが制限されております。
> クラウドホスト環境内の事象が解消しない場合には、クラウドホスト環境の再作成をお願いしていますので、再作成可能という前提でクラウドホスト環境の運用をお願い致します。
> 以下の弊社公開資料の注意事項もご参考にしていただきますようお願い致します。
> 
> [開発環境の配置とアクセス](https://learn.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/access-instances)
>---抜粋---
>注意
> ・Microsoft サポートでは、レベル 1 の開発環境でのトラブルシューティングが制限される場合があります。
> ・特定の状況では、問題を解決するために、Microsoft サポートからレベル 1 環境の新規展開が要求される場合があります。
> ・開発環境にはビジネス クリティカルなデータを含めるべきではなく、破棄可能と見なされます。
> ・120 の環境だけがテナントごとのサポートです。 特定のテナント下のクラウド ホスト環境数を制限して、サンドボックスおよび運用環境を配置できる十分なキャパシティを許可することをお勧めします。

(*2): https://jpdynamicserp.github.io/blog/D365FO%20Tech/database-just-in-time-jit-access/ の手順となります。
(*3): 本番環境、サンドボックス環境、クラウドホスト環境のフライトの管理方法の違いは https://jpdynamicserp.github.io/blog/D365FO%20Tech/what-is-flight/ にてご案内しております。


(*): 本記事は2023年9月8日時点での情報です。


---
## おわりに  

以上、 Dynamics 365 for Finance and Operations (D365FO) の環境ごとの違いについてご紹介しました。
=======
---
title: Dynamics 365 for Finance and Operations の環境ごとの違い
date: 2023-09-08
tags:
  - D365FO Tech
  - Tips
disableDisclaimer: false
---

こんにちは、Dynamics ERP サポートチームの福原です。
この記事では、 Dynamics 365 Finance and Operations (D365FO) の環境ごとの違いについてご案内します。
クラウドホスト環境、サンドボックス環境、Tier2環境、本番環境等、様々な呼び方の環境があり、また、それぞれの環境で使える機能も異なるので、分かりづらいというお声をいただくことがありますので、そのような場合には本記事をご参考ください。

<!-- more -->




| 環境名                         | 本番環境                 | サンドボックス環境                       | クラウドホスト環境                               | 
| :----------------------------- | :----------------------- | :--------------------------------------- | :----------------------------------------------- | 
| 配置可能なLCSプロジェクト                 | 実装プロジェクト         | 実装プロジェクト                         | 実装プロジェクト<br>  or パートナー試用版プロジェクト | 
| 呼ばれ方例                   | Production 環境 <br> 運用環境 <br> Microsoft-managed 環境 <br> セルフサービス環境  | Sandbox環境 <br> Tier2 ~ Tier5 環境 <br> 非運用環境  <br> Microsoft-managed 環境 <br> セルフサービス環境  | Cloud-hosted環境、<br> 開発環境            | 
| 配置場所                       | Azure                    | Azure                                    | Azure                                            | 
| Azure Subscription (*1)             | Microsoft                | Microsoft                                | 顧客                                             | 
| データベース                   | Azure SQL                | Azure SQL                                | Azure VM 内のオンプレミスSQL Server              | 
| SSMSによる<br> データベースへの接続 | 不可                     | 可 (*2)                                       | 可                                               | 
| RDP接続                        | 不可                     | 不可                                     | 可                                               | 
| フライト有効化方法 (*3)            | Microsoft                | Microsoft                                | 顧客

(*1): 本番環境、サンドボックス環境は、Microsoft 内の Azure Subscription に紐づいて管理されているので、顧客は Azure portal にて環境の情報を見ることができません。クラウドホスト環境は顧客の Azure Subscirption 内で構築されますので、Azure portal にて環境や請求の情報を見ることができます。

> [!NOTE]
> クラウドホスト環境は弊社からアクセスおよびログの取得ができないため、弊社によるトラブルシューティングが制限されております。
> クラウドホスト環境内の事象が解消しない場合には、クラウドホスト環境の再作成をお願いしていますので、再作成可能という前提でクラウドホスト環境の運用をお願い致します。
> 以下の弊社公開資料の注意事項もご参考にしていただきますようお願い致します。
> 
> [開発環境の配置とアクセス](https://learn.microsoft.com/ja-jp/dynamics365/fin-ops-core/dev-itpro/dev-tools/access-instances)
>---抜粋---
>注意
> ・Microsoft サポートでは、レベル 1 の開発環境でのトラブルシューティングが制限される場合があります。
> ・特定の状況では、問題を解決するために、Microsoft サポートからレベル 1 環境の新規展開が要求される場合があります。
> ・開発環境にはビジネス クリティカルなデータを含めるべきではなく、破棄可能と見なされます。
> ・120 の環境だけがテナントごとのサポートです。 特定のテナント下のクラウド ホスト環境数を制限して、サンドボックスおよび運用環境を配置できる十分なキャパシティを許可することをお勧めします。

(*2): https://jpdynamicserp.github.io/blog/FinOps-Platform/database-just-in-time-jit-access/ の手順となります。
(*3): 本番環境、サンドボックス環境、クラウドホスト環境のフライトの管理方法の違いは https://jpdynamicserp.github.io/blog/FinOps-Platform/what-is-flight/ にてご案内しております。


(*): 本記事は2023年9月8日時点での情報です。


---
## おわりに  

以上、 Dynamics 365 for Finance and Operations (D365FO) の環境ごとの違いについてご紹介しました。
>>>>>>> repoA/main:articles/FinOps-Platform/environments.md
