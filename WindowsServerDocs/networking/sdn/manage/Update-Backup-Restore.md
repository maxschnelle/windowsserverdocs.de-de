---
title: Upgrade, Sicherung und Wiederherstellung von SDN-Infrastruktur
description: In diesem Thema erfahren Sie, wie zu aktualisieren, Sichern und Wiederherstellen eine SDN-Infrastruktur.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 7916377f58261d0ccaa3fa24f135fccca3d5e79b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446330"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>Upgrade, Sicherung und Wiederherstellung von SDN-Infrastruktur

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema erfahren Sie, wie zu aktualisieren, Sichern und Wiederherstellen eine SDN-Infrastruktur. 

## <a name="upgrade-the-sdn-infrastructure"></a>Upgrade der SDN-Infrastruktur
SDN-Infrastruktur kann von Windows Server 2016 auf Windows Server-2019 aktualisiert werden. Führen Sie für das Upgrade, Sortierung die gleiche Sequenz von Schritten, wie im Abschnitt "die SDN-Infrastruktur aktualisieren". Vor dem Upgrade wird empfohlen, eine Sicherung der Datenbank des Netzwerkcontrollers.

Verwenden Sie für den Netzwerkcontroller-Computer das Cmdlet Get-NetworkControllerNode, überprüfen Sie den Status des Knotens ein, nachdem das Upgrade abgeschlossen wurde. Stellen Sie sicher, dass der Knoten wieder zu "Status nach oben" vor dem Upgrade der anderen Knoten verfügbar ist. Nachdem Sie alle Netzwerkcontroller-Knoten aktualisiert haben, aktualisiert die dem Netzwerkcontroller Microservices innerhalb des Netzwerkcontroller-Clusters innerhalb einer Stunde ausführen. Sie können ein sofortiges Update mit dem Cmdlet Update-Networkcontroller auslösen. 

Installieren Sie den gleichen Windows-Updates auf allen Komponenten des Betriebssystems des Systems Software Defined Networking (SDN), einschließlich:

- Hyper-V-Hosts mit SDN-Funktionalität
- Netzwerkcontroller-VMs
- Software virtueller SLB Mux-Computer
- RAS-Gateway-VMs 

>[!IMPORTANT]
>Wenn Sie System Center Virtual Manager verwenden, müssen Sie es mit der aktuellen Updaterollups aktualisieren.

Wenn Sie jede Komponente aktualisieren, können Sie eine der Standardmethoden für die Installation von Windows-Updates verwenden. Allerdings um minimaler Downtime für arbeitsauslastungen und die Integrität der Datenbank des Netzwerkcontrollers zu gewährleisten, gehen Sie folgendermaßen vor:

1. Aktualisieren Sie die Verwaltungskonsolen.<p>Installieren Sie die Updates auf allen Computern, in dem Sie das Network Controller-Powershell-Modul verwenden.  Einschließlich der an einer beliebigen Stelle, dass Sie die RSAT-NetworkController Rolle alleine installiert haben. Mit Ausnahme der Netzwerkcontroller-VMs selbst; Aktualisieren Sie sie im nächsten Schritt.

2. Klicken Sie auf der ersten VM-Netzwerk Controller installieren Sie alle Updates, und starten Sie neu.

3. Verwenden Sie vor dem Fortfahren auf der nächsten Network Controller-VM die `get-networkcontrollernode` Cmdlet, um den Status des Knotens zu überprüfen, die Sie aktualisiert und neu gestartet.

4. Warten Sie während des Neustartzyklus für den Netzwerkcontroller-Knoten heruntergefahren und neu gestartet werden, erneut aus.<p>Nach dem Neustart des virtuellen Computers dauert es einige Minuten, bis er wieder in geht die **_einrichten_** Status. Ein Beispiel der Ausgabe finden Sie unter 

5. Installieren von Updates auf jede SLB Mux-VM eine zu einem Zeitpunkt, um kontinuierliche Verfügbarkeit der Load Balancer-Infrastruktur sicherzustellen.

6. Aktualisieren von Hyper-V-Hosts und RAS-Gateways, beginnend mit den Hosts, die die RAS-Gateways, die enthalten in **Standby** Modus.<p>RAS-Gateway-VMs kann nicht live migriert werden, ohne Verlust der Mandanten-Verbindungen. Bei der Aktualisierung, achten Sie minimiert die Anzahl der Mandanten-Verbindungen ein Failover auf ein neues RAS-Gateway. Durch die Koordination der Aktualisierung der Hosts und -RAS-Gateways, ein Failover jeder Mandant einmal, höchstens.

    a. Den Host der virtuellen Computer, von denen Livemigration zu verschieben.<p>RAS-Gateway-VMs sollten auf dem Host bleiben.

    b. Installieren von Updates auf jede Gateway-VM auf diesem Host.

    c. Wenn das Update die Gateway-VM neu starten, müssen Sie dann einen Neustart des virtuellen Computers.  

    d. Installieren von Updates auf dem Host, auf dem die Gateway-VM, die gerade aktualisiert wurde.

    e. Starten Sie den Host neu, wenn die Updates erforderlich.

    f. Wiederholen Sie für jeden zusätzlichen Host, der einen standby-Gateway enthält.<p>Wenn keine standby-Gateways bleiben möchten, befolgen Sie dann die gleichen Schritte für alle verbleibenden Hosts.


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>Beispiel: Verwenden Sie das Cmdlet Get-networkcontrollernode 

In diesem Beispiel sehen Sie die Ausgabe für die `get-networkcontrollernode` Cmdlet von innerhalb der die Netzwerkcontroller-VMs ausgeführt.  

Der Status der Knoten, die Sie in der Beispielausgabe zu sehen ist:

- NCNode1.contoso.com = Down
- NCNode2.contoso.com = Up
- NCNode3.contoso.com = Up

>[!IMPORTANT]
>Für der Knoten an, warten Sie einige Minuten, bis der Status muss _**einrichten**_ , bevor Sie alle zusätzlichen Knoten, jeweils einzeln aktualisieren.

Nachdem Sie alle Netzwerkcontroller-Knoten aktualisiert haben, aktualisiert die dem Netzwerkcontroller die Microservices innerhalb des Netzwerkcontroller-Clusters innerhalb einer Stunde ausführen. 

>[!TIP]
>Sie können ein sofortiges Update mit Auslösen der `update-networkcontroller` Cmdlet.


```Powershell
PS C:\> get-networkcontrollernode
Name            : NCNode1.contoso.com
Server          : NCNode1.Contoso.com
FaultDomain     : fd:/NCNode1.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Down

Name            : NCNode2.Contoso.com
Server          : NCNode2.contoso.com
FaultDomain     : fd:/ NCNode2.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up

Name            : NCNode3.Contoso.com
Server          : NCNode3.Contoso.com
FaultDomain     : fd:/ NCNode3.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up
```

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>Beispiel: Verwenden Sie das Cmdlet Update-networkcontroller
In diesem Beispiel sehen Sie die Ausgabe für die `update-networkcontroller` Cmdlet, um den Netzwerkcontroller für die Aktualisierung zu erzwingen. 

>[!IMPORTANT]
>Führen Sie dieses Cmdlet aus, wenn Sie keine weitere Updates installiert haben.


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>Sichern der SDN-Infrastruktur

Regelmäßige Sicherungen der Netzwerkcontroller-Datenbank wird sichergestellt, die Geschäftskontinuität im Falle einer notfallwiederherstellung oder Datenverlust.  Sichern die Netzwerkcontroller-VMs ist nicht ausreichend, da sie nicht sicher ist, dass die Sitzung auf die mehrere Netzwerkcontroller Knoten weiterhin.

**Anforderungen:**
* Eine SMB-Freigabe und Anmeldeinformationen mit Lese-/Schreibberechtigungen für die Freigabe- und System.
* Sie können optional eine Gruppe Managed Service Account (GMSA) verwenden, wenn der Netzwerkcontroller Verwendung eines gruppenverwalteten Dienstkontos ebenfalls installiert wurde.

**Vorgehensweise:**

1. Verwenden Sie die VM-backup-Methode Ihrer Wahl oder verwenden Sie Hyper-V, um eine Kopie jeder Controller-VM-Netzwerk zu exportieren.<p>Sichern die Controller-VM-Netzwerk wird sichergestellt, dass die erforderlichen Zertifikate für die Entschlüsselung der Datenbank vorhanden sind.  

2. Wenn Sie System Center Virtual Machine Manager (SCVMM) verwenden möchten, beenden Sie den SCVMM-Dienst, und über SQL Server sichern.<p>Das Ziel besteht hier wird sichergestellt, dass keine Updates zu SCVMM während dieser Zeit durchgeführten was eine Inkonsistenz zwischen dem Netzwerkcontroller-Sicherung und SCVMM kann.  

   >[!IMPORTANT]
   >Starten Sie den SCVMM-Dienst nicht neu, bis die Netzwerkcontroller-Sicherung abgeschlossen ist.

3. Sichern Sie die Netzwerkcontroller-Datenbank mit der `new-networkcontrollerbackup` Cmdlet.

4. Überprüfen Sie den Abschluss und Erfolg der Sicherung mit der `get-networkcontrollerbackup` Cmdlet.

5. Wenn SCVMM zu verwenden, starten Sie die SCVMM-Dienst.



### <a name="example-backing-up-the-network-controller-database"></a>Beispiel: Sichern der Datenbank des Netzwerkcontrollers

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

# Get or Create Credential object for File share user

$ShareUserResourceId = "BackupUser"

$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }
If ($ShareCredential -eq $null) {
    $CredentialProperties = New-Object Microsoft.Windows.NetworkController.CredentialProperties
    $CredentialProperties.Type = "usernamePassword"
    $CredentialProperties.UserName = "contoso\alyoung"
    $CredentialProperties.Value = "<Password>"

    $ShareCredential = New-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential -Properties $CredentialProperties -ResourceId $ShareUserResourceId -Force
}

# Create backup

$BackupTime = (get-date).ToString("s").Replace(":", "_")

$BackupProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerBackupProperties
$BackupProperties.BackupPath = "\\fileshare\backups\NetworkController\$BackupTime"
$BackupProperties.Credential = $ShareCredential

$Backup = New-NetworkControllerBackup -ConnectionURI $URI -Credential $Credential -Properties $BackupProperties -ResourceId $BackupTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>Beispiel: Überprüfen des Status eines Sicherungsvorgangs für den Netzwerkcontroller

```Powershell
PS C:\ > Get-NetworkControllerBackup -ConnectionUri $URI -Credential $Credential -ResourceId $Backup.ResourceId
| ConvertTo-JSON -Depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerBackup/2017-04-25T16_53_13",
    "InstanceId":  "c3ea75ae-2892-4e10-b26c-a2243b755dc8",
    "Etag":  "W/\"0dafea6c-39db-401b-bda5-d2885ded470e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-25T16_53_13",
    "Properties":  {
                    "BackupPath":  "\\\\fileshare\backups\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  "",
                    "FailedResourcesList":  [

                                            ],
                    "SuccessfulResourcesList":  [
                                                    "/networking/v1/credentials/11ebfc10-438c-4a96-a1ee-8a048ce675be",
                                                    "/networking/v1/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                                                    "/networking/v1/credentials/b2a82c93-2583-4a1f-91f8-232b801e11bb",
                                                    "/networking/v1/credentials/BackupUser",
                                                    "/networking/v1/credentials/fd5b1b96-b302-4395-b6cd-ed9703435dd1",
                                                    "/networking/v1/virtualNetworkManager/configuration",
                                                    "/networking/v1/virtualSwitchManager/configuration",
                                                    "/networking/v1/accessControlLists/f8b97a4c-4419-481d-b757-a58483512640",
                                                    "/networking/v1/logicalnetworks/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8",
                                                    "/networking/v1/logicalnetworks/48610528-f40b-4718-938e-99c2be76f1e0",
                                                    "/networking/v1/logicalnetworks/89035b49-1ee3-438a-8d7a-f93cbae40619",
                                                    "/networking/v1/logicalnetworks/a9c8eaa0-519c-4988-acd6-11723e9efae5",
                                                    "/networking/v1/logicalnetworks/d4ea002c-c926-4c57-a178-461d5768c31f",
                                                    "/networking/v1/macPools/11111111-1111-1111-1111-111111111111",
                                                    "/networking/v1/loadBalancerManager/config",
                                                    "/networking/v1/publicIPAddresses/2c502b2d-b39a-4be1-a85a-55ef6a3a9a1d",
                                                    "/networking/v1/GatewayPools/Default",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8056-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8057-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5910-8056-b4c04f395931",
                                                    "/networking/v1/networkInterfaces/058430d3-af43-4328-a440-56540f41da50",
                                                    "/networking/v1/networkInterfaces/08756090-6d55-4dec-98d5-80c4c5a47db8",
                                                    "/networking/v1/networkInterfaces/2175d74a-aacd-44e2-80d3-03f39ea3bc5d",
                                                    "/networking/v1/networkInterfaces/2400c2c3-2291-4b0b-929c-9bb8da55851a",
                                                    "/networking/v1/networkInterfaces/4c695570-6faa-4e4d-a552-0b36ed3e0962",
                                                    "/networking/v1/networkInterfaces/7e317638-2914-42a8-a2dd-3a6d966028d6",
                                                    "/networking/v1/networkInterfaces/834e3937-f43b-4d3c-88be-d79b04e63bce",
                                                    "/networking/v1/networkInterfaces/9d668fe6-b1c6-48fc-b8b1-b3f98f47d508",
                                                    "/networking/v1/networkInterfaces/ac4650ac-c3ef-4366-96e7-d9488fb661ba",
                                                    "/networking/v1/networkInterfaces/b9f23e35-d79e-495f-a1c9-fa626b85ae13",
                                                    "/networking/v1/networkInterfaces/fdd929f1-f64f-4463-949a-77b67fe6d048",
                                                    "/networking/v1/virtualServers/15a891ee-7509-4e1d-878d-de0cb4fa35fd",
                                                    "/networking/v1/virtualServers/57416993-b410-44fd-9675-727cd4e98930",
                                                    "/networking/v1/virtualServers/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a",
                                                    "/networking/v1/virtualServers/6c812217-5931-43dc-92a8-1da3238da893",
                                                    "/networking/v1/virtualServers/d78b7fa3-812d-4011-9997-aeb5ded2b431",
                                                    "/networking/v1/virtualServers/d90820a5-635b-4016-9d6f-bf3f1e18971d",
                                                    "/networking/v1/loadBalancerMuxes/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d78b7fa3-812d-4011-9997-aeb5ded2b431_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d90820a5-635b-4016-9d6f-bf3f1e18971d_suffix",
                                                    "/networking/v1/Gateways/15a891ee-7509-4e1d-878d-de0cb4fa35fd_suffix",
                                                    "/networking/v1/Gateways/57416993-b410-44fd-9675-727cd4e98930_suffix",
                                                    "/networking/v1/Gateways/6c812217-5931-43dc-92a8-1da3238da893_suffix",
                                                    "/networking/v1/virtualNetworks/b3dbafb9-2655-433d-b47d-a0e0bbac867a",
                                                    "/networking/v1/virtualNetworks/d705968e-2dc2-48f2-a263-76c7892fb143",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.2",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.3",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.4"
                                                ],
                    "InProgressResourcesList":  [

                                                ],
                    "ProvisioningState":  "Succeeded",
                    "Credential":  {
                                        "Tags":  null,
                                        "ResourceRef":  "/credentials/BackupUser",
                                        "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                        "Etag":  null,
                                        "ResourceMetadata":  null,
                                        "ResourceId":  null,
                                        "Properties":  null
                                    }
                }
}
```

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>Wiederherstellen der SDN-Infrastruktur aus einer Sicherung

Wenn Sie alle erforderlichen Komponenten aus einer Sicherung wiederherstellen, gibt die SDN-Umgebung in einen funktionsfähigen Zustand zurück.  

>[!IMPORTANT]
>Die Schritte variieren abhängig von der Anzahl von Komponenten, die wiederhergestellt werden.


1. Bei Bedarf erneut bereitstellen Sie, Hyper-V-Hosts und den erforderlichen Speicher.

2. Bei Bedarf stellen die Netzwerkcontroller-VMs, die RAS-Gateway-VMs und virtuellen Mux-Computern aus einer Sicherung wieder her. 

3. Stop-NC-Host-Agent und die SLB-Host-Agent auf allen Hyper-V-Hosts:

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS-Gateway-VMs zu beenden.

5. Beenden Sie die SLB/Mux-VMs.

6. Wiederherstellen des Netzwerkcontrollers mit der `new-networkcontrollerrestore` Cmdlet.

7. Überprüfen Sie die Wiederherstellung **ProvisioningState** wissen, wann die Wiederherstellung erfolgreich abgeschlossen wurde.

8. Wenn Sie SCVMM zu verwenden, Wiederherstellen der VMM-Datenbank mithilfe der Sicherung, die zur gleichen Zeit wie die Sicherung des Netzwerkcontrollers erstellt wurde.

9. Wenn Sie die Workload-VMs aus einer Sicherung wiederherstellen möchten, tun Sie dies jetzt.

10. Überprüfen Sie die Integrität Ihres Systems mit dem Debug-Networkcontrollerconfigurationstate-Cmdlet.

```Powershell
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController "https://NC.contoso.com" -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

### <a name="example-restoring-a-network-controller-database"></a>Beispiel: Wiederherstellen einer Datenbank für den Netzwerkcontroller
 
```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

$ShareUserResourceId = "BackupUser"
$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }

$RestoreProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerRestoreProperties
$RestoreProperties.RestorePath = "\\fileshare\backups\NetworkController\2017-04-25T16_53_13"
$RestoreProperties.Credential = $ShareCredential

$RestoreTime = (Get-Date).ToString("s").Replace(":", "_")
New-NetworkControllerRestore -ConnectionURI $URI -Credential $Credential -Properties $RestoreProperties -ResourceId $RestoreTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>Beispiel: Überprüfen des Status der Wiederherstellung einer dem Netzwerkcontroller

```PowerShell
PS C:\ > get-networkcontrollerrestore -connectionuri $uri -credential $cred -ResourceId $restoreTime | convertto-json -depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerRestore/2017-04-26T15_04_44",
    "InstanceId":  "22edecc8-a613-48ce-a74f-0418789f04f6",
    "Etag":  "W/\"f14f6b84-80a7-4b73-93b5-59a9c4b5d98e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-26T15_04_44",
    "Properties":  {
                    "RestorePath":  "\\\\sa18fs\\sa18n22\\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  null,
                    "FailedResourcesList":  null,
                    "SuccessfulResourcesList":  null,
                    "ProvisioningState":  "Succeeded",
                    "Credential":  null
                }
}
```


Weitere Informationen zur Konfiguration von zustandsmeldungen, die angezeigt werden kann, finden Sie unter [Problembehandlung beim Windows Server 2016 Software definiert Networking-Stapel](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack).