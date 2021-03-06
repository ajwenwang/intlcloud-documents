## 概要

クラウド計算により、高性能計算（HPC）は、より広い帯域幅とより高い計算能力のアプリケーションを使用して、複雑な科学的問題、エンジニアリング問題、および業務問題を解決できます。

ただし、HPCによって解決される問題は通常プロジェクト向けであり、クラウドプラットフォームの高拡張性に対する要求も高い。この文章では、Tencent Cloudがどのように超高計算能力（CVM）、高拡張性（AS）、大容量ハードディスク（CBS）、およびオブジェクトストレージ（COS）の力を活用して、企業を応援してHPC業務を完成するかを紹介します。

## 顧客紹介：iCarbonX (Shenzhen) Company Limited	

**《Fast Company》2017世界で最も革新的な企業リストの中国トップ10にランクイン。一緒にリストに入った中国企業には、Alibaba、Tencent、Xiaomi、BBK、Huawei、およびWanda Groupなどの大企業があります。**

データマイニングと機械学習を通じて、iCarbonXは人工知能の利点を大規模なビッグデータ分析とアプリケーションにもたらし、デジタルライフをカスタマイズに管理する製品とサービスを提供します。

![](https://mc.qcloudimg.com/static/img/a1037773a47161e495e2f6407d48e2b1/image.jpg)

（马化腾氏とiCarbonX CEOの王俊氏がコミュニケーション中）

## ビジネス上の課題

- マルチオミックス検出の計算クラスタは、何千ものコアと何百TBものリソースを随時的に拡張する必要があります。
- 検出ワークフローの計算ノード環境の準備は面倒であり、手間がかかります。

## Tencent Cloudに基づいて業務を完成させる方法

![](https://mc.qcloudimg.com/static/img/e98b85e787c02b533f5ffd06a4166bac/31.png)

1. 初期データ出力：検出装置によるマルチオミックスデータの初期処理を実行します。
2. マルチオミックスデータ分析：この部分は主にTencent Cloudで実行され、3つのコアインフラストラクチャ機能に依存しています。
	- 複数台の30コア以上、さらに60コア以上の高性能サーバー クラスタ。
	- 大型、効率的なクラウドストレージからなるデータサーバー。
	- Tencent Cloud ASサービスを使用してHPCワークフロー全体を管理します。

その中で、最も拡張が必要な計算クラスタは、次のように配置されます：

![Alt text](https://mc.qcloudimg.com/static/img/d7208378accfb11c320668ee5089a0c3/02.png)
 
大規模な拡張機能を最も必要とするCompute NodeをASに任せて、iCarbonXが分間レベルで数千のコアと数百TBのHPCクラスタの作成を実現していることがわかります。計算クラスタの安定性およびリアルタイム性能が大幅に向上し、手間が削減され、それによってコストが大幅に節約されます。

> 注：
> 過去2か月だけで、Tencent CloudはHPCのお客様向けに60000以上のコアと数万のTBクラウドストレージを提供しました。これらはすべてただ数分間で完了したのです。

## 顧客価値

- Tencent Cloudの超高計算能力と高拡張能力により、お客様はクラウドで高性能計算を実行して研究スピードを向上させることができます。iCarbonXは、ASのおかげで、数千コアから数百TBまでのスケールアウト問題を容易に解決しました。
- クラウドプラットフォームの柔軟性とTencent Cloudの従量制課金（秒）を組み合わせることで、最小限の投資で高品質の計算サービスを顧客に提供し、コストを削減できるようにします。

