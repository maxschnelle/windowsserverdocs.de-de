---
title: SDN-Firewallüberwachung
description: Die firewallüberwachung ist eine neue Funktion für die Sdn-Firewall in Windows Server 2019. Wenn Sie die Sdn-Firewall aktivieren, werden alle Flows aufgezeichnet, die von Sdn-Firewallregeln (ACLs) mit aktivierter Protokollierung verarbeitet werden.
manager: grcusanz
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/22/2018
ms.openlocfilehash: 256c1e503dcaaf0e482ab3f69ca1c5a1b977a10b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996523"
---
# <a name="sdn-firewall-auditing"></a>SDN-Firewallüberwachung

>Gilt für: Windows Server 2019

Die firewallüberwachung ist eine neue Funktion für die Sdn-Firewall in Windows Server 2019. Wenn Sie die Sdn-Firewall aktivieren, werden alle Flows aufgezeichnet, die von Sdn-Firewallregeln (ACLs) mit aktivierter Protokollierung verarbeitet werden. Die Protokolldateien müssen eine Syntax aufweisen, die mit den [Azure Network Watcher Flow-Protokollen](/azure/network-watcher/network-watcher-nsg-flow-logging-overview)konsistent ist. Diese Protokolle können für die Diagnose verwendet werden oder zur späteren Analyse archiviert werden. 

In Kürze werden einige Beispiele für die Verarbeitung dieser Dateien mithilfe von Tools wie Power BI bereitgestellt.

_**Probieren Sie es aus, und geben Sie uns Feedback!**_

Hier ist ein Beispielskript zum Aktivieren der firewallüberwachung auf den Hyper-V-Hosts.Aktualisieren Sie die Variablen am Anfang, und führen Sie Sie auf einem Windows Server 2019-Computer mit installierter RSAT-networkcontroller-Funktion aus:

```PowerShell
$logpath = "C:\test\log1"
$servers = @("sa18n22-2", "sa18n22-3", "sa18n22-4")
$uri = "https://sa18n22sdn.sa18.nttest.microsoft.com"

# Create log directories on the hosts
invoke-command -Computername $servers  {
    param(
        $Path
    )
    mkdir $path    -force
} -argumentlist $LogPath

# Set firewall auditing settings on Network Controller
$AuditProperties = new-object Microsoft.Windows.NetworkController.AuditingSettingsProperties
$AuditProperties.OutputDirectory = $logpath
set-networkcontrollerauditingsettingsconfiguration -connectionuri $uri -properties $AuditProperties -force  | out-null

# Enable logging on each server
$servers = get-networkcontrollerserver -connectionuri $uri
foreach ($s in $servers) {
    $s.properties.AuditingEnabled = @("Firewall")
    new-networkcontrollerserver -connectionuri $uri -resourceid $s.resourceid -properties $s.properties -force | out-null
}
```

Nach der Aktivierung wird eine neue Datei im angegebenen Verzeichnis auf jedem Host ca. einmal pro Stunde angezeigt.Sie sollten diese Dateien regelmäßig verarbeiten und aus den Hosts entfernen.Die aktuelle Datei hat eine Länge von 0 (null) und ist gesperrt, bis Sie an der nächsten Stunden Markierung geleert wurde:

```syntax
PS C:\test\log1> dir

    Directory: C:\test\log1

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        7/19/2018   6:28 AM          17055 SdnFirewallAuditing.d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a.20180719TL122803093.json
-a----        7/19/2018   7:28 AM           7880 SdnFirewallAuditing.d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a.20180719TL132803173.json
-a----        7/19/2018   8:28 AM           7867 SdnFirewallAuditing.d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a.20180719TL142803264.json
-a----        7/19/2018   9:28 AM          10949 SdnFirewallAuditing.d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a.20180719TL152803360.json
-a----        7/19/2018   9:28 AM              0 SdnFirewallAuditing.d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a.20180719TL162803464.json
```

Diese Dateien enthalten eine Sequenz von Fluss Ereignissen, z. b.:

```syntax
{
    "records": [
        {
            "properties":{
                "Version":"1.0",
                "flows":[
                    {
                        "flows":[
                            {
                                "flowTuples":["1531963580,192.122.0.22,192.122.255.255,138,138,U,I,A"],
                                "portId":"9",
                                "portName":"7290436D-0422-498A-8EB8-C6CF5115DACE"
                            }
                        ],
                        "rule":"Allow_Inbound"
                    }
                ]
            },
            "operationName":"NetworkSecurityGroupFlowEvents",
            "resourceId":"394f647d-2ed0-4c31-87c5-389b8c0c8132",
            "time":"20180719:L012620622",
            "category":"NetworkSecurityGroupFlowEvent",
            "systemId":"d8b3b697-5355-40e2-84d2-1bf2f0e0dc4a"
            },
```


Beachten Sie, dass die Protokollierung nur für Regeln durchgeführt wird, für die die **Protokollierung** **aktiviert**ist. Beispiel:

```syntax
{
    "Tags":  null,
    "ResourceRef":  "/accessControlLists/AllowAll",
    "InstanceId":  "4a63e1a5-3264-4986-9a59-4e77a8b107fa",
    "Etag":  "W/\"1535a780-0fc8-4bba-a15a-093ecac9b88b\"",
    "ResourceMetadata":  null,
    "ResourceId":  "AllowAll",
    "Properties":  {
                       "ConfigurationState":  null,
                       "ProvisioningState":  "Succeeded",
                       "AclRules":  [
                                        {
                                            "ResourceMetadata":  null,
                                            "ResourceRef":  "/accessControlLists/AllowAll/aclRules/AllowAll_Inbound",
                                            "InstanceId":  "ba8710a8-0f01-422b-9038-d1f2390645d7",
                                            "Etag":  "W/\"1535a780-0fc8-4bba-a15a-093ecac9b88b\"",
                                            "ResourceId":  "AllowAll_Inbound",
                                            "Properties":  {
                                                               "Protocol":  "All",
                                                               "SourcePortRange":  "0-65535",
                                                               "DestinationPortRange":  "0-65535",
                                                               "Action":  "Allow",
                                                               "SourceAddressPrefix":  "*",
                                                               "DestinationAddressPrefix":  "*",
                                                               "Priority":  "101",
                                                               "Description":  null,
                                                               "Type":  "Inbound",
                                                               "Logging":  "Enabled",
                                                               "ProvisioningState":  "Succeeded"
                                                           }
                                        },
                                        {
                                            "ResourceMetadata":  null,
                                            "ResourceRef":  "/accessControlLists/AllowAll/aclRules/AllowAll_Outbound",
                                            "InstanceId":  "068264c6-2186-4dbc-bbe7-f504c6f47fa8",
                                            "Etag":  "W/\"1535a780-0fc8-4bba-a15a-093ecac9b88b\"",
                                            "ResourceId":  "AllowAll_Outbound",
                                            "Properties":  {
                                                               "Protocol":  "All",
                                                               "SourcePortRange":  "0-65535",
                                                               "DestinationPortRange":  "0-65535",
                                                               "Action":  "Allow",
                                                               "SourceAddressPrefix":  "*",
                                                               "DestinationAddressPrefix":  "*",
                                                               "Priority":  "110",
                                                               "Description":  null,
                                                               "Type":  "Outbound",
                                                               "Logging":  "Enabled",
                                                               "ProvisioningState":  "Succeeded"
                                                           }
                                        }
                                    ],
                       "IpConfigurations":  [

                                            ],
                       "Subnets":  [
                                       {
                                           "ResourceMetadata":  null,
                                           "ResourceRef":  "/virtualNetworks/10_0_1_0/subnets/Subnet1",
                                           "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                           "Etag":  null,
                                           "ResourceId":  null,
                                           "Properties":  null
                                       }
                                   ]
                   }
}
```