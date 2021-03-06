# CVAD Standard for Azure Workshop環境構築
## 基本環境構築
- ワークショップ参加者のメールアドレスプレフィックスにて、リソースグループを作成します。
- 次のボタンをクリックしてテンプレートよりデプロイを行います。このテンプレートではADサーバー用のVMを構築します。  
    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhogeda%2FPPTCVADStandardForAzureWorkshop%2Fmain%2Fazuredeploy.json)
- デプロイが完了した後はVMの実行コマンド機能を用いて、ADDSの構成、ユーザー作成を行います。
- パラメータは次の例を参考に入力してください。

| Parameter  | Sample    |
| --- | --- |
| virtualNetwork_name | [concat(resourceGroup().name,'-vnet')] |
| subnetworks | {"value":[{"name":"snet-enterprise","addressPrefix":"10.0.0.0/24"},{"name":"snet-wvd","addressPrefix":"10.0.1.0/24"}],"Count":2} |
| subnetNameOfAD | snet-enterprise |
| virtualMachineName | adds01 |
| adminUsername | ctxadmin |
| adminPassword | Citrix12345! |
