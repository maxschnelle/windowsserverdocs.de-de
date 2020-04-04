---
title: Einrichten von Updatesynchronisierungen
description: 'Windows Server Update Service (WSUS)-Thema: Einrichten und Konfigurieren von Update synchronierungen'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddd5c395-451b-44a0-8e08-a05db26d2282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c7bca5be7a8ec0e857cba65680fbc3b967af4f8
ms.sourcegitcommit: 3c3dfee8ada0083f97a58997d22d218a5d73b9c4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2020
ms.locfileid: "80639752"
---
# <a name="setting-up-update-synchronizations"></a>Einrichten von Updatesynchronisierungen

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Während der Synchronisierung werden von einem WSUS-Server Updates (Aktualisieren von Metadaten und Dateien) aus einer Update Quelle heruntergeladen. Außerdem werden neue Produkt Klassifizierungen und-Kategorien heruntergeladen, sofern vorhanden. Wenn der WSUS-Server zum ersten Mal synchronisiert wird, werden alle Updates heruntergeladen, die Sie beim Konfigurieren der Synchronisierungs Optionen angegeben haben. Nach der ersten Synchronisierung lädt Ihr WSUS-Server nur Updates von der Update Quelle sowie Revisionen der Metadaten für vorhandene Updates und Ablauf Aktualisierungen für Updates herunter.

Das erste Mal, wenn ein WSUS-Server Updates herunterlädt, kann einige Zeit in Anspruch nehmen. Wenn Sie mehrere WSUS-Server einrichten, können Sie den Prozess bis zu einem gewissen Grad beschleunigen, indem Sie alle Updates auf einem WSUS-Server herunterladen und dann die Updates in die Inhaltsverzeichnisse der anderen WSUS-Server kopieren.

Sie können Inhalt aus dem Inhaltsverzeichnis eines WSUS-Servers in einen anderen kopieren. Der Speicherort des Inhaltsverzeichnisses wird angegeben, wenn Sie die WSUS-Installationsprozedur nach der Installation ausführen. Sie können das Tool "WSUSutil. exe" verwenden, um Update Metadaten von einem WSUS-Server in eine Datei zu exportieren. Anschließend können Sie diese Datei in andere WSUS-Server importieren.

## <a name="setting-up-update-synchronizations"></a>Einrichten von Updatesynchronisierungen
Die Seite **Optionen** ist der zentrale Zugriffspunkt in der WSUS-Verwaltungskonsole, mit dem Sie die Synchronisierung von Updates durch den WSUS-Server anpassen. Sie können angeben, welche Updates automatisch synchronisiert werden sollen, wo der Server Updates, Verbindungseinstellungen und der Synchronisierungs Zeitplan erhält. Sie können den Konfigurations-Assistenten auch über die Seite **Optionen** verwenden, um den WSUS-Server zu einem beliebigen Zeitpunkt zu konfigurieren oder neu zu konfigurieren.

### <a name="synchronizing-update-by-product-and-classification"></a>Synchronisieren von Updates nach Produkt und Klassifizierung
Ein WSUS-Server lädt Updates basierend auf den Produkten oder Produktfamilien (z. b. Windows oder Windows Server 2008, Datacenter Edition) und Klassifizierungen (z. b. kritische Updates oder Sicherheitsupdates) herunter, die Sie angeben. bei der ersten Synchronisierung werden vom WSUS-Server alle in den angegebenen Kategorien verfügbaren Updates heruntergeladen. In nachfolgenden synchronierungen werden von Ihrem WSUS-Server nur die neuesten Updates (oder Änderungen an den bereits auf dem WSUS-Server verfügbaren Updates) für die von Ihnen angegebenen Kategorien heruntergeladen.

Sie können auf der Seite **Optionen** unter **Produkte und Klassifizierungen**Update-Produkte und-Klassifizierungen angeben. Produkte werden in einer Hierarchie gruppiert nach Produktfamilie aufgelistet. Wenn Sie Windows auswählen, wählen Sie automatisch alle Produkte aus, die dieser Produkt Hierarchie unterliegen. Wenn Sie das übergeordnete Kontrollkästchen aktivieren, wählen Sie alle untergeordneten Elemente und alle zukünftigen Versionen aus. Wenn Sie die untergeordneten Kontrollkästchen aktivieren, werden die übergeordneten Kontrollkästchen nicht ausgewählt. Die Standardeinstellung für Produkte ist alle Windows-Produkte, und die Standardeinstellung für Klassifizierungen ist kritisch und Sicherheitsupdates.

Wenn ein WSUS-Server im Replikat Modus ausgeführt wird, sind Sie nicht in der Lage, diese Aufgabe auszuführen. Weitere Informationen zum Replikat Modus finden Sie unter [Ausführen des WSUS-Replikat Modus](running-wsus-replica-mode.md)und [Schritt 1: Vorbereiten der WSUS-Bereitstellung](../plan/plan-your-wsus-deployment.md).

##### <a name="to-specify-update-products-and-classifications-for-synchronization"></a>So geben Sie Update Produkte und Klassifizierungen für die Synchronisierung an

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf den Knoten **Optionen** .

2.  Klicken Sie auf **Produkte und Klassifizierungen**, und klicken Sie dann auf die Registerkarte **Produkte** .

3.  Aktivieren Sie die Kontrollkästchen für die Produkte oder Produktfamilien, die Sie mit WSUS aktualisieren möchten, und klicken Sie dann auf **OK**.

4.  Aktivieren Sie auf der Registerkarte **Klassifizierungen** die Kontrollkästchen der Update Klassifizierungen, die vom WSUS-Server synchronisiert werden sollen, und klicken Sie dann auf **OK**.

> [!NOTE]
> Produkte oder Klassifizierungen können auf die gleiche Weise entfernt werden. Der WSUS-Server beendet die Synchronisierung neuer Updates für die gelöschten Produkte. Updates, die für diese Produkte synchronisiert wurden, bevor Sie Sie löschen, verbleiben jedoch auf dem WSUS-Server und werden als verfügbar aufgeführt.
> 
> Um diese Produkte zu entfernen, lehnen Sie das Update ab, wie unter [Update Operations (Updates](updates-operations.md)) beschrieben, und entfernen Sie Sie dann mithilfe des [Assistenten zum Bereinigen von Servern](the-server-cleanup-wizard.md) .

### <a name="synchronizing-updates-by-language"></a>Synchronisieren von Updates nach Sprache
Der WSUS-Server lädt Updates basierend auf den von Ihnen angegebenen Sprachen herunter. Sie können Updates in allen Sprachen synchronisieren, in denen Sie verfügbar sind, oder Sie können eine Teilmenge von Sprachen angeben. Wenn Sie über eine Hierarchie von WSUS-Servern verfügen und Updates in verschiedenen Sprachen herunterladen müssen, stellen Sie sicher, dass Sie alle erforderlichen Sprachen auf dem Upstreamserver angegeben haben. Auf einem Downstream-Server können Sie eine Teilmenge der Sprachen angeben, die Sie auf dem Upstreamserver angegeben haben.

### <a name="synchronizing-updates-from-the-microsoft-update-catalog"></a>Synchronisieren von Updates aus dem Microsoft Update-Katalog
Ausführliche Informationen zum Synchronisieren von Updates vom Microsoft Update-Katalog Standort finden Sie unter [WSUS und der Katalog Website](wsus-and-the-catalog-site.md).

## <a name="configuring-proxy-server-settings"></a>Konfigurieren von Proxy Server Einstellungen
Sie können den WSUS-Server für die Verwendung eines Proxy Servers während der Synchronisierung mit einem Upstreamserver oder Microsoft Update konfigurieren. Diese Einstellung gilt nur, wenn die Synchronisierung auf dem WSUS-Server ausgeführt wird. Standardmäßig wird vom WSUS-Server versucht, eine direkte Verbindung mit dem Upstreamserver oder Microsoft Update herzustellen.

#### <a name="to-specify-a-proxy-server-for-synchronization"></a>So geben Sie einen Proxy Server für die Synchronisierung an

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **Update Quelle und Proxy Server**.

2.  Aktivieren Sie auf der Registerkarte **Proxy Server** das Kontrollkästchen **Proxy Server beim Synchronisieren verwenden** , und geben Sie dann den Server Namen und die Portnummer des Proxy Servers ein.

    > [!NOTE]
    > Konfigurieren Sie WSUS mit der Portnummer, für deren Verwendung der Proxy Server konfiguriert ist.

    -   Wenn Sie eine Verbindung mit dem Proxy Server mit bestimmten Benutzer Anmelde Informationen herstellen möchten, aktivieren Sie das Kontrollkästchen **Benutzer Anmelde Informationen zum Herstellen einer Verbindung mit dem Proxy Server verwenden** , und geben Sie dann den Benutzernamen, die Domäne und das Kennwort des Benutzers in die entsprechenden Felder ein.

    -   Wenn Sie für den Benutzer, der eine Verbindung mit dem Proxy Server herstellt, die Standard Authentifizierung aktivieren möchten, aktivieren Sie das Kontrollkästchen Standard **Authentifizierung zulassen (Kennwort wird in Klartext gesendet)** .

3.  Klicken Sie auf **OK**.

    > [!NOTE]
    > Da WSUS den gesamten Netzwerk Datenverkehr initiiert, ist es nicht erforderlich, die Windows-Firewall auf einem WSUS-Server zu konfigurieren, der direkt mit Microsoft Update verbunden ist.

## <a name="configuring-the-update-source"></a>Konfigurieren der Update Quelle
Die Update Quelle ist der Speicherort, von dem der WSUS-Server seine Updates abruft und Metadaten aktualisiert. Sie können angeben, dass die Update Quelle entweder Microsoft Update oder ein anderer WSUS-Server sein soll (der WSUS-Server, der als Update Quelle fungiert, ist der Upstream-Server, und der Server ist der Downstream-Server).

Zum Anpassen der Synchronisierung des WSUS-Servers mit der Update Quelle stehen folgende Optionen zur Verfügung:

-   Sie können einen benutzerdefinierten Port für die Synchronisierung angeben. Weitere Informationen zum Konfigurieren von Ports finden Sie unter [Schritt 3: Konfigurieren von WSUS](../deploy/2-configure-wsus.md) im WSUS-Bereitstellungs Handbuch.

-   Sie können Secure Socket Layer (SSL) verwenden, um die Synchronisierung von Update Informationen zwischen WSUS-Servern zu sichern. Weitere Informationen zur Verwendung von SSL finden Sie im Abschnitt "3,5. Sichern Sie WSUS mit dem Secure Sockets Layer-Protokoll "von [Schritt 3: Konfigurieren von WSUS](../deploy/2-configure-wsus.md) im WSUS-Bereitstellungs Handbuch.

## <a name="synchronizing-manually-or-automatically"></a>Manuelles oder Automatisches Synchronisieren
Sie können entweder den WSUS-Server manuell synchronisieren oder eine Uhrzeit für die automatische Synchronisierung angeben.

#### <a name="to-manually-synchronize-the-wsus-server"></a>So synchronisieren Sie den WSUS-Server manuell

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **Synchronisierungs Zeitplan**.

2.  Klicken Sie auf **manuell synchronisieren**, und klicken Sie dann auf **OK**.

#### <a name="to-set-up-an-automatic-synchronization-schedule"></a>So richten Sie einen Zeitplan für die automatische Synchronisierung ein

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **Synchronisierungs Zeitplan**.

2.  Klicken Sie auf **automatisch synchronisieren**.

3.  Wählen Sie bei der **ersten Synchronisierung**die Uhrzeit aus, zu der die Synchronisierung jeden Tag gestartet werden soll.

4.  Wählen Sie für **Synchronisierung pro Tag**die Anzahl der Synchronitäten aus, die Sie jeden Tag ausführen möchten. Wenn Sie z. b. vier synchronizierungen täglich um 3:00 Uhr morgens durchführen möchten, erfolgt die Synchronisierung um 3:00 Uhr, 9:00 Uhr, 3:00 Uhr und 9:00 Uhr. jeden Tag. (Beachten Sie, dass ein zufälliger Zeit Offset der geplanten Synchronisierungs Zeit hinzugefügt wird, um die Serververbindungen auf Microsoft Update zu versetzen.)

5.  Klicken Sie auf **OK**.

#### <a name="to-synchronize-your-wsus-server-immediately"></a>So synchronisieren Sie den WSUS-Server sofort

1.  Wählen Sie in der WSUS-Verwaltungskonsole den obersten Server Knoten aus.

2.  Klicken Sie im Bereich **Übersicht** unter **Synchronisierungs Status**auf **Jetzt synchronisieren**.

> [!NOTE]
> Die Synchronisierung wird vom Downstreamserver initiiert.
