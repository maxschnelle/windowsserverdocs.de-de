---
title: Erstellen von Sicherheitsrichtlinien mit erweiterten Port-Zugriffssteuerungslisten
description: Dieses Thema enthält Informationen zu erweiterten Port Access Control Listen (ACLs) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-hv-switch
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a92e61c3-f7d4-4e42-8575-79d75d05a218
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2beb4ec1d78200b5c62d18ffb3f935843bd12ae0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308020"
---
# <a name="create-security-policies-with-extended-port-access-control-lists"></a>Erstellen von Sicherheitsrichtlinien mit erweiterten Port-Zugriffssteuerungslisten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zu erweiterten Port Access Control Listen (ACLs) in Windows Server 2016. Sie können erweiterte ACLs für den virtuellen Hyper-V-Switch konfigurieren, um Netzwerkdatenverkehr an die und von den virtuellen Computern (VMs), die über virtuelle Netzwerkadapter mit dem Switch verbunden sind, zuzulassen und zu blockieren.  
  
Dieses Thema enthält folgende Abschnitte:  
  
-   [Detaillierte ACL-Regeln](#bkmk_detailed)  
  
-   [Zustands behaftete ACL-Regeln](#bkmk_stateful)  
  
## <a name="detailed-acl-rules"></a><a name="bkmk_detailed"></a>Detaillierte ACL-Regeln  
Erweiterte ACLs für den virtuellen Hyper-v-Switch ermöglicht Ihnen das Erstellen detaillierter Regeln, die Sie auf einzelne VM-Netzwerkadapter anwenden können, die mit dem virtuellen Hyper-v-Switch verbunden sind. Durch die Möglichkeit, ausführliche Regeln zu erstellen, können Unternehmen und clouddienstanbieter (Cloud Service Providers, CSPs) netzwerkbasierte Sicherheitsbedrohungen in einer mehrinstanzfähigen freigegebenen Serverumgebung lösen.  
  
Mit erweiterten ACLs müssen Sie nicht allgemeine Regeln erstellen, mit denen der gesamte Datenverkehr über alle Protokolle an einen bzw. von einem virtuellen Computer blockiert oder zugelassen wird. Stattdessen können Sie jetzt den Netzwerkdatenverkehr über einzelne auf den virtuellen Computern ausgeführte Protokolle blockieren oder zulassen. Sie können erweiterte ACL-Regeln in Windows Server 2016 erstellen, die die folgenden 5-Tupel-Parameter enthalten: Quell-IP-Adresse, Ziel-IP-Adresse, Protokoll, Quellport und Zielport. Darüber hinaus kann in jeder Regel die Richtung des Netzwerkdatenverkehrs (ein- oder ausgehend) und die von der Regel unterstützte Aktion (Blockieren oder Zulassen des Datenverkehrs) angegeben werden.  
  
Sie können beispielsweise Port-ACLs für einen virtuellen Computer konfigurieren, um den gesamten ein- und ausgehenden HTTP- und HTTPS-Datenverkehr an Port 80 zuzulassen und gleichzeitig den Netzwerkdatenverkehr aller anderen Protokolle an allen Ports blockieren.  
  
Durch diese Möglichkeit, den Protokolldatenverkehr festzulegen, der von virtuellen Mandantencomputern empfangen werden kann, gewinnen Sie Flexibilität beim Konfigurieren der Sicherheitsrichtlinien.  
  
### <a name="configuring-acl-rules-with-windows-powershell"></a>Konfigurieren von ACL-Regeln mit Windows PowerShell  
Zum Konfigurieren einer erweiterten ACL müssen Sie den Windows PowerShell-Befehl **Add-VMNetworkAdapterExtendedAcl** verwenden. Dieser Befehl verfügt über vier verschiedene Syntaxen mit jeweils unterschiedlicher Verwendung:  
  
1.  Fügen Sie allen Netzwerkadaptern einer benannten VM, die durch den ersten Parameter (-VMName) angegeben wird, eine erweiterte ACL hinzu. Syntax:  
  
    > [!NOTE]  
    > Wenn Sie einem Netzwerkadapter anstelle von "alle" eine erweiterte ACL hinzufügen möchten, können Sie den Netzwerkadapter mit dem Parameter "-vmnetworkadaptername" angeben.  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMName] <string[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny}  
        [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
2.  Hinzufügen einer erweiterten ACL zu einem bestimmten virtuellen Netzwerkadapter auf einem bestimmten virtuellen Computer. Syntax:  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMNetworkAdapter] <VMNetworkAdapterBase[]> [-Action]  
        <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound |  
        Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort]  
        <string>] [[-Protocol] <string>] [-Weight] <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID  
        <int>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
3.  Hinzufügen einer erweiterten ACL zu allen virtuellen Netzwerkadaptern, die für die Verwendung durch das Hyper-V-Hostverwaltungs-Betriebssystem reserviert sind.  
  
    > [!NOTE]  
    > Wenn Sie einem Netzwerkadapter anstelle von "alle" eine erweiterte ACL hinzufügen möchten, können Sie den Netzwerkadapter mit dem Parameter "-vmnetworkadaptername" angeben.  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction]  
        <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress]  
        <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight] <int> -ManagementOS  
        [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName <string>]  
        [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
4.  Hinzufügen einer erweiterten ACL zu einem VM-Objekt, das Sie in Windows PowerShell erstellt haben, z. b. **$VM = Get-VM "my_vm"** . In der nächsten Codezeile können Sie diesen Befehl mit der folgenden Syntax ausführen, um eine erweiterte ACL zu erstellen:  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VM] <VirtualMachine[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow |  
        Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
### <a name="detailed-acl-rule-examples"></a>Beispiele für detaillierte ACL-Regeln  
In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **Add-VMNetworkAdapterExtendedAcl** zum Konfigurieren erweiterter Port-ACLs und zum Erstellen von Sicherheitsrichtlinien für virtuelle Computer verwenden können.  
  
-   [Erzwingen der Sicherheit auf Anwendungsebene](#bkmk_enforce)  
  
-   [Erzwingen der Sicherheit auf Benutzer-und Anwendungsebene](#bkmk_both)  
  
-   [Bereitstellen von Sicherheitsunterstützung für eine nicht-TCP/UDP-Anwendung](#bkmk_tcp)  
  
> [!NOTE]  
> Die Werte für den Regelparameter **Richtung** in den folgenden Tabellen basieren auf dem Fluss des Datenverkehrs zu dem bzw. von dem virtuellen Computer, für den Sie die Regel erstellen. Wenn der virtuelle Computer Datenverkehr empfängt, handelt es sich um eingehenden Datenverkehr. Wenn vom virtuellen Computer Datenverkehr gesendet wird, handelt es sich um ausgehenden Datenverkehr. Wenn Sie beispielsweise eine Regel auf einen virtuellen Computer anwenden, mit der eingehender Datenverkehr blockiert wird, verläuft die Richtung des eingehenden Datenverkehrs von externen Ressourcen zum virtuellen Computer. Wenn Sie eine Regel anwenden, mit der ausgehender Datenverkehr blockiert wird, verläuft die Richtung des ausgehenden Datenverkehrs vom lokalen virtuellen Computer zu den externen Ressourcen.  
  
### <a name="enforce-application-level-security"></a><a name="bkmk_enforce"></a>Erzwingen der Sicherheit auf Anwendungsebene  
Da von vielen Anwendungsservern für die Kommunikation mit Clientcomputern standardisierte TCP/UDP-Ports verwendet werden, können Sie leicht Regeln erstellen, mit denen der Zugriff auf einen Anwendungsserver blockiert wird, indem der Datenverkehr zu dem bzw. von dem für die Anwendung festgelegten Port gefiltert wird.  
  
Beispielsweise können Sie einem Benutzer die Anmeldung bei einem Anwendungsserver im Datencenter über eine Remotedesktopverbindung (Remote Desktop Connection, RDP) ermöglichen. Da für RDP der TCP-Port 3389 verwendet wird, können Sie schnell die folgende Regel einrichten:  
  
|Quell-IP|Ziel-IP|Protokoll|Quellport|Zielport|Richtung|Aktion|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|TCP|*|3389|Im|Zulassen|  
  
In den beiden folgenden Beispielen wird gezeigt, wie Sie mit Windows PowerShell-Befehlen Regeln erstellen können. Die erste Beispiel Regel blockiert den gesamten Datenverkehr an den virtuellen Computer mit dem Namen "ApplicationServer". Die zweite Beispiel Regel, die auf den Netzwerkadapter des virtuellen Computers mit dem Namen "ApplicationServer" angewendet wird, ermöglicht nur eingehenden RDP-Datenverkehr an den virtuellen Computer.  
  
> [!NOTE]  
> Wenn Sie Regeln erstellen, können Sie mit dem Parameter **-Weight** die Reihenfolge bestimmen, in der die Regeln vom virtuellen Hyper-V-Switch verarbeitet werden. Werte für **-Weight** werden als ganze Zahlen ausgedrückt. Regeln mit einer höheren Ganzzahl werden vor Regeln mit niedrigeren Ganzzahlen verarbeitet. Wenn Sie beispielsweise zwei Regeln auf den Netzwerkadapter eines virtuellen Computers angewendet haben (eine mit der Gewichtung 1 und eine mit der Gewichtung 10), wird die Regel mit der Gewichtung 10 zuerst angewendet.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Inbound" -LocalPort 3389 -Protocol "TCP" -Weight 10  
```  
  
### <a name="enforce-both-user-level-and-application-level-security"></a><a name="bkmk_both"></a>Erzwingen der Sicherheit auf Benutzer-und Anwendungsebene  
Da mit einer Regel ein 5-Tupel-IP-Paket (Quell-IP, Ziel-IP, Protokoll, Quellport und Zielport) verglichen werden kann, kann mit der Regel eine detailliertere Sicherheitsrichtlinie erzwungen werden als mit einer Port-ACL.  
  
Wenn Sie beispielsweise einen DHCP-Dienst für eine begrenzte Anzahl von Client Computern mithilfe einer bestimmten Gruppe von DHCP-Servern bereitstellen möchten, können Sie auf dem Windows Server 2016-Computer, auf dem Hyper-V ausgeführt wird, auf dem die Benutzer-VMS gehostet werden, die folgenden Regeln konfigurieren:  
  
|Quell-IP|Ziel-IP|Protokoll|Quellport|Zielport|Richtung|Aktion|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|255.255.255.255|UDP|*|67|Heraus|Zulassen|  
|*|10.175.124.0/25|UDP|*|67|Heraus|Zulassen|  
|10.175.124.0/25|*|UDP|*|68|Im|Zulassen|  
  
In den folgenden Beispielen wird gezeigt, wie Sie diese Regeln mit Windows PowerShell-Befehlen erstellen können.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 255.255.255.255 -RemotePort 67 -Protocol "UDP"-Weight 10  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 67 -Protocol "UDP"-Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 68 -Protocol "UDP"-Weight 20  
```  
  
### <a name="provide-security-support-to-a-non-tcpudp-application"></a><a name="bkmk_tcp"></a>Bereitstellen von Sicherheitsunterstützung für eine nicht-TCP/UDP-Anwendung  
Während der größte Teil des Netzwerkdatenverkehrs in einem Datacenter über TCP und UDP erfolgt, werden dennoch für einen Teil des Datenverkehrs andere Protokolle genutzt. Wenn Sie beispielsweise zulassen möchten, dass auf einer Gruppe von Servern eine IP-Multicastanwendung ausgeführt wird, die auf IGMP (Internet Group Management-Protokoll) basiert, können Sie die folgende Regel erstellen.  
  
> [!NOTE]  
> Für IGMP ist die IP-Protokollnummer 0x02 festgelegt.  
  
|Quell-IP|Ziel-IP|Protokoll|Quellport|Zielport|Richtung|Aktion|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|0x02|*|*|Im|Zulassen|  
|*|*|0x02|*|*|Heraus|Zulassen|  
  
Im folgenden Beispiel wird gezeigt, wie Sie diese Regeln mit Windows PowerShell-Befehlen erstellen können.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -Protocol 2 -Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -Protocol 2 -Weight 20  
```  
  
## <a name="stateful-acl-rules"></a><a name="bkmk_stateful"></a>Zustands behaftete ACL-Regeln  
Eine weitere neue Funktion der erweiterten ACLs ermöglicht das Konfigurieren zustandsbehafteter Regeln. Eine Zustands behaftete Regel filtert Pakete basierend auf fünf Attributen in einer Paket Quell-IP, Ziel-IP, Protokoll, Quellport und Zielport.  
  
Zustandsbehaftete Regeln haben die folgenden Funktionen:  
  
-   Sie lassen Datenverkehr immer zu und werden nicht zum Blockieren von Datenverkehr verwendet.  
  
-   Wenn Sie für den Parameter **Direction** den Wert %%amp;quot;inbound%%amp;quot; angeben und Datenverkehr der Regel entspricht, wird vom virtuellen Hyper-V-Switch eine entsprechende Regel erstellt, mit der das Senden von ausgehendem Datenverkehr durch den virtuellen Computer als Antwort an die externe Ressource zugelassen wird.  
  
-   Wenn Sie für den Parameter **Direction** den Wert %%amp;quot;outbound%%amp;quot; angeben und Datenverkehr der Regel entspricht, wird vom virtuellen Hyper-V-Switch dynamisch eine entsprechende Regel erstellt, mit der der Empfang von eingehendem Datenverkehr von der externen Ressource auf dem virtuellen Computer zugelassen wird.  
  
-   Dazu gehört ein Timeoutattribut, das in Sekunden gemessen wird. Wenn beim Switch ein Netzwerkpaket eingeht, das einer zustandsbehafteten Regel entspricht, wird vom virtuellen Hyper-V-Switch ein Zustand erstellt, damit alle nachfolgenden Pakete in beiden Richtungen des gleichen Flusses zugelassen werden. Der Zustand läuft ab, wenn in dem durch den Timeoutwert angegebenen Zeitraum kein Datenverkehr in einer der Richtungen auftritt.  
  
Im folgenden Beispiel wird gezeigt, wie Sie zustandsbehaftete Regeln verwenden können.  
  
### <a name="allow-inbound-remote-server-traffic-only-after-it-is-contacted-by-the-local-server"></a>Zulassen von eingehendem Datenverkehr von einem Remoteserver nur nach einer Kontaktaufnahme durch den lokalen Server  
In manchen Fällen muss eine zustandsbehaftete Regel verwendet werden, da nur mit dieser eine bekannte, hergestellte Verbindung nachverfolgt und von anderen Verbindungen unterschieden werden kann.  
  
Wenn Sie beispielsweise zulassen möchten, dass von einem Anwendungsserver für virtuelle Computer an Port 80 Verbindungen mit Webdiensten im Internet initiiert werden und Antworten der Remotewebserver auf den Datenverkehr des virtuellen Computers möglich sein sollen, können Sie eine zustandsbehaftete Regel konfigurieren. In dieser lassen Sie anfänglichen ausgehenden Datenverkehr vom virtuellen Computer zu den Webdiensten zu. Da die Regel zustandsbehaftet ist, wird auch der Antwortdatenverkehr vom virtuellen Computer an die Webserver zugelassen. Aus Sicherheitsgründen können Sie den gesamten eingehenden Netzwerkdatenverkehr an den virtuellen Computer blockieren.  
  
Für diese Regelkonfiguration können Sie die Einstellungen aus der folgenden Tabelle verwenden.  
  
> [!NOTE]  
> Aufgrund von Formatierungseinschränkungen und der Menge der Informationen in der folgenden Tabelle werden die Informationen anders angezeigt als in den vorherigen Tabellen dieses Dokuments.  
  
|Parameter|Regel 1|Regel 2|Regel 3|  
|-------------|----------|----------|----------|  
|Quell-IP|*|*|*|  
|Ziel-IP|*|*|*|  
|Protokoll|*|*|TCP|  
|Quellport|*|*|*|  
|Zielport|*|*|80|  
|Richtung|Im|Heraus|Heraus|  
|Aktion|Verweigern|Verweigern|Zulassen|  
|Zustandsbehaftet|Nein|Nein|Ja|  
|Timeout (in Sekunden)|N/V|N/V|3600|  
  
Mit der zustandsbehafteten Regel wird zugelassen, dass über den Anwendungsserver für virtuelle Computer eine Verbindung mit einem Remotewebserver hergestellt wird. Wenn das erste Paket gesendet wird, werden vom virtuellen Hyper-V-Switch dynamisch zwei Flusszustände erstellt, um alle an den Remotewebserver gesendeten und von diesem zurückgesendeten Pakete zuzulassen. Wenn der Fluss der Pakete zwischen den Servern endet, tritt für die Flusszustände ein Timeout gemäß dem festgelegten Timeoutwert von 3600 Sekunden (oder einer Stunde) auf.  
  
Im folgenden Beispiel wird gezeigt, wie Sie diese Regeln mit Windows PowerShell-Befehlen erstellen können.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1   
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Outbound" 80 "TCP" -Weight 100 -Stateful -Timeout 3600  
```  
  


