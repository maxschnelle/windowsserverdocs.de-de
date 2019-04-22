---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: Planen der Platzierung des globalen Katalogservers
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aefed1a2ed0d346f75ad4d135f8c0ae314fd7fc7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820681"
---
# <a name="planning-global-catalog-server-placement"></a>Planen der Platzierung des globalen Katalogservers

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Platzierung des globalen Katalogs ist erforderlich, mit Ausnahme von planen, wenn Sie die Gesamtstruktur mit eine einzelnen Domäne verfügen. Konfigurieren Sie alle Domänencontroller als globale Katalogserver, in der Gesamtstruktur mit einer einzelnen Domäne. Da alle Domänencontroller in der Gesamtstruktur die einzige Domänenverzeichnispartition gespeichert werden, erfordert konfigurieren jeden Domänencontroller als globalen Katalogserver keine zusätzlichen Datenträger-Speicherplatz, CPU-Auslastung oder Replikationsdatenverkehr. Reagieren in der Gesamtstruktur mit einer einzelnen Domäne alle Domänencontroller als virtuelle globale Katalogserver; d.h., können sie alle auf Authentifizierung oder Service Requests reagieren. Diese besondere Bedingung für die einzelnen Domäne Gesamtstrukturen ist beabsichtigt. Authentifizierungsanforderungen erfordern nicht, wenden Sie sich an einem globalen Katalogserver an, wie wenn mehrere Domänen vorhanden sind, und ein Benutzer kann Mitglied einer universellen Gruppe, die in einer anderen Domäne vorhanden sein. Allerdings können nur Domänencontroller, die als globale Katalogserver festgelegt sind, klicken Sie auf Abfragen auf dem globalen Katalogport 3268 des globalen Katalogs reagieren. Zur einfacheren Verwaltung in diesem Szenario und konsistente Antworten stellen Sie sicher, entfällt das Festlegen aller Domänencontroller als globale Katalogserver die Sorge, zu der, die Domäne Domänencontroller zum globalen Katalogabfragen reagieren können. Insbesondere jedes Mal ein Benutzer verwendet Start\Search\For Personen oder Druckern suchen oder universelle Gruppen erweitert, diese Anforderungen gesendet werden. nur zum globalen Katalog.  
  
In Gesamtstrukturen mit mehreren Domänen erleichtern die globalen Katalogserver anmeldeanforderungen von Benutzern und Gesamtstruktur-Suchvorgänge. Die folgende Abbildung zeigt, wie Sie bestimmen, welche Standorte werden globale Katalogserver müssen.  
  
![Planen der gc-Platzierung](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)  
  
In den meisten Fällen empfiehlt es sich, dass Sie bei der Installation neuer Domänencontroller des globalen Katalogs enthalten. Die folgenden Ausnahmen gelten:  
  
- Eingeschränkter Bandbreite: An Remotestandorten ist die Verbindung die wide Area Network (WAN) zwischen dem Remotestandort und am Hubstandort beschränkt ist, können Sie Zwischenspeichern der universellen Gruppenmitgliedschaft in der remote-standortsystemserver um die Anforderungen der Anmeldung von Benutzern auf der Website zu ermöglichen.  
- Inkompatibilität der Infrastruktur Operations master Role: Platzieren Sie den globalen Katalog nicht auf einem Domänencontroller, dass die Hosts die infrastrukturvorgängen Rolle in der Domäne beherrschen, wenn alle Domänencontroller in der Domäne globale Katalogserver sind, oder die Gesamtstruktur verfügt über nur eine Domäne.  
  
## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>Hinzufügen von globalen Katalogservern, die basierend auf anwendungsanforderungen

Bestimmte Anwendungen, z. B. Microsoft Exchange, Message Queuing (auch bekannt als MSMQ) und Anwendungen, die mithilfe von DCOM nicht angemessen zu reagieren gegenüber latente WAN-Verbindungen bieten und aus diesem Grund benötigen eine hoch verfügbaren globalen Katalogserver-Infrastruktur mit niedriger-Abfrage die Wartezeit. Bestimmen Sie, ob alle Anwendungen, die über eine langsame WAN-Verbindung unzureichend ausgeführt werden, oder ob die Speicherorte für Microsoft Exchange Server erforderlich. Wenn die Orte Ihrer Anwendungen, die nicht angemessen zu reagieren, über eine WAN-Verbindung liefern können enthalten, müssen Sie einen globaler Katalogserver am Speicherort, um die Verringerung von abfragelatenzen beitragen platzieren.  
  
> [!NOTE]  
> Read-only-Domänencontroller (RODCs) können zum Status des globalen Katalogs Server wurde erfolgreich höher gestuft werden. Allerdings können nicht bestimmten AD-aktivierte Anwendungen einen RODC als ein globaler Katalogserver nicht unterstützt. Beispielsweise wird keine Version von Microsoft Exchange Server RODCs verwendet. Funktioniert jedoch Microsoft Exchange Server in Umgebungen, die RODCs enthalten, solange es verfügbaren beschreibbaren Domänencontroller vorhanden sind. Exchange Server 2007 wird die RODCs effektiv ignoriert. Exchange Server 2003 ignoriert auch RODCs in standardbedingungen, in dem Exchange-Komponenten verfügbaren Domänencontroller automatisch erkennen. Für Exchange Server 2003 wurden keine Änderungen vorgenommen, um nur-Lese Verzeichnisserver aufmerksam zu machen. Aus diesem Grund kann versuchen, Exchange Server 2003-Dienste und Tools für die Verwendung von RODCs erzwingen zu einem unvorhersehbaren Verhalten führen.  
  
## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>Hinzufügen von globalen Katalogserver für eine große Anzahl von Benutzern

Platzieren Sie globale Katalogserver an allen Standorten, die mehr als 100 Benutzer, die Überlastung der WAN-Netzwerkverbindungen zu verringern und Produktivität von Datenverlusten bei einem Ausfall der WAN-Verbindung enthält.  
  
## <a name="using-highly-available-bandwidth"></a>Hoch verfügbaren Bandbreite verwenden

Sie müssen sich nicht um einen globalen Katalog an einer Position zu platzieren, die enthält keine Anwendungen, die einen globaler Katalogserver erfordern, umfasst weniger als 100 Benutzer und auch an einen anderen Speicherort, die einen globaler Katalogserver enthält verbunden ist, über ein WAN, die 100 % ist ein Verfügbare für Active Directory Domain Services (AD DS). In diesem Fall können die Benutzer den globale Katalogserver über die WAN-Verbindung zugreifen.  
  
Roaming-Benutzer müssen die globalen Katalogserver herstellen, wenn sie sich zum ersten Mal an einem beliebigen Speicherort anmelden. Wenn die Anmeldezeit über die WAN-Verbindung nicht akzeptabel ist, platzieren Sie einen globalen Katalog an einem Speicherort an, der durch eine große Anzahl von roaming-Benutzer besucht wird.  
  
## <a name="enabling-universal-group-membership-caching"></a>Aktivieren das Zwischenspeichern der universellen Gruppenmitgliedschaft

Für Standorte, die weniger als 100 Benutzer enthalten, und enthalten, die eine große Anzahl von roaming-Benutzer oder Anwendungen, die einen globaler Katalogserver erfordern nicht, können Sie Domänencontroller bereitstellen, die Windows Server 2008 ausgeführt werden und der universellen Gruppenmitgliedschaft aktivieren das Zwischenspeichern. Stellen Sie sicher, dass die globalen Katalogserver nicht mehr als einen Replikationshop vom Domänencontroller sind, auf dem Zwischenspeichern der universellen Gruppenmitgliedschaft aktiviert ist, damit Informationen zur universellen im Cache aktualisiert werden kann. Informationen zur wie universelle Gruppe Zwischenspeicherung finden Sie im Artikel [globalen Katalog Funktionsweise des](https://go.microsoft.com/fwlink/?LinkId=107063).  
  
Ein Arbeitsblatt, das Sie in der Dokumentation zu unterstützen, in dem globale Katalogserver und Domänencontroller platzieren mit Zwischenspeichern der universellen aktiviert werden sollen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_ herunterladen Designing_and_Deploying_Directory_and_Security_Services.ZIP, und öffnen Domänencontrollerkapazität (DSSTOPO_4.doc). Finden Sie unter den Informationen zu Speicherorten, die in denen globalen Katalogserver platziert werden, beim Bereitstellen der Gesamtstruktur-Stammdomäne und Regionaldomänen werden müssen.  
