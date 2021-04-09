# CVAD Standard for Azure Workshop環境構築
## 基本環境構築
- 任意のリソースグループを作成します。
-  次のボタンをクリックしてテンプレートよりデプロイを行います。このテンプレートではADサーバー用のVMを構築し、CustomScriptExtensionを用いてADDSの構成、ユーザー作成まで行います。  
    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhogeda%2FPPTWvdPoCEnvironment%2Fmain%2Fazuredeploy.json)
- Azure VMのCustomScriptExtensionでは複数のスクリプトファイルの実行をサポートしていません。そのため、タスクスケジューラーに他のスクリプトファイルを登録する仕組みを採用しています。
- スクリプトファイルは当該リポジトリに格納していますが、DNS機能を構成する前にVnetのDNS設定を実施してしまうと名前解決に失敗してしまいます。デプロイ完了後に手動でDNS設定をしてください。
- パラメータは次の例を参考に入力してください。
| Parameter  | Sample    |
| --- | --- |
| virtualNetwork_name | [concat(resourceGroup().name,'-vnet')] |
| subnetworks | {"value":[{"name":"snet-enterprise","addressPrefix":"10.0.0.0/24"},{"name":"snet-wvd","addressPrefix":"10.0.1.0/24"}],"Count":2} |
| subnetNameOfAD | snet-enterprise |
| virtualMachineName | adds01 |
| adminUsername | pptadmin |
| adminPassword | WVDPoC#123098! |
| fileUris | https://raw.githubusercontent.com/hogeda/PPTWvdPoCEnvironment/main/WindowsPowershellScript/ConfigureScheduledTask.ps1 |
| domainName | lab.hogeda.com |
| safeModeAdministratorPassword | WVDPoC#123098! | 
| userNames | kyohei.hogeda;kyohei.fugada;kyohei.piyoda |
| userPassword | WVDPoC#123098! |
| ouName | WVD |
| groupName | WVD Users |
