---
title: BranchCache-Bereitstellungshandbuch
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 3830b356-36d3-44f9-a1d7-990ff3e57403
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2868bfcca87f44ee9c29aa4c36de3486c660ee62
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989169"
---
# <a name="branchcache-deployment-guide"></a>BranchCache-Bereitstellungshandbuch

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In dieser Anleitung erfahren Sie, wie Sie BranchCache in Windows Server 2016 bereitstellen.

Zusätzlich zu diesem Thema enthält dieses Handbuch die folgenden Abschnitte.

-   [Auswählen eines BranchCache-Entwurfs](../../branchcache/plan/Choosing-a-BranchCache-Design.md)

-   [Bereitstellen von BranchCache](../../branchcache/deploy/Deploy-BranchCache.md)

## <a name="branchcache-deployment-overview"></a>BranchCache-Bereitstellungs Übersicht

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen von Windows Server 2016, Windows Server &reg; 2012 R2, Windows Server &reg; 2012, Windows Server &reg; 2008 R2 und zugehörigen Windows-Client Betriebssystemen enthalten ist.

Zur Verbesserung der WAN-Bandbreite kopiert BranchCache Inhalte von den Hauptinhaltsservern von Zweigstellen einer Organisation und erlaubt es Clientcomputern in diesen Zweigstellen, lokal und nicht über das WAN auf diese Inhalte zuzugreifen.

In Zweigstellen werden die Inhalte entweder auf Servern zwischengespeichert, auf denen das BranchCache-Feature von Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird. Wenn in der Zweigstelle keine Server verfügbar sind, werden die Inhalte auf Client Computern zwischengespeichert, auf denen Windows 10 &reg; , &reg; 8,1 Windows 8, Windows 8 oder Windows 7 ausgeführt wird &reg; .

Nachdem ein Client Computer Inhalte von der Hauptniederlassung oder dem cloudrechenzentrum angefordert und empfangen hat und die Inhalte in der Zweigstelle zwischengespeichert wurden, können andere Computer in derselben Zweigstelle den Inhalt lokal abrufen, anstatt über die WAN-Verbindung eine Verbindung mit dem Inhalts Server aufzunehmen.

**Vorteile der Bereitstellung von BranchCache**

Mit BranchCache werden Datei-, Web-und Anwendungs Inhalte in Zweigstellen Caches zwischengespeichert, sodass Client Computer über das lokale Netzwerk (Local Area Network, LAN) auf Daten zugreifen können, anstatt über langsame WAN-Verbindungen auf den Inhalt zuzugreifen.

BranchCache reduziert sowohl den WAN-Datenverkehr als auch die Zeit, die für Benutzer in Filialen zum Öffnen von Dateien im Netzwerk benötigt wird.  BranchCache stellt den Benutzern immer die aktuellsten Daten bereit und schützt die Sicherheit Ihrer Inhalte durch Verschlüsseln der Caches auf dem gehosteten Cache Server und auf Client Computern.

### <a name="what-this-guide-provides"></a>Inhalt dieses Handbuchs
Dieses Bereitstellungshandbuch zeigt Ihnen, wie BranchCache in den folgenden Modi bereitgestellt wird:

-   Modus "verteilter Cache". In diesem Modus laden Zweigstellen Client Computer Inhalte von den Inhalts Servern in der Hauptniederlassung oder der Cloud herunter und speichern den Inhalt für andere Computer in derselben Zweigstelle zwischen. Für den Modus für verteilte Caches ist in der Zweigstelle kein Servercomputer erforderlich.

-   Modus für gehostete Caches. In diesem Modus werden von Zweigstellen Client Computern Inhalt von den Inhalts Servern in der Hauptniederlassung oder der Cloud heruntergeladen, und von einem gehosteten Cache Server wird der Inhalt von den Clients abgerufen. Der gehostete Cache Server speichert dann den Inhalt für andere Client Computer zwischen.

Dieses Handbuch enthält auch Anweisungen zum Bereitstellen von drei Arten von Inhalts Servern. Inhalts Server enthalten den Quell Inhalt, der von Zweigstellen Client Computern heruntergeladen wird, und mindestens einen Inhalts Server ist erforderlich, um BranchCache in beiden Modi bereitzustellen. Es gibt die folgenden Typen von Inhaltsservern:

-   **Webserver basierte Inhalts Server**. Inhaltsserver dieses Typs senden Inhalte über HTTP und HTTPS an BranchCache-Clientcomputer. Auf diesen Inhalts Servern müssen die Versionen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden, die BranchCache unterstützen und auf denen das BranchCache-Feature installiert ist.

-   **Bits-basierte Anwendungsserver**. Diese Inhalts Server senden mithilfe der Bits (Bits) Inhalte an BranchCache-Client Computer. Auf diesen Inhalts Servern müssen die Versionen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden, die BranchCache unterstützen und auf denen das BranchCache-Feature installiert ist.

-   **Dateiserver basierte Inhalts Server**. Auf diesen Inhalts Servern müssen die Versionen Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt werden, die BranchCache unterstützen und auf denen die Server Rolle "Dateidienste" installiert ist. Außerdem muss der Rollen Dienst " **BranchCache für Netzwerkdateien** " der Server Rolle "Dateidienste" installiert und konfiguriert werden. Inhaltsserver dieses Typs senden Inhalte über SMB (Server Message Block) an BranchCache-Clientcomputer.

Weitere Informationen finden Sie unter [Betriebssystemversionen für BranchCache](../branchcache.md#bkmk_os).

### <a name="branchcache-deployment-requirements"></a>BranchCache-Bereitstellungs Anforderungen

Im folgenden finden Sie die Anforderungen für die Bereitstellung von BranchCache mithilfe dieses Handbuchs.

-   Auf **Datei-und Webinhalts Servern** muss eines der folgenden Betriebssysteme ausgeführt werden, um die BranchCache-Funktionalität bereitstellen zu können: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2. Windows 8-Clients und spätere Clients sehen weiterhin die Vorteile von BranchCache beim Zugriff auf Inhalts Server, auf denen Windows Server 2008 R2 ausgeführt wird. Sie können jedoch nicht die neuen Segmentierungs-und hashingtechnologien in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 nutzen.

-   Auf **Client Computern** muss Windows 10, Windows 8.1 oder Windows 8 ausgeführt werden, um das aktuellste Bereitstellungs Modell und die in Windows Server 2012 eingeführten Verbesserungen für das segmentieren und hashten nutzen zu können.

-   Auf **gehosteten Cache Servern** muss Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden, um die in diesem Dokument beschriebenen Verbesserungen für die Bereitstellung und Skalierungs Funktionen nutzen zu können.  Ein Computer, auf dem eines der Betriebssysteme ausgeführt wird, das als gehosteter Cache Server konfiguriert ist, kann weiterhin Client Computern unter Windows 7 bereitstellen. zu diesem Zweck muss er jedoch mit einem Zertifikat ausgestattet sein, das für die Transport Layer Security (TLS) geeignet ist, wie im Windows Server 2008 R2-und Windows 7 [BranchCache-Bereitstellungs Handbuch](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649232(v=ws.10))beschrieben.

-   **Eine Active Directory Domäne** ist erforderlich, um die automatische Ermittlung von Gruppenrichtlinie und gehosteten Caches zu nutzen, aber für die Verwendung von BranchCache ist keine Domäne erforderlich.  Sie können einzelne Computer mithilfe von Windows PowerShell konfigurieren. Außerdem ist es nicht erforderlich, dass auf Ihren Domänen Controllern Windows Server 2012 oder höher ausgeführt wird, um neue BranchCache-Gruppenrichtlinie Einstellungen zu nutzen. Sie können die BranchCache-Verwaltungsvorlagen auf Domänen Controllern importieren, auf denen frühere Betriebssysteme ausgeführt werden, oder Sie können die Gruppenrichtlinien Objekte Remote auf anderen Computern erstellen, auf denen Windows 10, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows 8 oder Windows Server 2012 ausgeführt wird.

-   **Active Directory Standorte** werden verwendet, um den Umfang von gehosteten Cache Servern einzuschränken, die automatisch ermittelt werden.  Um einen gehosteten Cache Server automatisch zu ermitteln, müssen sowohl der Client als auch der Server Computer demselben Standort angehören. BranchCache ist auf eine minimale Auswirkung auf Clients und Server ausgelegt und erzwingt keine zusätzlichen Hardwareanforderungen, die über diejenigen hinausgehen, die zum Ausführen der jeweiligen Betriebssysteme erforderlich sind.

**BranchCache-Verlauf und-Dokumentation**

BranchCache wurde erstmals in Windows 7 &reg; und Windows Server &reg; 2008 R2 eingeführt und wurde in Windows Server 2012, Windows 8 und höheren Betriebssystemen verbessert.

> [!NOTE]
> Wenn Sie BranchCache in anderen Betriebssystemen als Windows Server 2016 bereitstellen, sind die folgenden Dokumentations Ressourcen verfügbar.
>
> - Informationen zu BranchCache in Windows 8, Windows 8.1, Windows Server 2012 und Windows Server 2012 R2 finden Sie unter [Übersicht über BranchCache](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831696(v=ws.11)).
> - Informationen zu BranchCache in Windows 7 und Windows Server 2008 R2 finden Sie unter [BranchCache für Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd996634(v=ws.10)).