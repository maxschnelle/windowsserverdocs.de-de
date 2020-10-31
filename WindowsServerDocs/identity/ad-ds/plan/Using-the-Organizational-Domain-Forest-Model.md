---
ms.assetid: 093ef1ae-ebc1-490f-9fb1-2c000ce89eb6
title: Verwenden des Domänen Gesamtstruktur Modells der Organisation
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: 8300633d39e8ba7e5b19bfe8703d0cd9357423b4
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069142"
---
# <a name="using-the-organizational-domain-forest-model"></a>Verwenden des Domänen Gesamtstruktur Modells der Organisation

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Im Domänen Gesamtstruktur Modell der Organisation besitzen mehrere autonome Gruppen jeweils eine Domäne innerhalb einer Gesamtstruktur. Jede Gruppe steuert die Dienst Verwaltung auf Domänen Ebene, die es Ihnen ermöglicht, bestimmte Aspekte der Dienst Verwaltung autonom zu verwalten, während der Gesamtstruktur Besitzer die Dienst Verwaltung auf Gesamtstruktur Ebene steuert.

Die folgende Abbildung zeigt ein Domänen Gesamtstruktur Modell.

![Verwenden des Organisations Gesamtstruktur Modells "org"](../../media/Using-the-Organizational-Domain-Forest-Model/c50a3c6a-b0e4-43ec-ad62-f05d05f0bbd2.gif)

## <a name="domain-level-service-autonomy"></a>Dienst Autonomie auf Domänen Ebene

Das Domänen Gesamtstruktur Modell der Organisation ermöglicht die Delegierung der Zertifizierungsstelle für die Dienst Verwaltung auf Domänen Ebene. In der folgenden Tabelle werden die Typen der Dienst Verwaltung aufgelistet, die auf Domänen Ebene gesteuert werden können.

| Typ der Dienst Verwaltung | Zugehörige Aufgaben |
| -------------------------- |----------------- |
| Verwaltung von Domänen Controller Vorgängen    | -Erstellen und Entfernen von Domänen Controllern<br />-Überwachen der Funktionsweise von Domänen Controllern<br />-Verwalten von Diensten, die auf Domänen Controllern ausgeführt werden<br />-Sichern und Wiederherstellen des Verzeichnisses |
| Konfiguration von Domänen weiten Einstellungen         | -Erstellen von Domänen-und Domänen Benutzerkonto-Richtlinien, z. b. Kennwort, Kerberos und Konto Sperrungs Richtlinien<br />-Erstellen und Anwenden von Domänen weiten Gruppenrichtlinie |
| Delegierung von datenebenenverwaltung       | -Erstellen von Organisationseinheiten (OUs) und Delegieren der Verwaltung<br />-Reparieren von Problemen in der OE-Struktur, die Organisationseinheiten Besitzer nicht über ausreichende Zugriffsrechte für die Behebung verfügen |
| Verwaltung externer Vertrauens Stellungen | -Einrichten von Vertrauens Stellungen mit Domänen außerhalb der Gesamtstruktur |

Andere Arten der Dienst Verwaltung, z. b. die Schema-oder Replikations Topologieverwaltung, sind verantwortlich für den Gesamtstruktur Besitzer.

## <a name="domain-owner"></a>Domänen Besitzer

In einem Domänen Gesamtstruktur Modell von Organisationen sind Domänen Besitzer für Dienst Verwaltungsaufgaben auf Domänen Ebene verantwortlich. Domänen Besitzer verfügen über die Autorität für die gesamte Domäne sowie Zugriff auf alle anderen Domänen in der Gesamtstruktur. Aus diesem Grund müssen Domänen Besitzer vertrauenswürdige Personen sein, die vom Gesamtstruktur Besitzer ausgewählt werden.

Delegieren Sie die Dienst Verwaltung auf Domänen Ebene an einen Domänen Besitzer, wenn die folgenden Bedingungen erfüllt sind:

- Alle Gruppen, die an der Gesamtstruktur teilnehmen, vertrauen dem neuen Domänen Besitzer und den Dienst Verwaltungsmethoden der neuen Domäne.

- Der neue Domänen Besitzer vertraut dem Gesamtstruktur Besitzer und allen anderen Domänen Besitzern.

- Alle Domänen Besitzer in der Gesamtstruktur stimmen zu, dass der neue Domänen Besitzer über Dienst Administrator Verwaltung und Auswahl Richtlinien und-Methoden verfügt, die gleich oder strenger sind als ihre eigenen.

- Alle Domänen Besitzer in der Gesamtstruktur stimmen zu, dass Domänen Controller, die vom neuen Domänen Besitzer in der neuen Domäne verwaltet werden, physisch sicher sind.

Beachten Sie Folgendes: Wenn ein Gesamtstruktur Besitzer die Dienst Verwaltung auf Domänen Ebene an einen Domänen Besitzer delegiert, können andere Gruppen diese Gesamtstruktur nicht beitreten, wenn Sie dem Domänen Besitzer nicht vertrauen.

Alle Domänen Besitzer müssen sich bewusst sein, dass die Organisations Domänen in eine Bereitstellung mit mehreren Gesamtstrukturen verschoben werden können, wenn sich diese Bedingungen in der Zukunft ändern.

> [!NOTE]
> Eine weitere Möglichkeit zur Minimierung von Sicherheitsrisiken für eine Windows Server 2008-Active Directory Domäne besteht darin, die Administrator Rollen Trennung zu verwenden, die die Bereitstellung eines schreibgeschützten Domänen Controllers (Read-Only Domain Controller, RODC) in Ihrer Active Directory-Infrastruktur erfordert Ein RODC ist eine neue Art von Domänen Controller im Betriebssystem Windows Server 2008, das schreibgeschützte Partitionen der Active Directory-Datenbank hostet. Vor der Veröffentlichung von Windows Server 2008 musste jede Server Wartung auf einem Domänen Controller von einem Domänen Administrator ausgeführt werden. In Windows Server 2008 können Sie lokale Administrator Berechtigungen für einen RODC an beliebige Domänen Benutzer delegieren, ohne dass diesem Benutzer Administratorrechte für die Domäne oder andere Domänen Controller gewährt werden. Dies ermöglicht es dem Delegierten Benutzer, sich bei einem RODC anzumelden und Wartungsarbeiten wie das Upgrade eines Treibers auf dem Server auszuführen. Allerdings kann sich dieser Delegierte Benutzer nicht bei einem anderen Domänen Controller anmelden oder andere administrative Aufgaben in der Domäne ausführen. Auf diese Weise kann jeder vertrauenswürdige Benutzer die Fähigkeit zur effektiven Verwaltung des RODC delegieren, ohne die Sicherheit der übrigen Domäne zu beeinträchtigen. Weitere Informationen zu RODCs finden Sie unter [AD DS: Read-Only-Domänen Controllern](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732801(v=ws.10)).
