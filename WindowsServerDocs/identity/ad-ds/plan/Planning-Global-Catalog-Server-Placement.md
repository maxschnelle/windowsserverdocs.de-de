---
ms.assetid: 407d5e81-c04c-4275-9ae9-35f65b4a371a
title: Planen der Platzierung des globalen Katalogs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c32393640e929adf9681f511ed3707b85a3784db
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="planning-global-catalog-server-placement"></a>Planen der Platzierung des globalen Katalogs

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Platzierung des globalen Katalogs ist erforderlich, mit Ausnahme der planen, wenn Sie die Gesamtstruktur mit eine einzelnen Domäne verfügen. Konfigurieren Sie alle Domänencontroller in einer Gesamtstruktur mit einer einzelnen Domäne als globalen Katalogserver. Da alle Domänencontroller in der Gesamtstruktur das einzige Domänenverzeichnispartition gespeichert werden, erfordert konfigurieren jeden Domänencontroller als ein globaler Katalogserver keine Verwendung von zusätzlichen Speicherplatz, CPU-Auslastung oder Replikationsdatenverkehr. Reagieren alle Domänencontroller in einer Gesamtstruktur mit einer einzelnen Domäne als virtuelle globale Katalogserver; Das heißt, können sie alle Authentifizierung oder Serviceanfrage reagieren. Diese spezielle Bedingung für die einzelnen Domäne Gesamtstrukturen ist beabsichtigt. Authentifizierungsanforderungen erfordern einen globaler Katalogserver kontaktiert, wie bei der mehrere Domänen vorhanden sind, und ein Benutzer kann Mitglied einer universellen Gruppe, die in einer anderen Domäne vorhanden sein. Allerdings können nur Domänencontroller, die als globale Katalogserver festgelegt sind auf Abfragen des globalen Katalogs auf die Port 3268 des globalen Katalogs reagieren. Zur Vereinfachung der Verwaltung in diesem Szenario und konsistente Antworten sicherzustellen, entfällt alle Domänencontroller als globale Katalogserver Festlegen der Bedenken hinsichtlich der Domänencontroller zum globalen Katalogabfragen reagieren können. Genauer gesagt: jedes Mal ein Benutzer Start\Search\For Personen oder Drucker suchen oder universelle Gruppen erweitert, diese Anforderungen nur für den globalen Katalog wechseln.  
  
In mehreren Domänen Gesamtstrukturen erleichtern das globale Katalogserver Benutzer Anmeldeanfragen und Gesamtstruktur suchen. Die folgende Abbildungzeigt, wie Sie feststellen, welche Standorte globale Katalogserver erforderlich.  
  
![Planen der Platzierung des globalen Katalogs](media/Planning-Global-Catalog-Server-Placement/8fc4777c-47b6-4ee7-b8ad-a04e7c5ee67f.gif)  
  
In den meisten Fällen empfiehlt es sich, dass Sie bei der Installation neuer Domänencontroller den globalen Katalog einschließen. Die folgenden Ausnahmen gelten:  
  
-   Begrenzter Bandbreite: an Remotestandorten, wenn die Verbindung der wide Area Network (WAN) zwischen dem Remotestandort und dem Hubstandort begrenzt ist, können Zwischenspeichern der universellen Gruppenmitgliedschaft am Remotestandort um den Anforderungen der Anmeldung von Benutzern in der Website Rechnung tragen.  
  
-   Infrastruktur Operations Master-Rolle Inkompatibilität: platzieren Sie den globalen Katalog nicht auf einem Domänencontroller, auf dem die Infrastrukturmasterrolle in der Domäne gehostet werden, es sei denn, alle Domänencontroller in der Domäne globale Katalogserver sind oder die Gesamtstruktur verfügt über nur eine Domäne.  
  
## <a name="adding-global-catalog-servers-based-on-application-requirements"></a>Hinzufügen von globalen Katalogservern basierend auf den anwendungsanforderungen  
Bestimmte Anwendungen, z.B. Microsoft Exchange, Message Queuing (auch als MSMQ bezeichnet) und Anwendungen, die mit DCOM nicht ausreichend Antwort über latenten WAN-Links bieten und benötigen daher eine Infrastruktur mit hoher Verfügbarkeit globaler Katalog Abfrage mit geringer Latenz bereitstellen. Bestimmen Sie, ob alle Anwendungen, die über eine langsame WAN-Verbindung zu schlechter Leistung ausgeführt werden, in Regionen oder gibt an, ob die Speicherorte für Microsoft Exchange Server erforderlich. Wenn Ihre Speicherorte Anwendungen, die über eine WAN-Verbindung nicht ausreichend Antwort bereitstellen enthalten, müssen Sie einen globaler Katalogserver am Speicherort Abfragewartezeit reduzieren platzieren.  
  
> [!NOTE]  
> Read-only Domänencontrollern (RODCs) können erfolgreich zu globalen Katalog Serverstatus heraufgestuft werden. Allerdings können keine bestimmte AD-aktivierte Anwendungen ein RODC als globale Katalogserver unterstützen. Beispielsweise wird keine Version des Microsoft Exchange Server RODCs verwendet. Funktioniert Microsoft Exchange Server jedoch in Umgebungen, die RODCs enthalten, solange beschreibbaren Domänencontroller verfügbar sind. Exchange Server2007 wird effektiv RODCs ignoriert. Exchange Server2003 ignoriert RODCs auch in Standardbedingungen, in dem Exchange-Komponenten verfügbaren Domänencontroller automatisch erkannt. Mit Exchange Server2003 wurden keine Änderungen vorgenommen, um schreibgeschützte Verzeichnisserver aufmerksam zu machen. Daher kann bei dem Versuch, Exchange Server2003-Dienste und Tools für das Verwenden von RODCs erzwingen zu unvorhersehbarem Verhalten führen.  
  
## <a name="adding-global-catalog-servers-for-a-large-number-of-users"></a>Hinzufügen von globalen Katalogservern für eine große Anzahl von Benutzern  
Platzieren Sie globale Katalogserver an allen Standorten, die mehr als 100 Benutzer Überlastung des Netzwerks WAN-Links zu reduzieren und zu verhindern, dass Produktivitätsverluste bei einem Ausfall der WAN-Verbindung enthalten.  
  
## <a name="using-highly-available-bandwidth"></a>Verwenden hoch verfügbaren Bandbreite  
Sie müssen sich nicht um einen globalen Katalog an einer Position zu platzieren, werden keine Anwendungen, die einen globaler Katalogserver erforderlich, die enthält weniger als 100 Benutzer und auch an einen anderen Speicherort, der einen globaler Katalogserver enthält verbunden ist, über ein WAN, die 100Prozent für Active Directory-Domänendienste (AD DS) verfügbar ist. In diesem Fall können die Benutzer den globalen Katalogserver über die WAN-Verbindung zugreifen.  
  
Mobile Benutzer müssen die globalen Katalogserver herstellen, wenn sie sich zum ersten Mal an einer beliebigen Stelle anmelden. Wenn die Anmeldung über die WAN-Verbindung nicht akzeptabel ist, platzieren Sie einen globalen Katalog an einem Ort, der durch eine große Anzahl von servergespeicherten Benutzern aufgerufen werden.  
  
## <a name="enabling-universal-group-membership-caching"></a>Zwischenspeichern der universellen Gruppenmitgliedschaft aktivieren  
Für Standorte, die weniger als 100 Benutzer enthalten und enthalten, die keine große Anzahl von Roaming-Benutzer oder Anwendungen, die einen globaler Katalogserver erforderlich ist, können Sie Domänencontroller bereitstellen, die Windows Server2008 ausgeführt werden und das Zwischenspeichern der universellen Gruppenmitgliedschaft aktivieren. Stellen Sie sicher, dass die globalen Katalogserver nicht mehr als eine Replikationshop vom Domänencontroller sind, auf dem Zwischenspeichern der universellen Gruppenmitgliedschaft aktiviert ist, damit Informationen zu universellen Gruppen im Cache aktualisiert werden kann. Informationen, wie universelle Gruppe Zwischenspeichern funktioniert, finden Sie unter der globale Katalog Funktionsweise ([https://go.microsoft.com/fwlink/?LinkId=107063](https://go.microsoft.com/fwlink/?LinkId=107063)).  
  
Ein Arbeitsblatt, die Sie dokumentieren unterstützen, platzieren Sie globale Katalogserver und Domänencontroller mit Zwischenspeichern der universellen aktiviert werden soll, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen < DICT__Job_ Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>, and open Domain Controller Platzierung (DSSTOPO_4.doc). Finden Sie Informationen zu Standorten, in denen Sie die globalen Katalogserver zu platzieren, wenn Sie die Gesamtstruktur-Stammdomäne und regionale Domänen bereitstellen müssen.  
  


