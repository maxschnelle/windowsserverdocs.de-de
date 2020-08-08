---
title: Aktualisieren, sichern und Wiederherstellen der Sdn-Infrastruktur
description: In diesem Thema erfahren Sie, wie Sie eine Sdn-Infrastruktur aktualisieren, sichern und wiederherstellen.
manager: grcusanz
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/27/2018
ms.openlocfilehash: daca883456a32c707fc2c7b9bfd6193b0d917b58
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942580"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>Aktualisieren, sichern und Wiederherstellen der Sdn-Infrastruktur

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie eine Sdn-Infrastruktur aktualisieren, sichern und wiederherstellen.

## <a name="upgrade-the-sdn-infrastructure"></a>Aktualisieren der Sdn-Infrastruktur
Die Sdn-Infrastruktur kann von Windows Server 2016 auf Windows Server 2019 aktualisiert werden. Führen Sie für die Aktualisierungs Reihenfolge die gleichen Schritte wie im Abschnitt "Aktualisieren der Sdn-Infrastruktur" aus. Vor dem Upgrade wird empfohlen, eine Sicherung der Netzwerk Controller-Datenbank durchzuführen.

Verwenden Sie für Netzwerk Controller Computer das Get-networkcontrollernode-Cmdlet, um den Status des Knotens zu überprüfen, nachdem das Upgrade abgeschlossen wurde. Stellen Sie sicher, dass der Knoten in den Status "up" zurückkehrt, bevor Sie die anderen Knoten aktualisieren. Nachdem Sie alle Netzwerk Controller Knoten aktualisiert haben, aktualisiert der Netzwerk Controller die im Netzwerk Controller Cluster laufenden Mikro Dienste innerhalb einer Stunde. Mithilfe des Cmdlets "Update-networkcontroller" können Sie ein sofortiges Update ausführen.

Installieren Sie dieselben Windows-Updates auf allen Betriebssystemkomponenten des SDN-Systems (Software Defined Networking), das Folgendes umfasst:

- SDN-aktivierte Hyper-V-Hosts
- Netzwerk Controller-VMS
- Software Load Balancer MUX-VMS
- RAS-Gateway-VMS

>[!IMPORTANT]
>Wenn Sie System Center Virtual Manager verwenden, müssen Sie es mit den aktuellen Updaterollups aktualisieren.

Wenn Sie jede Komponente aktualisieren, können Sie eine der Standardmethoden zum Installieren von Windows-Updates verwenden. Führen Sie die folgenden Schritte aus, um eine minimale Ausfallzeit für Workloads und die Integrität der Netzwerk Controller-Datenbank sicherzustellen:

1. Aktualisieren Sie die Verwaltungs Konsolen.<p>Installieren Sie die Updates auf allen Computern, auf denen das PowerShell-Modul des Netzwerk Controllers verwendet wird.  Dies ist auch der Ort, an dem die RSAT-networkcontroller-Rolle selbst installiert ist. Ausschließen der Netzwerk Controller-VMs selbst Sie aktualisieren Sie im nächsten Schritt.

2. Installieren Sie auf der ersten Netzwerk Controller-VM alle Updates, und starten Sie neu.

3. Stellen Sie vor dem Fortfahren mit dem nächsten virtuellen Netzwerk Controller-Computer mit dem `get-networkcontrollernode` Cmdlet den Status des von Ihnen aktualisierten und neu gestarteten Knotens fest.

4. Warten Sie, bis der Netzwerk Controller Knoten herunterfährt, und wiederholen Sie dann den Neustart Vorgang.<p>Nachdem Sie den virtuellen Computer neu gestartet haben, kann es einige Minuten dauern, **_bis_** der Status wieder hergestellt ist. Ein Beispiel für die Ausgabe finden Sie unter.

5. Installieren Sie Updates nacheinander auf Jeder SLB MUX-VM, um die kontinuierliche Verfügbarkeit der Load Balancer-Infrastruktur sicherzustellen.

6. Aktualisieren Sie Hyper-V-Hosts und RAS-Gateways, beginnend mit den Hosts, die die RAS- **Standby** Gateways im Standbymodus enthalten.<p>RAS-Gateway-VMs können ohne Verlust von Mandanten Verbindungen nicht Live migriert werden. Während des Aktualisierungsprozesses müssen Sie darauf achten, wie oft das Failover von Mandanten Verbindungen auf ein neues RAS-Gateway minimiert wird. Durch koordinieren der Aktualisierung von Hosts und RAS-Gateways führt jeder Mandant höchstens ein Failover durch.

    a. Evakuieren Sie den Host von virtuellen Computern, die eine Live Migration durchführen können.<p>RAS-Gateway-VMS sollten auf dem Host verbleiben.

    b. Installieren Sie Updates auf jeder gatewayvm auf diesem Host.

    c. Wenn für das Update der Gateway-VM neu gestartet werden muss, starten Sie den virtuellen Computer neu.

    d. Installieren Sie Updates auf dem Host, der die soeben aktualisierte Gateway-VM enthält.

    e. Starten Sie den Host neu, wenn dies für die Updates erforderlich ist.

    f. Wiederholen Sie diesen Vorgang für jeden zusätzlichen Host mit einem Standby-Gateway.<p>Wenn keine Standby-Gateways verbleiben, führen Sie die gleichen Schritte für alle verbleibenden Hosts aus.


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>Beispiel: Verwenden des Cmdlets "Get-networkcontrollernode"

In diesem Beispiel sehen Sie, dass die Ausgabe für das `get-networkcontrollernode` Cmdlet auf einem der Netzwerk Controller-VMS ausgeführt wird.

Der Status der Knoten, die in der Beispielausgabe angezeigt werden, lautet:

- NCNode1.contoso.com = nach unten
- NCNode2.contoso.com = aufwärts
- NCNode3.contoso.com = aufwärts

>[!IMPORTANT]
>Sie müssen einige Minuten warten, bis sich der Status des Knotens in " _**hoch**_ " ändert, bevor Sie zusätzliche Knoten nacheinander aktualisieren.

Nachdem Sie alle Netzwerk Controller Knoten aktualisiert haben, aktualisiert der Netzwerk Controller die im Netzwerk Controller Cluster laufenden Mikro Dienste innerhalb einer Stunde.

>[!TIP]
>Sie können ein sofortiges Update mit dem- `update-networkcontroller` Cmdlet ausführen.


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

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>Beispiel: Verwenden des Cmdlets "Update-networkcontroller"
In diesem Beispiel sehen Sie die Ausgabe für das `update-networkcontroller` Cmdlet, um die Aktualisierung des Netzwerk Controllers zu erzwingen.

>[!IMPORTANT]
>Führen Sie dieses Cmdlet aus, wenn keine weiteren Updates installiert werden müssen.


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>Sichern der Sdn-Infrastruktur

Durch reguläre Sicherungen der Netzwerk Controller-Datenbank wird die Geschäftskontinuität im Fall eines Notfalls oder eines Daten Verlusts sichergestellt.  Das Sichern der Netzwerk Controller-VMS ist nicht ausreichend, weil dadurch nicht sichergestellt wird, dass die Sitzung über mehrere Netzwerk Controller Knoten hinweg fortgesetzt wird.

**Anforderungen:**
* Eine SMB-Freigabe und Anmelde Informationen mit Lese-/Schreibberechtigungen für die Freigabe und das Dateisystem.
* Sie können optional ein Gruppen verwaltetes Dienst Konto (Group Managed Service Account, GMSA) verwenden, wenn der Netzwerk Controller auch mit einem GMSA installiert wurde.

**Dringlichkeit**

1. Verwenden Sie die Sicherungsmethode der VM Ihrer Wahl, oder verwenden Sie Hyper-V, um eine Kopie der einzelnen Netzwerk Controller-VMS zu exportieren.<p>Beim Sichern der Netzwerk Controller-VM wird sichergestellt, dass die erforderlichen Zertifikate zum Entschlüsseln der Datenbank vorhanden sind.

2. Wenn Sie System Center Virtual Machine Manager (SCVMM) verwenden, wird der SCVMM-Dienst angehalten und über SQL Server gesichert.<p>Das Ziel besteht darin, sicherzustellen, dass während dieser Zeit keine Updates an SCVMM vorgenommen werden, was zu einer Inkonsistenz zwischen der Sicherung des Netzwerk Controllers und SCVMM führen könnte.

   >[!IMPORTANT]
   >Starten Sie den SCVMM-Dienst erst neu, wenn die Sicherung des Netzwerk Controllers beendet ist.

3. Sichern Sie die Netzwerk Controller-Datenbank mit dem- `new-networkcontrollerbackup` Cmdlet.

4. Überprüfen Sie den Abschluss und den Erfolg der Sicherung mit dem- `get-networkcontrollerbackup` Cmdlet.

5. Wenn Sie SCVMM verwenden, starten Sie den SCVMM-Dienst.



### <a name="example-backing-up-the-network-controller-database"></a>Beispiel: Sichern der Netzwerk Controller-Datenbank

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

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>Beispiel: Überprüfen des Status eines Sicherungs Vorgangs für den Netzwerk Controller

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

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>Wiederherstellen der Sdn-Infrastruktur aus einer Sicherung

Wenn Sie alle erforderlichen Komponenten aus der Sicherung wiederherstellen, wird die Sdn-Umgebung in einen Betriebsstatus zurückversetzt.

>[!IMPORTANT]
>Die Schritte variieren in Abhängigkeit von der Anzahl der wiederhergestellten Komponenten.


1. Stellen Sie ggf. Hyper-V-Hosts und den erforderlichen Speicher erneut bereit.

2. Stellen Sie ggf. die Netzwerk Controller-VMS, RAS-Gateway-VMS und MUX-VMS aus der Sicherung wieder her.

3. Den NC-Host-Agent und den SLB-Host-Agent auf allen Hyper-V-Hosts:

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. Beendet RAS-Gateway-VMS.

5. Beendet SLB MUX-VMS.

6. Stellen Sie den Netzwerk Controller mit dem- `new-networkcontrollerrestore` Cmdlet wieder her.

7. Überprüfen Sie den Restore **provisioningstate** , um zu ermitteln, wann die Wiederherstellung erfolgreich abgeschlossen wurde.

8. Wenn Sie SCVMM verwenden, stellen Sie die SCVMM-Datenbank mithilfe der Sicherung wieder her, die zur gleichen Zeit wie die Sicherung des Netzwerk Controllers erstellt wurde.

9. Wenn Sie Arbeits Auslastungs-VMS aus einer Sicherung wiederherstellen möchten, tun Sie dies jetzt.

10. Überprüfen Sie die Integrität Ihres Systems mit dem Cmdlet "Debug-networkcontrollerconfigurationstate".

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

### <a name="example-restoring-a-network-controller-database"></a>Beispiel: Wiederherstellen einer Netzwerk Controller-Datenbank

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

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>Beispiel: Überprüfen des Status einer Netzwerk Controller-Daten Bank Wiederherstellung

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


Informationen zu den möglicherweise angezeigten Konfigurations Zustands Meldungen finden Sie unter Problembehandlung [beim Software-Defined Networking-Stapel von Windows Server 2016](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack).