---
title: Hohe Verfügbarkeit gebietsübergreifende AD FS-Bereitstellung in Azure mit Azure Traffic Manager | Microsoft-Dokumentation
description: In diesem Dokument lernen Sie, wie Sie für die Bereitstellung von AD FS in Azure für hohe Verfügbarkeit zu erzielen.
keywords: AD fs mit Azure Traffic Manager, Adfs mit Azure Traffic Manager, geografische, mehrere Datencenter, geografische Datencenter, mehrere geografische Datencenter, AD FS in Azure bereitstellen, bereitstellen, Azure Adfs, Azure Adfs, Azure Ad fs, Adfs bereitstellen, Ad fs, Adfs in Azure bereitstellen, Bereitstellen von AD FS in Azure Bereitstellen von AD FS in Azure, Adfs Azure, Einführung in AD FS, Azure, AD FS in Azure Iaas, ADFS, Adfs in Azure verschieben
services: active-directory
documentationcenter: ''
author: anandyadavmsft
manager: mtillman
editor: ''
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: 4af0386ef97694baa9ba7f1e5e7163554d79734a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874121"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Hohe Verfügbarkeit gebietsübergreifende AD FS-Bereitstellung in Azure mit Azure Traffic Manager
[AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) bietet schrittweisen Führungslinie, wie Sie eine einfache AD FS-Infrastruktur für Ihre Organisation in Azure bereitstellen können. Dieser Artikel enthält die nächsten Schritte zum Erstellen einer gebietsübergreifende AD FS-Bereitstellung in Azure mithilfe [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/). Azure Traffic Manager lassen sich eine geografisch verteilt, hohe Verfügbarkeit und hoher Leistung von AD FS-Infrastruktur für Ihre Organisation erstellen Reihe von Methoden für das datenverkehrsrouting für unterschiedliche Anforderungen von der Infrastruktur zur Verfügung.

Eine hochverfügbare, gebietsübergreifende AD FS-Infrastruktur ermöglicht:

* **Beseitigung von einzelnen Fehlerquelle zu vermeiden:** Mit den Failoverfunktionen von Azure Traffic Manager können Sie eine hochverfügbare AD FS-Infrastruktur erreichen, auch wenn einer der Rechenzentren in einem Teil der ganzen Welt ausfällt
* **Verbesserte Leistung:** Sie können die empfohlene Bereitstellung in diesem Artikel verwenden, um eine hochleistungsfähige AD FS-Infrastruktur bereitzustellen, mit die Benutzer schneller authentifizieren können. 

## <a name="design-principles"></a>Designprinzipien
![Gesamtentwurf](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Die grundlegenden Entwurfsprinzipien werden gleichen Entwurfsprinzipien im AD FS-Bereitstellung im Azure-Artikel aufgeführt. Das obige Diagramm zeigt eine einfache Erweiterung der grundlegenden Bereitstellung auf einer anderen geografischen Region. Im folgenden sind einige Punkte zu beachten, wenn Sie die Bereitstellung auf neuen geografischen Region erweitern

* **Virtuelles Netzwerk:** Sie sollten ein neues virtuelles Netzwerk in der geografischen Region erstellen, zusätzliche AD FS-Infrastruktur bereitgestellt werden soll. In der Abbildung oben sehen Sie Geo1 VNET "und" Geo2 VNET wie die beiden virtuellen Netzwerke in jeder geografischen Region.
* **Domänencontroller und AD FS-Server im neuen geografischen VNET:** Es wird empfohlen, zu der Domäne bereitstellen, die Controller in der neuen geografischen Region, damit die AD FS-Server in der neuen Region keine wenden Sie sich an einem Domänencontroller in einer anderen weit Netzwerk, um eine Authentifizierung und die Verbesserung der Leistung abzuschließen.
* **Speicherkonten:** Speicherkonten sind einer Region zugeordnet. Da Sie Computer in einer neuen geografischen Region bereitstellen möchten, müssen Sie zum Erstellen neuer Speicherkonten, die in der Region verwendet werden.  
* **Netzwerksicherheitsgruppen:** Da Storage-Konten in einer Region erstellt Netzwerksicherheitsgruppen in einer anderen geografischen Region verwendet werden, können nicht. Aus diesem Grund müssen Sie neue netzwerksicherheitsgruppen ähnlich denen in der ersten geografischen Region für das int- und das DMZ-Subnetz in der neuen geografischen Region erstellen.
* **DNS-Bezeichnungen für öffentliche IP-Adressen:** Azure Traffic Manager können Endpunkte finden Sie unter ausschliesslich über DNS-Bezeichnungen. Aus diesem Grund müssen Sie DNS-Bezeichnungen für öffentlichen IP-Adressen der externen Lastenausgleichsmodule erstellen.
* **Mit Azure Traffic Manager:** Microsoft Azure Traffic Manager können Sie zum Steuern der Verteilung des Benutzerdatenverkehrs an Ihre Dienstendpunkte in verschiedenen Rechenzentren auf der ganzen Welt ausgeführt. Azure Traffic Manager arbeitet auf DNS-Ebene. Er verwendet DNS-Antworten, um Endbenutzer-Datenverkehr an Global verteilte Endpunkte zu leiten. Clients stellen dann eine Verbindung mit diesen Endpunkten direkt. Dank verschiedener Routingoptionen Leistung "," gewichtet "und" Priorität können Sie einfach die Wahl der Routingoption am besten geeignet für die Anforderungen Ihrer Organisation auswählen. 
* **Vnet-zu-vnet-Konnektivität zwischen zwei Regionen:** Sie müssen nicht selbst über Konnektivität zwischen den virtuellen Netzwerken verfügen. Da jedes virtuelles Netzwerk den Zugriff auf Domänencontroller hat und AD FS und WAP-Server selbst, können sie ganz ohne Verbindung zwischen den virtuellen Netzwerken in verschiedenen Regionen arbeiten. 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Schritte zum Integrieren von Azure Traffic Manager
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>Bereitstellen von AD FS in der neuen geografischen region
Führen Sie die Schritte und die Richtlinien in [AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) die gleiche Topologie in der neuen geografischen Region bereitstellen.

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>DNS-Bezeichnungen für öffentliche IP-Adressen der Lastenausgleichsmodule Internetzugriff (öffentlich)
Wie bereits erwähnt, kann Azure Traffic Manager nur auf DNS-Bezeichnungen als Endpunkte verweisen, und daher ist es wichtig, um DNS-Bezeichnungen für öffentlichen IP-Adressen der externen Lastenausgleichsmodule erstellen. Folgende Screenshot zeigt, wie Sie Ihre DNS-Bezeichnung für die öffentliche IP-Adresse konfigurieren können. 

![DNS-Bezeichnung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Bereitstellen von Azure Traffic Manager
Gehen Sie folgendermaßen vor, um ein Traffic Manager-Profil zu erstellen. Weitere Informationen können Sie auch zum verweisen [Verwalten von Azure Traffic Manager-Profilen](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles).

1. **Erstellen Sie ein Traffic Manager-Profil:** Geben Sie Ihre Traffic Manager-Profil einen eindeutigen Namen zu. Dieser Name des Profils ist Teil des DNS-Namens und fungiert als Präfix für die Traffic Manager-domänennamenbezeichnung. Der Name / Präfix hinzugefügt. trafficmanager.net, um eine DNS-Bezeichnung für Ihre Traffic Manager zu erstellen. Der folgende Screenshot zeigt den Traffic Manager DNS-Präfix mysts festgelegt wird und die resultierenden DNS-Bezeichnung mysts.trafficmanager.NET". 
   
    ![Traffic Manager-profilerstellung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Routingmethode für Datenverkehr:** Es gibt drei Routingoptionen in Traffic Manager zur Verfügung:
   
   * Priority 
   * Leistung
   * Gewichteter
     
     **Leistung** ist die empfohlene Option, um reaktionsschnelle AD FS-Infrastruktur zu erreichen. Sie können jedoch eine der anderen Routingmethoden für Ihre Anforderungen am besten geeignet. Die AD FS-Funktionen wird durch die Wahl der Routingoption nicht beeinträchtigt. Finden Sie unter [Traffic Manager-Routingmethoden für Datenverkehr](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) für Weitere Informationen. Im Beispiel Screenshot darüber sehen die **Leistung** Methode ausgewählt.
3. **Konfigurieren von Endpunkten:** Klicken Sie auf der Traffic Manager-Seite klicken Sie auf die Endpunkte, und wählen Sie hinzufügen. Dadurch wird eine hinzufügen-endpunktseite ähnlich wie im folgenden Screenshot geöffnet.
   
   ![Konfigurieren von Endpunkten](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Führen Sie bei den verschiedenen Eingaben die folgende Richtlinie:
   
   **Typ:** Wählen Sie Azure-Endpunkt aus, wie es in eine Azure öffentliche IP-Adresse verweisen möchten.
   
   **Name:** Erstellen Sie einen Namen, den mit dem Endpunkt zugeordnet werden soll. Dies ist nicht der DNS-Name und hat keinen Einfluss auf DNS-Einträge.
   
   **Zielressourcentyp:** Wählen Sie die öffentliche IP-Adresse als der Wert dieser Eigenschaft. 
   
   **Zielressource:** Dadurch erhalten Sie eine Option aus, um zwischen den verschiedenen DNS-Bezeichnungen wählen, dass in Ihrem Abonnement zur Verfügung stehen. Wählen Sie die DNS-Bezeichnung entsprechend dem Endpunkt, den Sie konfigurieren.
   
   Fügen Sie der Endpunkt für jede geografische Region gewünschten Azure Traffic Manager zum Weiterleiten von Datenverkehr an.
   Weitere Informationen und ausführliche Anleitungen zum Hinzufügen / Konfigurieren von Endpunkten in Traffic Manager finden Sie unter [hinzufügen, deaktivieren, aktivieren oder Löschen von Endpunkten](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints)
4. **Konfigurieren des Tests an:** Klicken Sie auf der Konfiguration, in der Traffic Manager-Seite. Auf der Konfigurationsseite müssen Sie so ändern Sie die überwachungseinstellungen für die Suche auf HTTP-Port 80 und der relative Pfad festlegen
   
    ![Konfigurieren des Tests](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Stellen Sie sicher, dass der Status der Endpunkte ONLINE ist, sobald die Konfiguration abgeschlossen ist**. Wenn alle Endpunkte im Status "" heruntergestuft "sind, werden Azure Traffic Manager einen versucht zum Weiterleiten von Datenverkehr vorausgesetzt, dass die Diagnoseergebnisse fehlerhaft und alle Endpunkte erreichbar sind.
   > 
   > 
5. **Ändern von DNS-Einträgen für Azure Traffic Manager:** Der Verbunddienst sollte einen CNAME-Eintrag auf den Azure Traffic Manager DNS-Namen. Erstellen Sie einen CNAME-Eintrag in der öffentlichen DNS-Einträgen, sodass jemand, der den Verbunddienst erreichen tatsächlich Azure Traffic Manager erreicht werden.
   
    Z. B. wenn die Verbund-Service-fs.fabidentity.com an Traffic Manager verweisen möchten, müssten Sie den DNS-Ressourceneintrag folgt aktualisieren:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>Testen des Routings und AD FS-Anmeldung
### <a name="routing-test"></a>Routingtest
Ein einfachen Test für das routing wäre, die versuchen, DNS-Namen des Verbunddiensts von einem Computer in jeder geografischen Region anpingen. Abhängig von der Routingmethode spiegelt der tatsächlich angepingte Endpunkt in der pingausgabe angezeigt. Z. B. bei Auswahl der Performance-routing, wird Sie dann der Endpunkt der Region des Clients am ehesten entsprechen erreicht werden. Im folgenden finden Sie die Momentaufnahme zwei Pings von zwei Clientcomputern der anderen Region, in der Region Asien, Osten und eine im Westen der USA. 

![Routingtest](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS-Anmeldung testen
Die einfachste Möglichkeit zum Testen der AD FS ist die Verwendung von der Seite "IdpInitiatedSignon.aspx". Damit Sie so vorgehen, es ist erforderlich, um auf die AD FS-Eigenschaften "idpinitiatedsignon" zu aktivieren. Führen Sie die Schritte unten aus, um die AD FS-Installation überprüfen

1. Führen Sie die unten angegebene Cmdlet auf dem AD FS-Server mithilfe von PowerShell, um es "aktiviert" festzulegen. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Von jedem externen Computer Zugriff https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Daraufhin sollte die AD FS-Seite wie die folgende:
   
    ![AD FS-Test – authentifizierungsaufforderung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    und bei erfolgreicher Anmeldung, es wird Ihnen eine Erfolgsmeldung wie unten dargestellt:
   
    ![AD FS-Test – Authentifizierung erfolgreich](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Verwandte Links
* [AD FS-Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [Traffic Manager-Routingmethoden für Datenverkehr](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>Nächste Schritte
* [Verwalten von Azure Traffic Manager-Profilen](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [Hinzufügen, deaktivieren, aktivieren oder Löschen von Endpunkten](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

