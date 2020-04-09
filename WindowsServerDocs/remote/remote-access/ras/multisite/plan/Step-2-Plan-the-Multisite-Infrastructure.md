---
title: Schritt 2 Planen der Infrastruktur für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 64c10107-cb03-41f3-92c6-ac249966f574
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 61d4faafa91a685cad50b4f47aaad8efd9b9a500
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858343"
---
# <a name="step-2-plan-the-multisite-infrastructure"></a>Schritt 2 Planen der Infrastruktur für mehrere Standorte

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der nächste Schritt beim Bereitstellen des Remote Zugriffs in einer Topologie mit mehreren Standorten besteht darin, die Infrastrukturplanung für mehrere Standorte abzuschließen. einschließlich, Active Directory, Sicherheitsgruppen und Gruppenrichtlinie Objekten.  
## <a name="21-plan-active-directory"></a><a name="bkmk_2_1_AD"></a>2,1 Plan Active Directory  
Eine Remote Zugriffs Bereitstellung für mehrere Standorte kann in einer Reihe von Topologien konfiguriert werden:  
  
-   **Einzelne Active Directory Site, mehrere Einstiegspunkte**: in dieser Topologie verfügen Sie über einen einzelnen Active Directory Standort für Ihre gesamte Organisation mit schnellen intranetverknüpfungen auf der gesamten Website, aber Sie verfügen über mehrere RAS-Server, die in ihrer gesamten Organisation bereitgestellt werden, die jeweils als Einstiegspunkt fungieren. Ein geografisches Beispiel für diese Topologie ist die Verwendung einer einzelnen Active Directory Site für die USA mit Einstiegspunkten an der Ostküste und der Westküste.  
  
    ![Infrastruktur für mehrere Standorte](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo1.png)  
  
-   **Mehrere Active Directory Standorte, mehrere Einstiegspunkte**: in dieser Topologie verfügen Sie über zwei oder mehr Active Directory Standorte mit einem Remote Zugriffs Server, die als Einstiegspunkt für jeden Standort bereitgestellt werden. Jeder RAS-Server ist dem Active Directory Domänen Controller für den Standort zugeordnet. Ein geografisches Beispiel für diese Topologie ist die Verwendung einer Active Directory Site für die USA und eines für Europa mit einem einzelnen Einstiegspunkt für jeden Standort. Beachten Sie Folgendes: Wenn Sie über mehrere Active Directory Standorte verfügen, benötigen Sie keinen Einstiegspunkt, der mit jedem Standort verknüpft ist. Außerdem können einigen Active Directory Websites mehrere Einstiegspunkte zugeordnet werden.  
  
    ![Topologie mit mehreren Standorten](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo2.png)  
  
An einem Einstiegspunkt mit mehreren Standorten können Sie einen einzelnen RAS-Server, mehrere RAS-Server oder einen Remote Zugriffs Server-Cluster konfigurieren.   
  
### <a name="active-directory-best-practices-and-recommendations"></a>Bewährte Methoden und Empfehlungen Active Directory  
Beachten Sie die folgenden Empfehlungen und Einschränkungen für Active Directory-Bereitstellung in einem Szenario mit mehreren Standorten:  
  
1.  Jede Active Directory Site kann einen oder mehrere RAS-Server oder einen Server Cluster enthalten, der als Einstiegspunkte für mehrere Standorte für Client Computer fungiert. Es ist jedoch nicht erforderlich, dass eine Active Directory Site einen Einstiegspunkt hat.  
  
2.  Ein Einstiegspunkt mit mehreren Standorten kann nur einer einzelnen Active Directory Site zugeordnet werden. Wenn auf Client Computern, auf denen Windows 8 ausgeführt wird, eine Verbindung mit einem bestimmten Einstiegspunkt hergestellt wird, werden Sie als zu der Active Directory Site, die dem Einstiegspunkt zugeordnet ist, als  
  
3.  Es wird empfohlen, dass jeder Active Directory Standort über einen Domänen Controller verfügt. Der Domänen Controller kann schreibgeschützt sein.  
  
4.  Wenn jeder Active Directory Standort einen Domänen Controller enthält, wird das Gruppenrichtlinien Objekt für einen Server im Einstiegspunkt von einem der Domänen Controller in der Active Directory Site verwaltet, die dem Endpunkt zugeordnet ist. Wenn an diesem Standort keine Domänen Controller mit aktiviertem Schreibzugriff vorhanden sind, wird das Gruppenrichtlinien Objekt für einen Server auf einem Domänen Controller mit aktiviertem Schreibzugriff verwaltet, der dem ersten Remote Zugriffs Server am nächsten liegt, der im Einstiegspunkt konfiguriert ist. Der nächstgelegene Wert wird durch eine Berechnung der Link Kosten festgelegt. Beachten Sie, dass in diesem Szenario nach dem vornehmen von Konfigurationsänderungen bei der Replikation zwischen dem Domänen Controller, der das Gruppenrichtlinien Objekt verwaltet, und dem schreibgeschützten Domänen Controller auf dem Active Directory Standort des Servers eine Verzögerung auftreten kann.  
  
5.  Client-Gruppenrichtlinien Objekte und optionale Anwendungsserver-Gruppenrichtlinien Objekte werden auf dem Domänen Controller verwaltet, der als primärer Domänen Controller Emulator (PDC) ausgeführt wird. Dies bedeutet, dass Client-Gruppenrichtlinien Objekte nicht notwendigerweise an der Active Directory Site verwaltet werden, die den Einstiegspunkt enthält, mit dem Clients eine Verbindung herstellen.  
  
6.  Wenn der Domänen Controller für einen Active Directory Standort nicht erreichbar ist, stellt der RAS-Server eine Verbindung mit einem alternativen Domänen Controller am Standort her (falls verfügbar). Wenn dies nicht der Fall ist, wird eine Verbindung mit dem Domänen Controller eines anderen Standorts hergestellt, um ein aktualisiertes GPO abzurufen und Clients zu authentifizieren. In beiden Fällen können die Remote Zugriffs-Verwaltungskonsole und die PowerShell-Cmdlets nicht zum Abrufen oder Ändern von Konfigurationseinstellungen verwendet werden, bis der Domänen Controller verfügbar ist. Beachten Sie Folgendes:  
  
    1.  Wenn der Server, auf dem der PDC-Emulator ausgeführt wird, nicht verfügbar ist, müssen Sie einen verfügbaren Domänen Controller mit aktualisierten GPOs als PDC-Emulator angeben.  
  
    2.  Wenn der Domänen Controller, von dem ein Server-Gruppenrichtlinien Objekt verwaltet wird, nicht verfügbar ist, verwenden Sie das PowerShell-Cmdlet Set-daentrypointdc, um einen neuen Domänen Controller dem Einstiegspunkt zuzuordnen. Der neue Domänen Controller muss vor dem Ausführen des Cmdlets über aktuelle GPOs verfügen.  
  
## <a name="22-plan-security-groups"></a><a name="bkmk_2_2_SG"></a>2,2 Planen von Sicherheitsgruppen  
Während der Bereitstellung eines einzelnen Servers mit erweiterten Einstellungen wurden alle Client Computer, die über DirectAccess auf das interne Netzwerk zugreifen, in einer Sicherheitsgruppe gesammelt. Bei einer Bereitstellung mit mehreren Standorten wird diese Sicherheitsgruppe nur für Windows 8-Client Computer verwendet. Bei einer Bereitstellung mit mehreren Standorten werden Windows 7-Client Computer für jeden Einstiegspunkt in der Bereitstellung für mehrere Standorte in separaten Sicherheitsgruppen erfasst. Wenn Sie z. b. zuvor alle Client Computer in der Gruppe DA_Clients gruppiert haben, müssen Sie jetzt alle Windows 7-Computer aus dieser Gruppe entfernen und Sie in einer anderen Sicherheitsgruppe platzieren. Beispielsweise erstellen Sie in der Topologie mehrere Einstiegspunkte für mehrere Active Directory Standorte eine Sicherheitsgruppe für den USA Einstiegspunkt (DA_Clients_US) und einen für den Einstiegspunkt Europa (DA_Clients_Europe). Platzieren Sie alle Windows 7-Client Computer, die sich in der USA befinden, in der Gruppe DA_Clients_US und alle, die sich in Europa in der DA_Clients_Europe Gruppe befinden. Wenn Sie über keine Windows 7-Client Computer verfügen, müssen Sie keine Sicherheitsgruppen für Windows 7-Computer planen.  
  
Die folgenden Sicherheitsgruppen sind erforderlich:  
  
-   Eine Sicherheitsgruppe für alle Windows 8-Client Computer. Es wird empfohlen, für jede Domäne eine eindeutige Sicherheitsgruppe für diese Clients zu erstellen.  
  
-   Eine eindeutige Sicherheitsgruppe, die Windows 7-Client Computer für jeden Einstiegspunkt enthält. Es wird empfohlen, für jede Domäne eine eindeutige Gruppe zu erstellen. Beispiel: domain1 \ DA_Clients_Europe; Domäne2 \ DA_Clients_Europe; Domain1 \ DA_Clients_US; Domäne2 \ DA_Clients_US.  
  
## <a name="23-plan-group-policy-objects"></a><a name="bkmk_2_3_GPO"></a>2,3 planen Gruppenrichtlinie Objekte  
DirectAccess-Einstellungen, die während der Remote Zugriffs Bereitstellung konfiguriert werden, werden in GPOs gesammelt. Ihre Einzel Server Bereitstellung verwendet bereits GPOs für DirectAccess-Clients, den Remote Zugriffs Server und optional für Anwendungsserver. Für eine Bereitstellung mit mehreren Standorten sind folgende Gruppenrichtlinien Objekte erforderlich:  
  
-   Ein Server-GPO für jeden Einstiegspunkt.  
  
-   Ein Gruppenrichtlinien Objekt für jede Domäne mit Client Computern, auf denen Windows 8 ausgeführt wird.  
  
-   Ein Gruppenrichtlinien Objekt für jeden Einstiegspunkt und jede Domäne, die Windows 7-Client Computer enthält.  
  
GPOs können wie folgt konfiguriert werden:  
  
-   **Automatisch**: Sie können angeben, dass GPOs automatisch durch den Remote Zugriff erstellt werden. Für jedes GPO wird ein Standardname angegeben, der geändert werden kann.  
  
-   **Manuell**: Sie können Gruppenrichtlinien Objekte verwenden, die vom Active Directory-Administrator manuell erstellt wurden.  
  
> [!NOTE]  
> Wenn DirectAccess für die Verwendung bestimmter Gruppenrichtlinien Objekte konfiguriert ist, kann es nicht für die Verwendung unterschiedlicher GPOs konfiguriert werden.  
  
### <a name="231-automatically-created-gpos"></a>2.3.1 automatisch erstellte Gruppenrichtlinien Objekte  
Beachten Sie beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Automatisch erstellte Gruppenrichtlinienobjekte werden entsprechend des Speicherorts und Verknüpfungszielparameters wie folgt angewendet:  
  
    -   Für das Server-Gruppenrichtlinien Objekt zeigen der Speicherort und die Verknüpfungs Parameter auf die Domäne, die den Remote Zugriffs Server enthält.  
  
    -   Für Client-Gruppenrichtlinien Objekte wird das Verknüpfungs Ziel auf den Stamm der Domäne festgelegt, in der das Gruppenrichtlinien Objekt erstellt wurde. Für jede Domäne, die Client Computer enthält, wird ein Gruppenrichtlinien Objekt erstellt, und das Gruppenrichtlinien Objekt wird mit dem Stamm der einzelnen Domänen verknüpft. .  
  
-   Für automatisch erstellte Gruppenrichtlinien Objekte benötigt der RAS-Server Administrator die folgenden Berechtigungen, um DirectAccess-Einstellungen anzuwenden:  
  
    -   Berechtigungen zum Erstellen von Gruppenrichtlinien Objekten für erforderliche Domänen.  
  
    -   Verknüpfungsberechtigungen für alle ausgewählten Clientdomänenstämme.  
  
    -   Die Berechtigung zum Erstellen des WMI-Filters für GPOs ist erforderlich, wenn DirectAccess nur für mobile Computer konfiguriert wurde.  
  
    -   Link Berechtigungen für die Stämme von Domänen, die den Einstiegspunkten zugeordnet sind (die Server-GPO-Domänen)  
  
    -   Es wird empfohlen, dass der Remotezugriffsadministrator über Leserechte für Gruppenrichtlinienobjekte für jede Domäne verfügt. Dadurch wird der Remote Zugriff aktiviert, um sicherzustellen, dass GPOs mit doppelten Namen beim Erstellen von Gruppenrichtlinien Objekten für die Bereitstellung für mehrere Standorte nicht vorhanden sind.  
  
    -   Active Directory Replikations Berechtigungen für Domänen, die Einstiegspunkten zugeordnet sind. Dies liegt daran, dass beim ersten Hinzufügen von Einstiegspunkten das Server-GPO für den Einstiegspunkt auf dem Domänen Controller erstellt wird, der diesem Einstiegspunkt am nächsten ist. Da die Verknüpfungs Erstellung jedoch nur auf dem PDC-Emulator unterstützt wird, muss das Gruppenrichtlinien Objekt vom Domänen Controller, auf dem es erstellt wurde, auf den Domänen Controller repliziert werden, auf dem der PDC-Emulator ausgeführt wird, bevor der Link erstellt wird  
  
Beachten Sie, dass eine Warnung ausgegeben wird, wenn die richtigen Berechtigungen für die Replikation und verknüpfte Gruppenrichtlinien Objekte nicht vorhanden sind. Der Remote Zugriffs Vorgang wird fortgesetzt, die Replikation und Verknüpfung werden jedoch nicht ausgeführt. Wenn eine Link Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, auch nachdem die Berechtigungen vorhanden sind. Stattdessen muss der Administrator die Links manuell erstellen.  
  
### <a name="232-manually-created-gpos"></a>manuell erstellte Gruppenrichtlinien Objekte  
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Die folgenden Gruppenrichtlinien Objekte sollten für die Bereitstellung für mehrere Standorte manuell erstellt werden:  
  
    -   **Server-GPO**: ein Server-Gruppenrichtlinien Objekt für jeden Einstiegspunkt (in der Domäne, in der sich der Einstiegspunkt befindet). Dieses GPO wird auf jedem RAS-Server im Einstiegspunkt angewendet.  
  
    -   **Client-GPO (Windows 7)** : ein Gruppenrichtlinien Objekt für jeden Einstiegspunkt und jede Domäne mit Windows 7-Client Computern, die eine Verbindung zu Einstiegspunkten in der Bereitstellung für mehrere Standorte herstellen. Zum Beispiel domain1 \ DA_W7_Clients_GPO_Europe; Domäne2 \ DA_W7_Clients_GPO_Europe; Domain1 \ DA_W7_Clients_GPO_US; Domäne2 \ DA_W7_Clients_GPO_US. Wenn keine Windows 7-Client Computer eine Verbindung mit Einstiegspunkten herstellen, sind GPOs nicht erforderlich.  
  
-   Es ist nicht erforderlich, zusätzliche GPOs für Windows 8-Client Computer zu erstellen. Ein Gruppenrichtlinien Objekt für jede Domäne, die Client Computer enthält, wurde bereits erstellt, als der einzelne RAS-Server bereitgestellt wurde. Bei einer Bereitstellung mit mehreren Standorten fungieren diese Client-Gruppenrichtlinien Objekte als GPOs für Windows 8-Clients.  
  
-   Die GPOs sollten vorhanden sein, bevor Sie in den Bereitstellungs-Assistenten für mehrere Standorte auf die Schaltfläche Commit klicken  
  
-   Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte wird in der gesamten Domäne eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
-   Wenn Sie die DirectAccess-Einstellungen mithilfe von manuell erstellten Gruppenrichtlinien Objekten anwenden, benötigt der RAS-Server Administrator vollständige GPO-Berechtigungen (bearbeiten, löschen, Ändern der Sicherheit) für die manuell erstellten Gruppenrichtlinien Objekte.  
  
Beachten Sie, dass eine Warnung ausgegeben wird, wenn die richtigen Berechtigungen für die Replikation und verknüpfte Gruppenrichtlinien Objekte nicht vorhanden sind. Der Remote Zugriffs Vorgang wird fortgesetzt, die Replikation und Verknüpfung werden jedoch nicht ausgeführt. Wenn eine Link Warnung ausgegeben wird, werden Verknüpfungen nicht automatisch erstellt, auch nachdem die Berechtigungen vorhanden sind. Stattdessen muss der Administrator die Links manuell erstellen.  
  
### <a name="233-managing-gpos-in-a-multi-domain-controller-environment"></a>2.3.3 Verwalten von Gruppenrichtlinien Objekten in einer Umgebung mit mehreren Domänen Controllern  
Jedes GPO wird von einem bestimmten Domänen Controller wie folgt verwaltet:  
  
-   Das Server-Gruppenrichtlinien Objekt wird von einem der Domänen Controller an der Active Directory Site verwaltet, die dem Server zugeordnet ist, oder, wenn Domänen Controller an diesem Standort schreibgeschützt sind, von einem schreibgeschützten Domänen Controller, der dem ersten Server am Einstiegspunkt am nächsten ist.  
  
-   Client-Gruppenrichtlinien Objekte werden vom Domänen Controller verwaltet, der als PDC-Emulator ausgeführt wird.  
  
Beachten Sie Folgendes, wenn Sie GPO-Einstellungen manuell ändern möchten:  
  
-   Führen Sie für Server-Gruppenrichtlinien Objekte das PowerShell-Cmdlet `Get-DAEntryPointDC -EntryPointName <name of entry point>`aus, um zu ermitteln, welcher Domänen Controller mit einem bestimmten Einstiegspunkt verknüpft ist.  
  
-   Wenn Sie mit den PowerShell-Cmdlets für Netzwerke oder der Gruppenrichtlinie Management Console Änderungen vornehmen, wird standardmäßig der Domänen Controller verwendet, der als PDC-Emulator fungiert.  
  
-   Beachten Sie Folgendes, wenn Sie Einstellungen auf einem Domänen Controller ändern, bei dem es sich nicht um den Domänen Controller handelt, der dem Einstiegspunkt (für Server-Gruppenrichtlinien Objekte) oder dem PDC-Emulator (für Client-GPOs) zugeordnet ist:  
  
    1.  Stellen Sie vor dem Ändern der Einstellungen sicher, dass der Domänen Controller mit einem aktuellen GPO repliziert wird, und [Sichern Sie GPO-Einstellungen](https://go.microsoft.com/fwlink/?LinkID=257928), bevor Sie Änderungen vornehmen. Wenn das Gruppenrichtlinien Objekt nicht aktualisiert wird, können Konflikte bei der Replikation auftreten, was zu einer beschädigten Remote Zugriffs Konfiguration führt.  
  
    2.  Nachdem Sie die Einstellungen geändert haben, müssen Sie darauf warten, dass die Änderungen auf den Domänen Controller repliziert werden, der den Gruppenrichtlinien Objekten zugeordnet ist. Nehmen Sie keine weiteren Änderungen mithilfe der Remote Zugriffs-Verwaltungskonsole oder PowerShell-Cmdlets für den Remote Zugriff vor, bis die Replikation beendet ist. Wenn ein Gruppenrichtlinien Objekt auf zwei verschiedenen Domänen Controllern bearbeitet wird, bevor die Replikation beendet ist, können Mergekonflikte auftreten, was zu einer beschädigten Konfiguration führt.  
  
-   Alternativ können Sie die Standardeinstellung im Dialogfeld **Domänen Controller ändern** in der Gruppenrichtlinie-Verwaltungskonsole oder mithilfe des PowerShell-Cmdlets **Open-netgpo** ändern, damit Änderungen, die über die-Konsole oder die-Cmdlets für Netzwerke vorgenommen wurden, den von Ihnen angegebenen Domänen Controller verwenden.  
  
    1.  Klicken Sie hierzu in der Gruppenrichtlinie-Verwaltungskonsole mit der rechten Maustaste auf den Domänen-oder Standort Container, und klicken Sie dann auf **Domänen Controller ändern**.  
  
    2.  Geben Sie in PowerShell den Parameter Domain Controller für das Cmdlet Open-netgpo an. Wenn Sie z. b. die privaten und öffentlichen Profile in der Windows-Firewall auf einem Gruppenrichtlinien Objekt mit dem Namen domain1 \ DA_Server_GPO _Europe mit einem Domänen Controller namens Europe-DC.Corp.contoso.com aktivieren möchten, gehen Sie wie folgt vor:  
  
        ```  
        $gpoSession = Open-NetGPO -PolicyStore "domain1\DA_Server_GPO _Europe" -DomainController "europe-dc.corp.contoso.com"  
        Set-NetFirewallProfile -GpoSession $gpoSession -Name @("Private","Public") -Enabled True  
        Save-NetGPO -GpoSession $gpoSession  
        ```  
  
#### <a name="modifying-domain-controller-association"></a>Ändern der Domänen Controller Zuordnung  
Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. In einigen Szenarien kann es erforderlich sein, einen anderen Domänen Controller für ein GPO zuzuweisen:  
  
-   **Wartung und Ausfall von Domänen Controllern**: Wenn der Domänen Controller, von dem ein Gruppenrichtlinien Objekt verwaltet wird, nicht verfügbar ist, kann es erforderlich sein, das GPO auf einem anderen Domänen Controller zu verwalten.  
  
-   **Optimierung der Konfigurations Verteilung**: nach der Änderung der Netzwerkinfrastruktur ist es möglicherweise erforderlich, das Server-Gruppenrichtlinien Objekt eines Einstiegs Punkts auf einem Domänen Controller an demselben Active Directory Standort wie den Einstiegspunkt zu verwalten.   
  
## <a name="24-plan-dns"></a><a name="bkmk_2_4_DNS"></a>2,4 Planen des DNS  
Beachten Sie beim Planen von DNS für eine Bereitstellung mit mehreren Standorten Folgendes:  
  
1.  Client Computer verwenden die ConnectTo-Adresse, um eine Verbindung mit dem Remote Zugriffs Server herzustellen. Für jeden Einstiegspunkt in der Bereitstellung ist eine andere ConnectTo-Adresse erforderlich. Jeder Einstiegspunkt "ConnectTo Address" muss im öffentlichen DNS verfügbar sein, und die von Ihnen gewählte Adresse muss mit dem Antragsteller Namen des IP-HTTPS-Zertifikats, das Sie für die IP-HTTPS-Verbindung bereitstellen, identisch sein.   
  
2.  Außerdem erzwingt der Remote Zugriff das symmetrische Routing. Daher können nur Teredo-und IP-HTTPS-Clients eine Verbindung herstellen, wenn eine Bereitstellung für mehrere Standorte aktiviert ist. Damit systemeigene IPv6-Clients eine Verbindung herstellen können, muss die ConnectTo-Adresse (die IP-HTTPS-URL) sowohl in die externen IPv6-und IPv4-Adressen des Remote Zugriffs Servers aufgelöst werden.  
  
3.  RAS erstellt einen Standard-Webtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Konnektivität zum internen Netzwerk zu prüfen. Während der Konfiguration des einzelnen Servers sollten die folgenden Namen in DNS registriert werden:  
  
    1.  DirectAccess-WebProbe Host: sollte in die interne IPv4-Adresse des RAS-Servers oder die IPv6-Adresse in einer reinen IPv6-Umgebung aufgelöst werden.  
  
    2.  DirectAccess-corpconnectivityhost: sollte in eine localhost-Adresse (Loopback) aufgelöst werden (entweder: 1 oder 127.0.0.1, je nachdem, ob IPv6 im Unternehmensnetzwerk bereitgestellt wird).  
  
    Bei einer Bereitstellung für mehrere Standorte muss für jeden Einstiegspunkt ein zusätzlicher DNS-Eintrag für DirectAccess-WebProbe Host erstellt werden. Beim Hinzufügen eines Einstiegs Punkts versucht der Remote Zugriff, diesen zusätzlichen DirectAccess-WebProbe Host-Eintrag automatisch zu erstellen. Wenn dies jedoch nicht möglich ist, wird eine Warnung angezeigt, und Sie müssen den Eintrag manuell erstellen.  
  
    > [!NOTE]  
    > Wenn DNS-Bereinigung in Ihrer DNS-Infrastruktur aktiviert ist, wird empfohlen, das Bereinigung für die DNS-Einträge zu deaktivieren, die automatisch durch den Remote Zugriff erstellt werden.  
  

  



