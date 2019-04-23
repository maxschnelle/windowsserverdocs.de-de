---
ms.assetid: 093ef1ae-ebc1-490f-9fb1-2c000ce89eb6
title: Verwenden des organisatorischen Domänengesamtstruktur-Modells
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 876a15dcdd951e0323fb7ddb7be96317f5512f0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875911"
---
# <a name="using-the-organizational-domain-forest-model"></a>Verwenden des organisatorischen Domänengesamtstruktur-Modells

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In das Organisationsdomäne Forest-Modell wird eine Domäne innerhalb einer Gesamtstruktur von jeder mehrere autonome Gruppen besitzen. Jede Gruppe steuert, auf Domänenebene dienstverwaltung, das es ihnen, bestimmte Aspekte der dienstverwaltung autonom verwalten, während der dienstverwaltung auf Gesamtstrukturebene steuert, der Gesamtstrukturbesitzer ermöglicht wird.  

Die folgende Abbildung zeigt ein Organisationsdomäne Forest-Modell.  

![verwenden das Org Domäne Forest-Modell](../../media/Using-the-Organizational-Domain-Forest-Model/c50a3c6a-b0e4-43ec-ad62-f05d05f0bbd2.gif)  

## <a name="domain-level-service-autonomy"></a>Die Autonomie eines Dienstes der Domänenebene

Das Organisationsdomäne Forest-Modell ermöglicht die Delegierung von Autorität für die dienstverwaltung auf Domänenebene. Die folgende Tabelle enthält die Typen der dienstverwaltung, die auf der Domänenebene gesteuert werden kann.  

|Typ der dienstverwaltung|Zugeordneten Aufgaben|  
|------------------------------|--------------------|  
|Verwaltung von den Betrieb von Domänencontrollern|– Erstellen und Entfernen von Domänencontrollern<br />-Überwachung die Funktionsweise von Domänencontrollern<br />– Verwalten von Diensten, die auf einem Domänencontroller ausgeführt werden<br />– Sichern und Wiederherstellen des Verzeichnisses|  
|Konfiguration der Einstellungen für die gesamte Domäne|-Erstellen von Domänen- und Domänenbenutzer Kontorichtlinien, z. B. Kennwort, Kerberos und Kontosperrungsrichtlinien<br />– Erstellen und Anwenden von Gruppenrichtlinien domänenweite|  
|Delegierung der Verwaltung der Datenebene|-Erstellen von Organisationseinheiten (OUs) und das Delegieren der Verwaltung<br />-Lösung von Problemen in der OE-Struktur, die Besitzer der OU keine ausreichende Zugriffsrechte zum Beheben|  
|Verwaltung von Vertrauensstellungen|-Einrichten von Vertrauensstellungen mit Domänen außerhalb der Gesamtstruktur|  

Andere Arten von Servicemanagement, z. B. Schema oder die Verwaltung von Replikationstopologien, sind die Verantwortung für den Gesamtstrukturbesitzer.  

## <a name="domain-owner"></a>Domänenbesitzer

Bei einem Modell Organisationsdomäne Gesamtstruktur dienen Domänenbesitzer Dienstverwaltungsaufgaben auf Domänenebene. Domänenbesitzer sind berechtigt, über die gesamte Domäne sowie Zugriff auf alle anderen Domänen in der Gesamtstruktur. Aus diesem Grund müssen der Domänenbesitzer vertrauenswürdigen Personen, die durch den Gesamtstrukturbesitzer ausgewählt sein.  

Delegieren der dienstverwaltung von Domänenebenen-auf einem Besitzer, wenn die folgenden Bedingungen erfüllt sind:  

- Alle Gruppen, die Teilnahme an der Gesamtstruktur vertrauen, der Besitzer der neuen Domäne und den Service Management-Methoden der neuen Domäne.  

- Der Besitzer der neuen Domäne vertraut der Gesamtstrukturbesitzer und alle anderen Domänenbesitzer.  

- Alle Domänenbesitzer in der Gesamtstruktur zustimmen, dass der Besitzer der neuen Domäne verfügt, Administrator-dienstverwaltung und Richtlinien zur Serverauswahl und Methoden, die gleich oder strenger als ihre eigenen.  

- Alle Domänenbesitzer in der Gesamtstruktur stimmen zu, dass Domänencontroller, die von der Besitzer der neuen Domäne in der neuen Domäne verwaltet werden, physisch sicher sind.  

Beachten Sie, dass wenn eine Gesamtstruktur Besitzer Delegaten auf Domänenebene dienstverwaltung auf einem Besitzer, andere Gruppen können nicht zu dieser Gesamtstruktur zu verknüpfen, wenn sie nicht die Domänenbesitzer vertrauen.  

Alle Domänenbesitzer müssen bewusst sein, wenn eine dieser Bedingungen in der Zukunft ändern, es notwendig ist, verschieben die Organisationen Domänen in einer Bereitstellung mit mehreren Gesamtstrukturen werden könnten.  

> [!NOTE]  
> Eine weitere Möglichkeit zum Minimieren von Sicherheitsrisiken für eine Windows Server 2008 Active Directory-Domäne ist der administratorrollentrennung, einsetzen, die die Bereitstellung von einem schreibgeschützten Domänencontroller (RODC) in Ihrer Active Directory-Infrastruktur erforderlich ist. Einen RODC handelt es sich um eine neue Art von Domänencontroller im Windows Server 2008-Betriebssystem, das schreibgeschützten Partitionen der Active Directory-Datenbank hostet. Vor der Veröffentlichung von Windows Server 2008 mussten alle Server-Wartungsarbeiten auf einem Domänencontroller von einem Domänenadministrator ausgeführt werden. In Windows Server 2008 können Sie für einen RODC an jeden Domänenbenutzer lokale Administratorrechte delegieren, ohne dass diesem Benutzer keine administrativen Rechte für die Domäne oder andere Domänencontroller gewährt. Dies ermöglicht den delegierten Benutzer, melden Sie sich bei einem RODC, und führen Sie die Wartungsarbeiten, wie z. B. das Aktualisieren eines Treibers, auf dem Server. Allerdings kann nicht diesen delegierten Benutzer melden Sie sich auf alle anderen Domänencontroller oder andere administrative Aufgaben ausführen, in der Domäne. Auf diese Weise können beliebige vertrauenswürdige Benutzer kann sein delegiert die Möglichkeit, den RODC effektiv zu verwalten, ohne Beeinträchtigung der Sicherheits den Rest der Domäne. Weitere Informationen zu RODCs finden Sie unter [AD DS: Read-Only Domain Controller](https://go.microsoft.com/fwlink/?LinkId=106616).  
