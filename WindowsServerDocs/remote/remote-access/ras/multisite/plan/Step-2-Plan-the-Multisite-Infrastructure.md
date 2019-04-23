---
title: Schritt 2 Planen der Infrastruktur für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64c10107-cb03-41f3-92c6-ac249966f574
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 771df80fc3130b5c4c03bf628a95d67b7df04b36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888201"
---
# <a name="step-2-plan-the-multisite-infrastructure"></a>Schritt 2 Planen der Infrastruktur für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Der nächste Schritt im Bereitstellen des Remotezugriffs in einer Topologie für mehrere Standorte ist zum Abschließen der Planung der Infrastruktur für mehrere Standorte. wie z.B., Active Directory-Sicherheitsgruppen und Gruppenrichtlinienobjekte.  
## <a name="bkmk_2_1_AD"></a>2.1 Planen von Active Directory  
Eine remotezugriffsbereitstellung für mehrere Standorte kann in einer Reihe von Topologien konfiguriert werden:  
  
-   **Einzelne Active Directory-Standort, der mehrere Einstiegspunkte**– In dieser Topologie haben Sie einen einzelnen Active Directory-Standort für Ihre gesamte Organisation mit schnellen Intranet-Links, die in der Website, aber Sie haben mehrere RAS-Server bereitgestellt in der gesamten Organisation, jede fungiert als Einstiegspunkt. Eine geografische Beispiel dieser Topologie ist einen einzelnen Active Directory-Standort für die USA Einstiegspunkte für die Ostküste und der Westküste haben.  
  
    ![Infrastruktur für mehrere Standorte](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo1.png)  
  
-   **Mehrere Active Directory-Standorte, mehrere Einstiegspunkte**– In dieser Topologie haben Sie zwei oder mehr Active Directory-Standorte mit einem RAS-Server, die als Einstiegspunkt für jeden Standort bereitgestellt. Jeder RAS-Server, die mit dem Active Directory-Domänencontroller für den Standort zugeordnet ist. Eine geografische Beispiel dieser Topologie ist Active Directory-Standort für die USA und eine für "Europa" mit einem einzelnen Einstiegspunkt für die einzelnen Standorte verfügen. Beachten Sie, dass wenn Sie über mehrere Active Directory-Standorte verfügen Sie nicht benötigen, ein Einstiegspunkts an jedem Standort zugeordnet haben. Darüber hinaus können einige Active Directory-Standorten mehr als ein Einstiegspunkt zugeordnet haben.  
  
    ![-Topologie für mehrere Standorte](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo2.png)  
  
In einem Einstiegspunkt Sie können eine einzelne RAS-Server mehrere RAS-Server konfigurieren, oder RAS-Server-Clustern.   
  
### <a name="active-directory-best-practices-and-recommendations"></a>Active Directory best Practices und Empfehlungen  
Beachten Sie die folgenden Empfehlungen und Einschränkungen für die Active Directory-Bereitstellung in einem Szenario mit mehreren Standorten:  
  
1.  Jeder Active Directory-Standort kann es sich um eine oder mehrere RAS-Server oder einen Server-Cluster für mehrere Standorte Einstiegspunkte für Clientcomputer ordnungsgemäß enthalten. Active Directory-Standort ist jedoch nicht erforderlich, um ein Einstiegspunkt zu erhalten.  
  
2.  Ein Einstiegspunkt kann nur einen einzelnen Active Directory-Standort zugeordnet werden. Wenn Clientcomputer mit Windows 8 mit einem bestimmten Einstiegspunkt verbinden, gelten sie als zu dieser Einstiegspunkt zugeordneten Active Directory-Standort gehören.  
  
3.  Es wird empfohlen, dass jeder Active Directory-Standort ein Domänencontroller verfügt. Der Domänencontroller kann schreibgeschützt sein.  
  
4.  Wenn jeder Active Directory-Standort einen Domänencontroller enthält, wird das Gruppenrichtlinienobjekt für einen Server im Einstiegspunkt von einer der Domänencontroller in der Active Directory-Standort, der dem Endpunkt zugeordneten verwaltet. Wenn keine Domänencontroller mit aktiviertem Schreibzugriff in diesem Standort vorhanden sind, wird das Gruppenrichtlinienobjekt für einen Server auf einem Domänencontroller mit Schreibzugriff verwaltet, die mit der ersten RAS-Server am nächsten befindet, die in den Einstiegspunkt konfiguriert ist. Wird am nächsten gelegenen durch einen Link, der Berechnung Kosten bestimmt werden kann. Beachten Sie, dass in diesem Szenario wird nach dem Ändern der Konfiguration gibt es möglicherweise einer Verzögerung bei der Replikation zwischen dem Domänencontroller verwalten das GPO und dem schreibgeschützten Domänencontroller in Active Directory-Standort des Servers.  
  
5.  Client-Gruppenrichtlinienobjekte und optional Application Server, die GPOs auf dem Domänencontroller ausgeführt wird, wie des Emulators des primären-Domänencontrollers (PDC) verwaltet werden. Dies bedeutet, dass diese Gruppenrichtlinienobjekte werden nicht unbedingt in Active Directory-Standort, der den Einstiegspunkt enthält verwaltet Client an dem Clients eine Verbindung herstellen.  
  
6.  Wenn der Domänencontroller für Active Directory-Standort nicht erreichbar ist, wird der RAS-Server mit einem anderen Domänencontroller am Standort (sofern verfügbar) verbinden. Wenn dies nicht der Fall ist, wird er mit dem Domänencontroller für einen anderen Standort, um aktualisierte Gruppenrichtlinienobjekte zu empfangen und zum Authentifizieren von Clients eine Verbindung herstellt. In beiden Fällen kann die Remotezugriffs-Verwaltungskonsole und die PowerShell-Cmdlets verwendet werden, abrufen und Ändern von Konfigurationseinstellungen, bis der Domänencontroller verfügbar ist. Beachten Sie Folgendes:  
  
    1.  Wenn der Server ausgeführt wird, als PDC-Emulator nicht verfügbar ist, müssen Sie einen verfügbaren Domänencontroller festlegen, der als PDC-Emulator Gruppenrichtlinienobjekte aktualisiert wurde.  
  
    2.  Wenn der Domänencontroller, der einen Server-Gruppenrichtlinienobjekt verwaltet nicht verfügbar ist, verwenden Sie das Set-DAEntryPointDC-PowerShell-Cmdlet, um einen neuen Domänencontroller mit dem Einstiegspunkt zuzuordnen. Der neue Domänencontroller muss auf dem neuesten Stand Gruppenrichtlinienobjekte werden, vor dem Ausführen des Cmdlets.  
  
## <a name="bkmk_2_2_SG"></a>2.2 Planen von Sicherheitsgruppen  
Während der Bereitstellung eines einzelnen Servers mit erweiterten Einstellungen wurden alle Clientcomputer, die Zugriff auf das interne Netzwerk über DirectAccess in einer Sicherheitsgruppe erfasst. In einer Bereitstellung für mehrere Standorte wird dieser Sicherheitsgruppe für Windows 8-Clientcomputer verwendet. Bei einer Bereitstellung für mehrere Standorte werden Windows 7-Clientcomputer in separate Sicherheitsgruppen für jeden Einstiegspunkt in die Bereitstellung für mehrere Standorte gesammelt werden. Z. B. Wenn Sie zuvor alle Clientcomputer in der Gruppe DA_Clients gruppiert haben, müssen Sie jetzt entfernen alle Windows 7-Computer aus dieser Gruppe und platzieren Sie sie in einer anderen Sicherheitsgruppe. In der mehrere Active Directory-Standorte, z. B. Topologie für mehrere Einstiegspunkte, Sie erstellen eine Sicherheitsgruppe für den Einstiegspunkt für die USA (DA_Clients_US) und eine für den Einstiegspunkt für Europa (DA_Clients_Europe). Alle Windows 7-Clientcomputer in der United States in der Gruppe DA_Clients_US und alle befindet sich in "Europa" in der Gruppe DA_Clients_Europe zu platzieren. Wenn Sie keine Windows 7-Clientcomputer verfügen, müssen Sie keine Sicherheitsgruppen für Windows 7-Computer zu planen.  
  
Erforderlichen Sicherheitsgruppen lauten wie folgt aus:  
  
-   Eine Sicherheitsgruppe für alle Windows 8-Clientcomputer. Es wird empfohlen, um eine eindeutige Sicherheits-Gruppe für diese Clients für jede Domäne zu erstellen.  
  
-   Eine eindeutige Sicherheits-Gruppe, die Windows 7-Clientcomputer für jeden Einstiegspunkt enthält. Es wird empfohlen, um eine eindeutige Gruppe für jede Domäne erstellen. Zum Beispiel: Domain1\DA_Clients_Europe; Domain2\DA_Clients_Europe; Domain1\DA_Clients_US; Domain2\DA_Clients_US.  
  
## <a name="bkmk_2_3_GPO"></a>2.3 Planen von Gruppenrichtlinienobjekten  
Während der Bereitstellung des Remotezugriffs konfigurierten DirectAccess-Einstellungen werden in GPOs gesammelt. Die Einzelserver-Bereitstellung bereits verwendet Gruppenrichtlinienobjekte für DirectAccess-Clients, die RAS-Server und optional für Anwendungsserver. Eine Bereitstellung für mehrere Standorte erfordert die folgenden Gruppenrichtlinienobjekte:  
  
-   Ein Server-Gruppenrichtlinienobjekt für jeden Einstiegspunkt.  
  
-   Ein Gruppenrichtlinienobjekt für jede Domäne, mit Windows 8-Clientcomputer enthalten.  
  
-   Ein Gruppenrichtlinienobjekt für jeden Einstiegspunkt und jede Domäne, die Windows 7-Clientcomputer enthalten.  
  
Gruppenrichtlinienobjekte können wie folgt konfiguriert werden:  
  
-   **Automatisch**– Sie können angeben, dass Gruppenrichtlinienobjekte automatisch vom Remotezugriff erstellt werden. Ein Standardname für jedes Gruppenrichtlinienobjekt angegeben ist, und kann geändert werden.  
  
-   **Manuell**– Sie können Gruppenrichtlinienobjekte verwenden, die von Active Directory-Administrator manuell erstellt wurden.  
  
> [!NOTE]  
> Nachdem DirectAccess Verwendung bestimmter Gruppenrichtlinienobjekte konfiguriert wurde, kann nicht es konfiguriert werden, um Gruppenrichtlinienobjekte zu verwenden.  
  
### <a name="231-automatically-created-gpos"></a>2.3.1 automatisch erstellter Gruppenrichtlinienobjekte  
Beachten Sie beim Verwenden automatisch erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Automatisch erstellte Gruppenrichtlinienobjekte werden entsprechend des Speicherorts und Verknüpfungszielparameters wie folgt angewendet:  
  
    -   Bei Gruppenrichtlinienobjekten des Servers zeigen den Speicherort und die Verknüpfungsparameter, auf die Domäne, die mit dem RAS-Server.  
  
    -   Für Client-Gruppenrichtlinienobjekte wird das Ziel des Links auf den Stamm der Domäne festgelegt, in dem das Gruppenrichtlinienobjekt erstellt wurde. Ein Gruppenrichtlinienobjekt erstellt für jede Domäne, die Clientcomputer enthält, und das Gruppenrichtlinienobjekt wird mit dem Stamm jeder Domäne verknüpft werden. .  
  
-   Für die automatisch erstellte Gruppenrichtlinienobjekte benötigt Serveradministrator zum Anwenden der DirectAccess-Einstellungen des RAS die folgenden Berechtigungen:  
  
    -   Berechtigungen für die erforderlichen Domänen für die Gruppenrichtlinienobjekte.  
  
    -   Verknüpfungsberechtigungen für alle ausgewählten Clientdomänenstämme.  
  
    -   Berechtigung zum Erstellen des WMI-Filters für Gruppenrichtlinienobjekte ist erforderlich, wenn DirectAccess konfiguriert wurde, um nur mobile Computer arbeiten.  
  
    -   Verknüpfungsberechtigungen für die Stämme von Domänen, die die Einstiegspunkte (die Server-GPO-Domänen) zugeordnet  
  
    -   Es wird empfohlen, dass der Remotezugriffsadministrator über Leserechte für Gruppenrichtlinienobjekte für jede Domäne verfügt. Dadurch werden Remote Access, um sicherzustellen, dass Gruppenrichtlinienobjekte mit doppelten Namen beim Erstellen von Gruppenrichtlinienobjekten für die Bereitstellung für mehrere Standorte nicht vorhanden.  
  
    -   Active Directory-Replikation-Berechtigungen für Domänen, die Einstiegspunkte zugeordnet. Dies ist, da beim Hinzufügen von Einstiegspunkten zunächst das Server-GPO für den Einstiegspunkt auf dem Domänencontroller, die am nächsten an dieser Einstiegspunkt erstellt wird. Allerdings da verknüpfungserstellung auf dem PDC-Emulator unterstützt wird, muss das Gruppenrichtlinienobjekt vom Domänencontroller repliziert werden auf dem sie mit dem Domänencontroller, der als PDC-Emulator ausgeführt wird, vor dem Erstellen des Links erstellt wurde.  
  
Beachten Sie, wenn die richtigen Berechtigungen für die Replikation und das Verknüpfen von Gruppenrichtlinienobjekten nicht vorhanden sind, eine Warnung ausgegeben wird. Der Remotezugriffsvorgang wird fortgesetzt, aber Replikation und das Verknüpfen erfolgt nicht. Wenn eine Warnung ausgegeben wird Verknüpfung wird Links nicht automatisch erstellt werden, auch nachdem die Berechtigungen vorhanden sind. Stattdessen muss der Administrator die Links manuell erstellen.  
  
### <a name="232-manually-created-gpos"></a>2.3.2 manuell erstellte Gruppenrichtlinienobjekte  
Beachten Sie beim Verwenden manuell erstellter Gruppenrichtlinienobjekte Folgendes:  
  
-   Die folgenden Gruppenrichtlinienobjekte sollte für die Bereitstellung für mehrere Standorte manuell erstellt werden:  
  
    -   **Server-Gruppenrichtlinienobjekt**– ein Server-Gruppenrichtlinienobjekt für jeden Einstiegspunkt (in der Domäne, in dem sich der Einstiegspunkt befindet). Dieses Gruppenrichtlinienobjekt wird auf jedem RAS-Server im Einstiegspunkt angewendet werden.  
  
    -   **Client-Gruppenrichtlinienobjekt (Windows 7)**– ein Gruppenrichtlinienobjekt für jeden Einstiegspunkt und jede Domäne, die mit Windows 7-Clientcomputer, die an Einstiegspunkte in die Bereitstellung mit mehreren Standorten eine Verbindung herstellen. Z. B. Domain1\DA_W7_Clients_GPO_Europe; Domain2\DA_W7_Clients_GPO_Europe; Domain1\DA_W7_Clients_GPO_US; Domain2\DA_W7_Clients_GPO_US. Wenn keine Windows 7-Clientcomputer auf Einstiegspunkte verbunden sind werden, sind die Gruppenrichtlinienobjekte nicht erforderlich.  
  
-   Es ist nicht erforderlich, die zusätzliche Gruppenrichtlinienobjekte für Windows 8-Client zu erstellen. Ein Gruppenrichtlinienobjekt für jede Domäne, die Clientcomputer enthalten wurde bereits erstellt, wenn der RAS-Servers bereitgestellt wurde. Diese Client-Gruppenrichtlinienobjekte funktionieren in einer Bereitstellung für mehrere Standorte wie die Gruppenrichtlinienobjekte für Windows 8-Clients verwendet wird.  
  
-   Die Gruppenrichtlinienobjekte sollten vorhanden sein, bevor Sie auf die Schaltfläche "Commit" in den Assistenten für die Bereitstellung für mehrere Standorte.  
  
-   Beim Verwenden manuell erstellter Gruppenrichtlinienobjekte wird in der gesamten Domäne eine Suche nach einer Verknüpfung zum Gruppenrichtlinienobjekt durchgeführt. Wenn das Gruppenrichtlinienobjekt in der Domäne nicht verknüpft ist, wird im Domänenstamm automatisch eine Verknüpfung erstellt. Wenn die zum Erstellen der Verknüpfung erforderlichen Berechtigungen nicht verfügbar sind, wird eine Warnung ausgegeben.  
  
-   Beim muss verwenden manuell-Gruppenrichtlinienobjekte, um DirectAccess-Einstellungen zu übernehmen den RAS-Server-Administrator uneingeschränkte Berechtigungen (bearbeiten, löschen, Ändern der Sicherheit) in den manuell erstellten Gruppenrichtlinienobjekten.  
  
Beachten Sie, wenn die richtigen Berechtigungen für die Replikation und das Verknüpfen von Gruppenrichtlinienobjekten nicht vorhanden sind, eine Warnung ausgegeben wird. Der Remotezugriffsvorgang wird fortgesetzt, aber Replikation und das Verknüpfen erfolgt nicht. Wenn eine Warnung ausgegeben wird Verknüpfung wird Links nicht automatisch erstellt werden, auch nachdem die Berechtigungen vorhanden sind. Stattdessen muss der Administrator die Links manuell erstellen.  
  
### <a name="233-managing-gpos-in-a-multi-domain-controller-environment"></a>2.3.3 Verwaltung von Gruppenrichtlinienobjekten in einer Umgebung mit mehreren Domänencontrollern  
Jedes Gruppenrichtlinienobjekt wird von einem bestimmten Domänencontroller wie folgt verwaltet werden:  
  
-   Das Server-Gruppenrichtlinienobjekt von einem der Domänencontroller in Zusammenhang mit dem Server Active Directory-Standort verwaltet wird, oder wenn der Domänencontroller an diesem Standort schreibgeschützt sind, zeigen Sie von einem mit aktiviertem Schreibzugriff Domänencontroller, der erste Server in den Eintrag am nächsten liegt.  
  
-   Client-Gruppenrichtlinienobjekte werden vom Domänencontroller als PDC-Emulator verwaltet.  
  
Wenn Sie manuell möchten Hinweis der GPO-Einstellungen Folgendes geändert:  
  
-   Führen Sie für Gruppenrichtlinienobjekte, um zu ermitteln, welcher Domänencontroller mit einem bestimmten Einstiegspunkt verknüpft ist, das PowerShell-Cmdlet `Get-DAEntryPointDC -EntryPointName <name of entry point>`.  
  
-   Wenn Sie Änderungen mit PowerShell-Cmdlets für Netzwerke oder der Gruppenrichtlinien-Verwaltungskonsole, vornehmen, wird standardmäßig der Domänencontroller fungiert als PDC-Emulator verwendet.  
  
-   Wenn Sie Einstellungen auf einem Domänencontroller, die nicht auf dem Domänencontroller, der den Einstiegspunkt (für Server-GPOs) oder der PDC-Emulator (für Client-Gruppenrichtlinienobjekte) zugeordnet ist ändern, beachten Sie Folgendes:  
  
    1.  Stellen Sie sicher, dass der Domänencontroller mit einem aktuellen Gruppenrichtlinienobjekt, repliziert werden, vor der Änderung der Einstellungen, und [sichern Sie die GPO-Einstellungen](https://go.microsoft.com/fwlink/?LinkID=257928), bevor die Änderungen. Wenn das Gruppenrichtlinienobjekt nicht aktualisiert wird, können Merge-Konflikte während der Replikation, sodass einer beschädigten Remotezugriffskonfiguration auftreten.  
  
    2.  Nach dem Ändern der Einstellungen, müssen Sie warten, für die Änderungen an den Domänencontroller repliziert werden, die den Gruppenrichtlinienobjekten zugeordnet ist. Nehmen Sie keine zusätzliche Änderungen, die mithilfe der Remotezugriffs-Verwaltungskonsole oder Remotezugriffs-PowerShell-Cmdlets, bis die Replikation abgeschlossen ist. Wenn Sie ein Gruppenrichtlinienobjekt auf zwei verschiedenen Domänencontrollern bearbeitet wurde, bevor die Replikation abgeschlossen ist, können Zusammenführungskonflikte, wodurch einer fehlerhaften Konfiguration auftreten  
  
-   Alternativ können Sie ändern, die standardmäßig die Einstellung mithilfe der **Domänencontroller ändern** Dialogfeld Feld in der Gruppenrichtlinien-Verwaltungskonsole oder über die **Open-NetGPO** PowerShell-Cmdlet, damit die Änderungen wurden mithilfe der Konsole oder der Netzwerk-Cmdlets verwenden den Domänencontroller, die Sie angeben.  
  
    1.  Zu diesem Zweck in der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste in des Containers Domänen- oder Standortcontainer, und klicken Sie auf **Domänencontroller ändern**.  
  
    2.  Geben Sie den DomainController-Parameter für das Open-NetGPO-Cmdlet, zu diesem Zweck in PowerShell. Um die privaten und öffentlichen Profile in der Windows-Firewall auf einem Gruppenrichtlinienobjekt namens domain1\DA_Server_GPO _Europe über einen Domänencontroller namens Europe-DC.corp.contoso.com zu aktivieren, führen Sie z. B. Folgendes ein:  
  
        ```  
        $gpoSession = Open-NetGPO -PolicyStore "domain1\DA_Server_GPO _Europe" -DomainController "europe-dc.corp.contoso.com"  
        Set-NetFirewallProfile -GpoSession $gpoSession -Name @("Private","Public") -Enabled True  
        Save-NetGPO -GpoSession $gpoSession  
        ```  
  
#### <a name="modifying-domain-controller-association"></a>Ändern die Zuordnung der Domänen-controller  
Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. In einigen Szenarien kann es erforderlich, für ein Gruppenrichtlinienobjekt ein anderen Domänencontrollers zuweisen:  
  
-   **Wartung der Domänencontroller und Ausfallzeiten**– Wenn der Domänencontroller, der ein Gruppenrichtlinienobjekt verwaltet nicht verfügbar ist, es kann erforderlich sein, das Gruppenrichtlinienobjekt auf einem anderen Domänencontroller verwalten.  
  
-   **Optimierung der konfigurationsverteilung**-nachdem Netzwerkinfrastruktur geändert hat, ist es möglicherweise erforderlich, um das Server-GPO eines Einstiegspunkts auf einem Domänencontroller in derselben Active Directory-Standort als Einstiegspunkt zu verwalten.   
  
## <a name="bkmk_2_4_DNS"></a>2.4 Planen von DNS  
Beachten Sie Folgendes ein, bei der Planung von DNS für eine Bereitstellung für mehrere Standorte:  
  
1.  Clientcomputer verwenden die ConnectTo-Adresse, um eine Verbindung mit dem RAS-Server herzustellen. Jeden Einstiegspunkt in der Bereitstellung erfordert eine andere ConnectTo-Adresse. Jeder Eintrag Punkt ConnectTo-Adresse muss in der öffentlichen DNS verfügbar sein, und die von Ihnen gewählte Adresse muss der Antragstellername des IP-HTTPS-Zertifikats, die Sie für die IP-HTTPS-Verbindung bereitstellen übereinstimmen.   
  
2.  Darüber hinaus erzwingt RAS symmetrisches routing; aus diesem Grund können nur Teredo und IP-HTTPS-Clients verbinden, wenn eine Bereitstellung für mehrere Standorte aktiviert ist. Damit um systemeigene IPv6-Clients eine Verbindung herstellen zu können, muss die ConnectTo-Adresse (die IP-HTTPS-URL) in beide die externen (Internetverbindung) IPv6 und IPv4-Adressen auf dem RAS-Server aufgelöst werden.  
  
3.  RAS erstellt einen Standard-Webtest, der von DirectAccess-Clientcomputern dazu verwendet wird, die Konnektivität zum internen Netzwerk zu prüfen. Während der Konfiguration des einzelnen Servers sollten die folgenden Namen im DNS registriert wurden:  
  
    1.  DirectAccess-WebProbeHost – sollte auflösen, um die interne IPv4-Adresse des RAS-Servers und zur IPv6-Adresse in einer reinen IPv6-Umgebung.  
  
    2.  DirectAccess-CorpConnectivityHost – sollte auflösen in eine Adresse "localhost" (Loopback) (entweder:: 1 "oder" 127.0.0.1, je nachdem, ob IPv6 im Unternehmensnetzwerk bereitgestellt wird).  
  
    In einer Bereitstellung mit mehreren Standorten muss ein weiterer DNS-Eintrag für die Directaccess-WebProbeHost für jeden Einstiegspunkt erstellt werden. Wenn Sie einen Einstiegspunkt hinzufügen, versucht RAS automatisch, diesen zusätzlichen Directaccess-WebProbeHost-Eintrag erstellen. Allerdings bei einem Fehler eine Warnung wird angezeigt, und Sie müssen den Eintrag manuell erstellen.  
  
    > [!NOTE]  
    > Wenn DNS-Bereinigung in der DNS-Infrastruktur aktiviert ist, wird empfohlen, deaktivieren die Bereinigung auf die DNS-Einträge, die automatisch vom Remotezugriff erstellt.  
  

  



