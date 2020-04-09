---
title: Regions übergreifende Hochverfügbarkeit AD FS Bereitstellung in Azure mit Azure Traffic Manager | Microsoft-Dokumentation
description: Bereitstellen von AD FS in Azure für hohe Verfügbarkeit.
services: active-directory
author: anandyadavmsft
manager: mtillman
ms.prod: windows-server
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: 9bfb59fadd2cf6b07d3c47ab69f0fe67974706a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855203"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Regions übergreifende Hochverfügbarkeit AD FS Bereitstellung in Azure mit Azure Traffic Manager
[AD FS Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) bietet eine Schritt-für-Schritt-Anleitung, wie Sie eine einfache AD FS-Infrastruktur für Ihre Organisation in Azure bereitstellen können. Dieser Artikel enthält die nächsten Schritte zum Erstellen einer Regions übergreifenden Bereitstellung von AD FS in Azure mithilfe von [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/). Azure Traffic Manager unterstützt Sie bei der Erstellung einer geografisch verteilten Hochverfügbarkeit und hochleistungsfähigen AD FS Infrastruktur für Ihre Organisation, indem Sie eine Reihe von Routing Methoden verwenden, die für unterschiedliche Anforderungen aus der Infrastruktur verfügbar sind.

Eine hochverfügbare, Regions übergreifende AD FS Infrastruktur ermöglicht Folgendes:

* **Beseitigung von Single Point of Failure:** Mit den Failoverfunktionen von Azure Traffic Manager können Sie eine hochverfügbare AD FS Infrastruktur erreichen, auch wenn eines der Rechenzentren in einem Teil der Welt ausfällt.
* **Verbesserte Leistung:** Mithilfe der in diesem Artikel vorgeschlagenen Bereitstellung können Sie eine leistungsstarke AD FS-Infrastruktur bereitstellen, mit der sich Benutzer schneller authentifizieren können. 

## <a name="design-principles"></a>Designprinzipien
![Gesamtentwurf](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Die grundlegenden Entwurfs Prinzipien sind identisch mit den Entwurfs Prinzipien im Artikel AD FS Bereitstellung in Azure. Das obige Diagramm zeigt eine einfache Erweiterung der grundlegenden Bereitstellung in einer anderen geografischen Region. Im folgenden finden Sie einige Punkte, die Sie beim Erweitern Ihrer Bereitstellung auf eine neue geografische Region beachten

* **Virtuelles Netzwerk:** Sie sollten ein neues virtuelles Netzwerk in der geografischen Region erstellen, in der Sie zusätzliche AD FS Infrastruktur bereitstellen möchten. In der obigen Abbildung sehen Sie Geo1 vnet und Geo2 vnet als die beiden virtuellen Netzwerke in jeder geografischen Region.
* **Domänen Controller und AD FS Server im neuen geografischen vnet:** Es wird empfohlen, Domänen Controller in der neuen geografischen Region bereitzustellen, damit die AD FS Server in der neuen Region keinen Domänen Controller in einem anderen weit entfernten Netzwerk kontaktieren müssen, um eine Authentifizierung abzuschließen und so die Leistung zu verbessern.
* **Speicher Konten:** Speicher Konten sind einer Region zugeordnet. Da Sie Computer in einer neuen geografischen Region bereitstellen werden, müssen Sie neue Speicher Konten erstellen, die in der Region verwendet werden.  
* **Netzwerk Sicherheitsgruppen:** Als Speicher Konten können Netzwerk Sicherheitsgruppen, die in einer Region erstellt werden, nicht in einer anderen geografischen Region verwendet werden. Daher müssen Sie neue Netzwerk Sicherheitsgruppen erstellen, die denen in der ersten geografischen Region für das int-und DMZ-Subnetz in der neuen geografischen Region ähneln.
* **DNS-Bezeichnungen für öffentliche IP-Adressen:** Azure-Traffic Manager können nur über DNS-Bezeichnungen auf Endpunkte verweisen. Daher müssen Sie DNS-Bezeichnungen für die öffentlichen IP-Adressen der externen Lasten Ausgleichs Module erstellen.
* **Azure-Traffic Manager:** Microsoft Azure Traffic Manager ermöglicht es Ihnen, die Verteilung des Benutzer Datenverkehrs an die Dienst Endpunkte zu steuern, die in verschiedenen Daten Centern auf der ganzen Welt ausgeführt werden. Azure Traffic Manager funktioniert auf der DNS-Ebene. Er verwendet DNS-Antworten, um Endbenutzer-Datenverkehr an Global verteilte Endpunkte weiterzuleiten. Clients stellen dann eine direkte Verbindung mit diesen Endpunkten her. Mit unterschiedlichen Routing Optionen für Leistung, gewichtet und Priorität können Sie problemlos die Routing Option auswählen, die für die Anforderungen Ihrer Organisation am besten geeignet ist. 
* Vnet **-zu-v-Netzwerkkonnektivität zwischen zwei Regionen:** Sie benötigen keine Konnektivität zwischen den virtuellen Netzwerken. Da jedes virtuelle Netzwerk Zugriff auf Domänen Controller hat und über AD FS-und WAP-Server verfügt, kann er ohne jegliche Konnektivität zwischen den virtuellen Netzwerken in unterschiedlichen Regionen funktionieren. 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Schritte zum Integrieren von Azure-Traffic Manager
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>Bereitstellen von AD FS in der neuen geografischen Region
Befolgen Sie die Schritte und Richtlinien in [AD FS Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md) , um die gleiche Topologie in der neuen geografischen Region bereitzustellen.

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>DNS-Bezeichnungen für öffentliche IP-Adressen der (öffentlichen) Load Balancer mit Internet Zugriff
Wie bereits erwähnt, kann der Azure-Traffic Manager nur auf DNS-Bezeichnungen als Endpunkte verweisen. Daher ist es wichtig, dass DNS-Bezeichnungen für die öffentlichen IP-Adressen der externen Lasten Ausgleichs Module erstellt werden. Der folgende Screenshot zeigt, wie Sie Ihre DNS-Bezeichnung für die öffentliche IP-Adresse konfigurieren können. 

![DNS-Bezeichnung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Bereitstellen von Azure Traffic Manager
Führen Sie die folgenden Schritte aus, um ein Traffic Manager-Profil zu erstellen. Weitere Informationen finden Sie auch unter [Verwalten eines Azure Traffic Manager Profils](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles).

1. **Erstellen Sie ein Traffic Manager Profil:** Legen Sie Ihrem Traffic Manager-Profil einen eindeutigen Namen zu. Der Name des Profils ist Teil des DNS-Namens und fungiert als Präfix für die Traffic Manager Domänen Namen Bezeichnung. Der Name/das Präfix wird zu. Trafficmanager.net hinzugefügt, um eine DNS-Bezeichnung für Ihren Traffic Manager zu erstellen. Der folgende Screenshot zeigt das Traffic Manager-DNS-Präfix, das als mysts festgelegt wird, und die resultierende DNS-Bezeichnung lautet mysts.Trafficmanager.net. 
   
    ![Traffic Manager Profilerstellung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Routing Methode für Datenverkehr:** In Traffic Manager stehen drei Routing Optionen zur Verfügung:
   
   * Priority 
   * Leistung
   * Tem
     
     Die Leistung ist die empfohlene Option, um eine hohe Reaktions **Fähigkeit** AD FS-Infrastruktur zu erreichen. Sie können jedoch eine beliebige Routing Methode auswählen, die für Ihre Bereitstellungs Anforderungen am besten geeignet ist. Die AD FS Funktionalität wird von der ausgewählten Routing Option nicht beeinträchtigt. Weitere Informationen finden Sie unter [Traffic Manager Routing Methoden für Datenverkehr](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) . Im obigen Beispiel Screenshot sehen Sie die ausgewählte **Leistungs** Methode.
3. **Endpunkte konfigurieren:** Klicken Sie auf der Seite Traffic Manager auf Endpunkte, und wählen Sie hinzufügen aus. Dadurch wird eine Seite zum Hinzufügen eines Endpunkts geöffnet, die dem folgenden Screenshot ähnelt.
   
   ![Konfigurieren von Endpunkten](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Befolgen Sie für die unterschiedlichen Eingaben die folgenden Richtlinien:
   
   **Typ:** Wählen Sie Azure-Endpunkt aus, da wir auf eine öffentliche Azure-IP-Adresse verweisen.
   
   **Name:** Erstellen Sie einen Namen, den Sie dem Endpunkt zuordnen möchten. Dies ist nicht der DNS-Name und hat keine Auswirkungen auf DNS-Einträge.
   
   **Ziel Ressourcentyp:** Wählen Sie öffentliche IP-Adresse als Wert für diese Eigenschaft aus. 
   
   **Ziel Ressource:** Dadurch haben Sie die Möglichkeit, aus den unter Ihrem Abonnement verfügbaren DNS-Bezeichnungen auszuwählen. Wählen Sie die DNS-Bezeichnung aus, die dem Endpunkt entspricht, den Sie konfigurieren.
   
   Fügen Sie einen Endpunkt für jede geografische Region hinzu, an die der Azure-Traffic Manager Datenverkehr weiterleiten soll.
   Weitere Informationen und ausführliche Schritte zum Hinzufügen/Konfigurieren von Endpunkten in Traffic Manager finden Sie unter [hinzufügen, deaktivieren, aktivieren oder Löschen von Endpunkten](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) .
4. Test **konfigurieren:** Klicken Sie in der Traffic Manager-Seite auf Konfiguration. Auf der Konfigurationsseite müssen Sie die Monitoreinstellungen ändern, um den HTTP-Port 80 und den relativen Pfad/ADFS/Probe zu überprüfen.
   
    ![Test konfigurieren](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Stellen Sie sicher, dass der Status der Endpunkte nach Abschluss der Konfiguration Online ist**. Wenn sich alle Endpunkte im Status "heruntergestuft" befinden, versucht Azure Traffic Manager, den Datenverkehr weiterzuleiten, wobei angenommen wird, dass die Diagnose falsch ist und alle Endpunkte erreichbar sind.
   > 
   > 
5. **Ändern von DNS-Einträgen für Azure-Traffic Manager:** Der Verbund Dienst muss ein CNAME-Namen für den DNS-Namen des Azure-Traffic Manager sein. Erstellen Sie einen CNAME in den öffentlichen DNS-Einträgen, damit jeder, der versucht, den Verbund Dienst zu erreichen, tatsächlich den Azure-Traffic Manager erreicht.
   
    Wenn Sie z. b. den Verbund Dienst FS.fabidentity.com auf den Traffic Manager verweisen möchten, müssen Sie den DNS-Ressourcen Daten Satz wie folgt aktualisieren:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>Testen des Routings und AD FS anmelden
### <a name="routing-test"></a>Routing Test
Ein sehr grundlegender Test für das Routing wäre der Versuch, den DNS-Namen des Verbund Dienstanbieter von einem Computer in jeder geografischen Region zu pingen. Abhängig von der ausgewählten Routing Methode wird der Endpunkt, der tatsächlich Pingen soll, in der Ping-Anzeige widergespiegelt. Wenn Sie z. b. das Leistungs Routing ausgewählt haben, wird der Endpunkt, der dem Bereich des Clients am nächsten liegt, erreicht. Im folgenden finden Sie eine Momentaufnahme von zwei Pings von zwei verschiedenen Regions Client Computern: eine in der Region EastAsia und eine in der Region USA, Westen. 

![Routing Test](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS des Anmelde Tests
Die einfachste Möglichkeit zum Testen von AD FS ist die Verwendung der Seite idpinitiatedsignon. aspx. Um dies zu erreichen, ist es erforderlich, idpinitiatedsignon in den AD FS Eigenschaften zu aktivieren. Führen Sie die folgenden Schritte aus, um das AD FS Setup zu überprüfen

1. Führen Sie das folgende Cmdlet auf dem AD FS Server mithilfe von PowerShell aus, um es auf "aktiviert" festzulegen. 
   Set-ADF sproperties-enableidpinitiatedsignonpage $true
2. Von einem beliebigen externen Computer Zugriff https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Die AD FS Seite sollte wie folgt angezeigt werden:
   
    ![AD FS-Test-Authentifizierungs Aufforderung](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    bei erfolgreicher Anmeldung wird Ihnen eine Erfolgsmeldung angezeigt, wie unten dargestellt:
   
    ![AD FS-Test: Authentifizierung erfolgreich](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Verwandte Links
* [Grundlegende AD FS Bereitstellung in Azure](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [Traffic Manager Routing Methoden für Datenverkehr](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>Nächste Schritte
* [Verwalten eines Azure Traffic Manager Profils](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [Hinzufügen, deaktivieren, aktivieren oder Löschen von Endpunkten](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

