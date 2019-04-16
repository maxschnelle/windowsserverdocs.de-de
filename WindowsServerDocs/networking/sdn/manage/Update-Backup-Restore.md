---
title: Update, Sicherung und Wiederherstellung Software Defined Networking-Infrastruktur
description: "Dieses Thema ist Teil der Software Defined Networking-Anleitung für Updates, Sicherung und Wiederherstellung SDN-Infrastruktur in Windows Server2016."
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: grcusanz
ms.openlocfilehash: bb7194ec865db980962853b87d68a84a5446269e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="update-backup-and-restore-software-defined-networking-infrastructure"></a>Update, Sicherung und Wiederherstellung Software Defined Networking-Infrastruktur

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält die folgenden Abschnitte.

- [Aktualisierung der SDN-Infrastruktur](#bkmk_Updating)
- [Sicherung der SDN-Infrastruktur](#bkmk_backup)
- [Die SDN-Infrastruktur aus einer Sicherung wiederherstellen](#bkmk_restore)

## <a name="bkmk_Updating"></a>Aktualisierung der SDN-Infrastruktur

Aktualisierung ist die Installation von Windows-Updates auf alle Komponenten des Betriebssystems des Systems Software Defined Networking (SDN).  Dazu gehören die SDN Hyper-V-Hosts, Netzwerk-Controller-VMs, Software Load Balancer Mux VMs und RAS-Gateway-VMs aktiviert.  Es ist wichtig, dass alle diese Komponenten genau dieselben Updates installiert haben.  Wenn Sie System Center Virtual Machine Manager verwendet wird, es wird empfohlen, dass Sie auch sie mit der neuesten Updaterollups auch aktualisieren.

Aktualisieren der einzelnen Komponenten erfolgt mithilfe der standardmäßigen Methoden für die Installation von Windows-Updates, jedoch die Schritteim folgenden beschrieben, muss eingegeben werden, um sicherzustellen, dass minimaler Downtime für Arbeitsauslastungen, und die Integrität der Datenbank Netzwerkcontroller.

### <a name="step-1-update-the-management-consoles"></a>Schritt1: Aktualisieren der Verwaltungskonsolen
Installieren Sie erforderlichen Updates auf jedem der Computer an, in dem Sie das Netzwerk-Controller-PowerShell-Modul verwenden.  Dazu gehören eine beliebige Stelle, dass Sie die Remoteserver-Verwaltungstools NetworkController Rolle selbst installiert haben.  Dies ist nicht einschließlich der Netzwerk-Controller-VMs selbst, wie sie in Schritt2 aktualisiert werden.

### <a name="step-2-update-the-network-controllers"></a>Schritt2: Aktualisieren Sie die Netzwerkcontroller
Dies ist der wichtigste Schrittden Updatezyklus, da jede virtuelle Maschine Netzwerk-Controller aktualisiert werden muss und werden im Cluster Netzwerkcontroller vor dem Fortfahren mit dem nächsten vollständig wieder online.

Starten Sie mit einem Netzwerk-Controller-VM, und installieren Sie alle erforderlichen Updates zu.  Starten Sie den virtuellen Computer ggf. neu.

Bevor Sie mit der nächsten Network Controller virtuellen Maschine verwendet werden Get-Networkcontrollernode zum Überprüfen des Status des Knotens, der aktualisiert wurde, und neu gestartet.  Warten Sie, bis der Netzwerkcontroller Knoten ausfallen, die während des Neustartzyklus und kehren dann wieder nach oben erneut.  Nach dem Neustart des virtuellen Computers kann es einige Minuten wieder in den Zustand von Position dennoch.

#### <a name="example-using-get-networkcontrollernode-to-check-the-status-of-network-controller-nodes"></a>Beispiel: Get-Networkcontrollernode zum Überprüfen des Status von Netzwerkcontroller Knoten verwenden

Dieses Beispiel zeigt die Ausgabe von Get-Networkcontrollernode von innerhalb der Netzwerk-Controller-VMs ausführen.  Es zeigt, dass NCNode1.contoso.com ausgefallen ist, während die anderen beiden Knoten fehlerfrei sind.  Sie müssen warten, zu mehreren Minuten dauern, bis der Status für diesen Knoten ändert einrichten, bevor Sie mit allen zusätzlichen Knoten aktualisieren.

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

Nur nach allen Netzwerk-Controller-Knoten in den Schaltflächenzustand befinden, können Sie diese Schrittefür jeden zusätzlichen Netzwerkcontroller Knoten wiederholen?  Fahren Sie mit jeder Knoten gleichzeitig zu aktualisieren.

Nachdem alle Knoten Netzwerkcontroller aktualisiert werden, aktualisiert der Netzwerkcontroller die Microservices innerhalb des Clusters Netzwerkcontroller innerhalb einer Stunde ausgeführt.  Sie können eine sofortige Aktualisierung mit dem Cmdlet Update-Networkcontroller auslösen.

#### <a name="example-using-update-networkcontroller-to-force-network-controller-to-update"></a>Beispiel: Verwenden von Update-Networkcontroller Netzwerkcontroller aktualisieren erzwingen

Dieser Befehl zeigt das Ergebnis des Update-Networkcontroller, wenn nicht noch um zu installierende Updates vorhanden sind.

```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

### <a name="step-3-update-slb-muxes"></a>Schritt3: Update SLB Muxes

Installieren Sie Updates auf jeder SLB Mux virtuelle Computer eine zu einem Zeitpunkt um fortlaufende Verfügbarkeit der Load Balancer Infrastruktur sicherzustellen.

### <a name="step-4-update-hyper-v-hosts-and-ras-gateways"></a>Schritt4: Update Hyper-V-Hosts und RAS-Gateways

Da der RAS-Gateway-VMs live ohne Verlust von Verbindungen Mandanten migriert werden kann, muss darauf geachtet werden um die Anzahl, wie oft die Mandanten zu minimieren, die Verbindungen zu einem neuen RAS-Gateways bei der Aktualisierung ein Failover werden.  Durch das Aktualisieren der Hosts und RAS-Gateways koordinieren jeder Mandant nur einen höchstens einmal Failover.  

Gehen Sie für jeden Host, beginnend mit den Hosts, die den RAS-Gateways enthalten, die in den Standby-Modus sind folgendermaßen vor:

1.  Verlassen Sie den Host der virtuellen Maschinen, die Livemigration fähig sind.  RAS-Gateway-VMs sollte auf dem Host bleiben.
2.  Installieren von Updates auf jede Gateway-VM auf diesem Host.
3.  Aktualisieren der Gateway-VM neu erfordert dann einen Neustart des virtuellen Computers.  
4.  Installieren Sie Updates auf dem Host mit dem Gateway-VM, der gerade aktualisiert wurde.
5.  Der Server neu gestartet, wenn die Updates erforderlich.
6.  Wiederholen Sie für jeden zusätzlichen Host mit einem Standby-Gateway.  Wenn keine Standby-Gateways bleiben, folgen Sie dann dieselben Schrittefür alle verbleibenden Hosts.

## <a name="bkmk_backup"></a>Sicherung der SDN-Infrastruktur

Regelmäßige Sicherungen der Netzwerk-Controller-Datenbank sind entscheidend für die Geschäftskontinuität bei einem Notfall oder Datenverlust.  Sichern der Netzwerk-Controller virtueller Computer ist nicht ausreichend, da es nicht gewährleistet, dass mehrere Netzwerkcontroller Knoten, wenn das Quorum aufrechterhalten wird.
Anforderungen:
 * Eine SMB-Freigabe und Anmeldeinformationen mit Lese- und Schreibberechtigungen für die Freigabe und das Dateisystem.
 * Wenn Sie den Netzwerk-Controller installiert wurde, verwenden ein GMSA auch, können Sie optional eine Gruppe Managed Service Account (GMSA) verwenden.

Zum Ausführen einer Sicherung, gehen Sie wie folgt vor:

1. Sichern Sie die Netzwerk-Controller virtuellen Maschinen, die mit der VM-Backup-Methode Ihrer Wahl, oder verwenden Sie Hyper-V So exportieren Sie eine Kopie jedes virtuellen Computers Netzwerk-Controller.  Dadurch wird sichergestellt, dass eine vollständige Wiederherstellung einschließlich Wiederherstellung der Infrastruktur virtueller Computer ausgeführt wird, die erforderlichen Zertifikate für die Entschlüsselung der Datenbank vorhanden sind.
2. Wenn Sie System Center Virtual Machine Manager (SCVMM) verwenden, beenden Sie den SCVMM-Dienst, und Sichern sie Sie über SQL Server ausführt, um sicherzustellen, dass keine Updates zu SCVMM während dieses Zeitraums vorgenommen werden, der eine Inkonsistenz zwischen dem Netzwerkcontroller Sicherung und SCVMM erstellt werden konnte.  Den SCVMM-Dienst nicht neu gestartet, bis zum Abschluss der Sicherung Netzwerkcontroller wurde.
3. Sichern Sie die neue Networkcontrollerbackup mit Netzwerkcontroller-Datenbank.

 #### <a name="example-backing-up-the-network-controller-database"></a>Beispiel: Sichern der Netzwerk-Controller-Datenbank
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

4. Verwenden Sie Get-Networkcontrollerbackup, um nach Abschluss des Vorgangs und Erfolg der Sicherung suchen.

 #### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>Beispiel: Überprüfen des Status eines Sicherungsvorgangs Netzwerkcontroller

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

5.  Bei Verwendung von SCVMM können Sie jetzt SCVMM-Dienst starten.

## <a name="bkmk_restore"></a>Die SDN-Infrastruktur aus einer Sicherung wiederherstellen

Wiederherstellung ist der Prozess der Wiederherstellung alle erforderlichen Komponenten aus der Sicherung auf eine SDN-Umgebung in einen betriebsbereiten Zustand zurück.  Die Schrittevariieren etwas abhängig von der Komponenten, die wiederhergestellt werden.

1. Bei Bedarf erneut bereitstellen Sie, Hyper-V-Hosts und den erforderlichen Speicher.

2. Falls erforderlich, Wiederherstellen Sie Netzwerk-Controller-VMs, RAS-Gateway-VMs und Mux-VMs aus einer Sicherung. 

3. Beenden Sie NC-Host-Agent und SLB Host-Agent auf allen Hyper-V-Hosts

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. Beenden des RAS-Gateway-VMs

5. Beenden Sie SLB Mux-VMs

6. Wiederherstellen der Netzwerk-Controller mit dem neuen Networkcontrollerrestore-Cmdlet.

 #### <a name="example-restoring-a-network-controller-database"></a>Beispiel: Die Wiederherstellung einer Datenbank Netzwerkcontroller
 
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

7. Überprüfen Sie die Wiederherstellung ProvisioningState bekannt sein, wenn die Wiederherstellung erfolgreich abgeschlossen wurde.

 #### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>Beispiel: Überprüfen des Status der Wiederherstellung einer Netzwerkcontroller

    ```
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

8. Bei Verwendung von SCVMM Wiederherstellen der SCVMM-Datenbank mithilfe der Sicherung, die gleichzeitig als Netzwerkcontroller Sicherung erstellt wurde.

9. Wenn virtuellen aus einer Sicherung wiederhergestellt werden, können Sie dies jetzt tun.

10. Verwenden Sie das Cmdlet "Debug-Networkcontrollerconfigurationstate", um die Integrität Ihres Systems zu überprüfen.

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

Informationen zu Konfiguration Meldungen, die möglicherweise angezeigt werden, finden Sie unter [Problembehandlung bei der Windows Server2016 Software definierten-Netzwerkstapel](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack).