---
ms.assetid: eb600904-24b8-4488-a278-c1c971dc2f2d
title: Planen der Platzierung regionaler Domänen Controller
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 574c5a4c0d009a34b1d327ac4aef3b9f5210b0bf
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959392"
---
# <a name="planning-regional-domain-controller-placement"></a>Planen der Platzierung regionaler Domänen Controller

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um die Kosteneffizienz zu gewährleisten, sollten Sie so viele regionale Domänen Controller wie möglich platzieren. Überprüfen Sie zunächst das Arbeitsblatt "geografische Standorte und Kommunikations Links" (DSSTOPO_1.doc), das zum [Erfassen von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) verwendet wird, um festzustellen, ob es sich um einen Hub handelt.

Planen Sie, regionale Domänen Controller für jede Domäne zu platzieren, die an jedem Hub-Standort repräsentiert wird. Wenn Sie regionale Domänen Controller an allen Hub-Standorten platzieren, sollten Sie die Notwendigkeit zum Platzieren regionaler Domänen Controller an Satellitenstandorten beurteilen. Wenn Sie unnötige regionale Domänen Controller von Satellitenstandorten entfernen, werden die für die Verwaltung einer Remote Serverinfrastruktur erforderlichen Supportkosten reduziert.

Stellen Sie außerdem sicher, dass die physische Sicherheit von Domänen Controllern an Hub-und Satellitenstandorten gewährleistet ist, sodass nicht autorisierte Mitarbeiter darauf zugreifen können. Platzieren Sie keine beschreibbaren Domänen Controller an einem Hub und Satellitenstandorten, an denen Sie die physische Sicherheit des Domänen Controllers nicht garantieren können. Eine Person, die überphysischen Zugriff auf einen beschreibbaren Domänen Controller verfügt, kann das System durch folgende Angriffe angreifen:

- Zugriff auf physische Datenträger durchstarten eines alternativen Betriebssystems auf einem Domänen Controller.
- Entfernen (und möglicherweise ersetzen) physischer Datenträger auf einem Domänen Controller.
- Abrufen und Bearbeiten einer Kopie der Systemstatus Sicherung eines Domänen Controllers.

Fügen Sie schreibgeschützte regionale Domänen Controller nur zu Standorten hinzu, an denen Sie Ihre physische Sicherheit gewährleisten können.

An Standorten mit unzureichender physischer Sicherheit ist die Bereitstellung eines schreibgeschützten Domänen Controllers (Read-Only Domain Controller, RODC) die empfohlene Lösung. Mit Ausnahme von Konto Kennwörtern enthält ein RODC alle Active Directory Objekte und Attribute, die ein Beschreib barer Domänen Controller enthält. Es können jedoch keine Änderungen an der Datenbank vorgenommen werden, die auf dem RODC gespeichert ist. Änderungen müssen an einem beschreibbaren Domänen Controller vorgenommen und dann zurück auf den RODC repliziert werden.

Zum Authentifizieren von Client Anmeldungen und des Zugriffs auf lokale Dateiserver platzieren die meisten Organisationen regionale Domänen Controller für alle regionalen Domänen, die an einem bestimmten Standort dargestellt werden. Sie müssen jedoch viele Variablen in Erwägung gezogen, wenn Sie bewerten, ob für einen geschäftlichen Standort die lokale Authentifizierung durch die Clients erforderlich ist oder die Clients die Authentifizierung und Abfrage über eine WAN-Verbindung (Wide Area Network) benötigen. Die folgende Abbildung zeigt, wie Sie bestimmen können, ob Domänen Controller an Satellitenstandorten platziert werden sollen.

![Planen der regionalen Domänen Controller Platzierung](media/Planning-Regional-Domain-Controller-Placement/49892c8c-2c99-4aab-92ba-808dbc8048e2.gif)

## <a name="onsite-technical-expertise-availability"></a>Verfügbarkeit technischer Fachkenntnissen vor Ort

Domänen Controller müssen aus verschiedenen Gründen kontinuierlich verwaltet werden. Platzieren Sie einen regionalen Domänen Controller nur an Standorten, die Personen enthalten, die den Domänen Controller verwalten können, oder stellen Sie sicher, dass der Domänen Controller Remote verwaltet werden kann.

In Zweigstellen Umgebungen, in denen normalerweise schlechte physische Sicherheit und Personal mit geringem Informationstechnologie-Know-how vorkommen, ist die Bereitstellung eines RODC häufig die empfohlene Lösung. Lokale Administrator Berechtigungen für einen RODC können an beliebige Domänen Benutzer delegiert werden, ohne dass diesem Benutzer Benutzerrechte für die Domäne oder andere Domänen Controller gewährt werden. Dadurch kann sich ein lokaler branchbenutzer bei einem RODC anmelden und Wartungsarbeiten auf dem Server durchführen, z. b. durch ein Upgrade eines Treibers. Der Verzweigungs Benutzer kann sich jedoch nicht bei einem anderen Domänen Controller anmelden oder andere administrative Aufgaben in der Domäne ausführen. Auf diese Weise kann dem Zweig Benutzer die Fähigkeit zur effektiven Verwaltung des RODC in der Zweigstelle delegiert werden, ohne die Sicherheit der übrigen Domäne oder der Gesamtstruktur zu beeinträchtigen.

## <a name="wan-link-availability"></a>WAN-Link Verfügbarkeit

WAN-Verknüpfungen, bei denen häufige Ausfälle auftreten, können den Benutzern einen erheblichen Produktivitätsverlust verursachen, wenn der Speicherort keinen Domänen Controller enthält, der die Benutzer authentifizieren kann. Wenn die Verfügbarkeit Ihres WAN-Links nicht 100 Prozent beträgt und Ihre Remote Standorte einen Dienstausfall nicht tolerieren können, platzieren Sie einen regionalen Domänen Controller an Standorten, an denen die Benutzer die Möglichkeit haben, sich anzumelden oder den Zugriff auf Exchange Server zu ermöglichen, wenn die WAN-Verbindung ausfällt.

## <a name="authentication-availability"></a>Verfügbarkeit der Authentifizierung

Bestimmte Organisationen (z. b. Banken) erfordern, dass Benutzer jederzeit authentifiziert werden. Platzieren Sie einen regionalen Domänen Controller an einem Speicherort, an dem die WAN-Link Verfügbarkeit nicht 100 Prozent beträgt, Benutzer jedoch jederzeit authentifiziert werden müssen.

## <a name="logon-performance-over-wan-links"></a>Anmelde Leistung über WAN-Verbindungen

Wenn die Verfügbarkeit von WAN-Verbindungen äußerst zuverlässig ist, hängt das Platzieren eines Domänen Controllers am Standort von den Anmelde Leistungsanforderungen über die WAN-Verbindung ab. Zu den Faktoren, die die Anmelde Leistung über das WAN beeinflussen, zählen die Verbindungsgeschwindigkeit und die verfügbare Bandbreite, die Anzahl von Benutzern und Verwendungs Profilen sowie der Umfang des Anmeldungs-und Replikations Datenverkehrs

### <a name="wan-link-speed-and-bandwidth-utilization"></a>WAN-Verbindungsgeschwindigkeit und Bandbreitenauslastung

Die Aktivitäten eines einzelnen Benutzers können eine langsame WAN-Verbindung erfassen. Platzieren Sie einen Domänen Controller an einem Speicherort, wenn die Anmelde Leistung über die WAN-Verbindung nicht zulässig ist.

Der durchschnittliche Prozentsatz der Bandbreitenauslastung gibt an, wie eine Netzwerkverbindung überlastet ist. Wenn eine Netzwerkverbindung eine durchschnittliche Bandbreitenauslastung hat, die größer als ein akzeptabler Wert ist, platzieren Sie einen Domänen Controller an diesem Speicherort.

### <a name="number-of-users-and-usage-profiles"></a>Anzahl von Benutzern und Verwendungs Profilen

Mithilfe der Anzahl der Benutzer und ihrer Verwendungs Profile an einem bestimmten Speicherort können Sie ermitteln, ob Sie regionale Domänen Controller an diesem Standort platzieren müssen. Um Produktivitätsverluste zu vermeiden, wenn ein WAN-Link ausfällt, platzieren Sie einen regionalen Domänen Controller an einem Standort, der über 100 oder mehr Benutzer verfügt.

Die Verwendungs Profile geben an, wie die Benutzer die Netzwerkressourcen verwenden. Sie müssen einen Domänen Controller nicht an einem Speicherort platzieren, der nur wenige Benutzer enthält, die nicht häufig auf Netzwerkressourcen zugreifen.

### <a name="logon-network-traffic-vs-replication-traffic"></a>Anmelden von Netzwerk Datenverkehr und Replikations Datenverkehr

Wenn ein Domänen Controller nicht innerhalb des gleichen Standorts wie der Active Directory Client verfügbar ist, erstellt der Client Anmelde Datenverkehr im Netzwerk. Der Umfang des Anmelde Netzwerk Datenverkehrs, der im physischen Netzwerk erstellt wird, wird durch verschiedene Faktoren beeinflusst, einschließlich Gruppenmitgliedschaften. Anzahl und Größe von Gruppenrichtlinie Objekten (GPOs); Anmelde Skripts; und Features wie Offline Ordner, Ordner Umleitung und Roamingprofile.

Auf der anderen Seite generiert ein Domänen Controller, der an einem bestimmten Speicherort platziert wird, Replikations Datenverkehr im Netzwerk. Die Häufigkeit und die Anzahl der Updates, die auf den auf den Domänen Controllern gehosteten Partitionen vorgenommen werden, beeinflussen die Menge an Replikations Datenverkehr, der im Netzwerk erstellt wird Zu den unterschiedlichen Aktualisierungs Typen, die auf den auf den Domänen Controllern gehosteten Partitionen vorgenommen werden können, zählen das Hinzufügen oder Ändern von Benutzern und Benutzer Attributen, das Ändern von Kenn Wörtern und das Hinzufügen oder Ändern globaler Gruppen, Drucker oder Volumes.

Um zu ermitteln, ob Sie einen regionalen Domänen Controller an einem Standort platzieren müssen, vergleichen Sie die Kosten für den von einem Standort ohne Domänen Controller erstellten Anmelde Datenverkehr im Vergleich zu den Kosten für den Replikations Datenverkehr, der durch Platzieren eines Domänen Controllers am Standort erstellt wurde

Nehmen wir beispielsweise an, ein Netzwerk mit Zweigstellen, die über langsame Verbindungen mit dem Hauptsitz verbunden sind und die Domänen Controller problemlos hinzugefügt werden können. Wenn der tägliche Anmelde-und Verzeichnis Such Datenverkehr einiger Remote Standort Benutzer mehr Netzwerk Datenverkehr als die Replikation aller Unternehmensdaten in den Branch verursacht, sollten Sie ggf. einen Domänen Controller zum Branch hinzufügen.

Wenn das Verringern der Kosten für die Verwaltung von Domänen Controllern wichtiger als der Netzwerkverkehr ist, zentralisieren Sie entweder die Domänen Controller für diese Domäne, und platzieren Sie keine regionalen Domänen Controller am Standort, oder platzieren Sie die RODCs am Standort.

Ein Arbeitsblatt, in dem Sie die Platzierung der regionalen Domänen Controller und die Anzahl der Benutzer für jede Domäne unterstützen können, die an den einzelnen Standorten repräsentiert wird, finden Sie unter [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608), herunterladen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip und Öffnen von "Domänen Controller Platzierung" (DSSTOPO_4.doc).

Sie müssen die Informationen zu Standorten, an denen Sie regionale Domänen Controller platzieren müssen, in Bezug auf die Bereitstellung regionaler Domänen untersuchen. Weitere Informationen zum Bereitstellen von regionalen Domänen finden Sie unter Bereitstellen von [regionalen Windows Server 2008-Domänen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755118(v=ws.10)).
