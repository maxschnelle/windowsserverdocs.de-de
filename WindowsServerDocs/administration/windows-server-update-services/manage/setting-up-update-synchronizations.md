---
title: Einrichten von Updatesynchronisierungen
description: Windows Server Update Service (WSUS)-Thema – wie einrichten und Konfigurieren des Update-Synchronisierung
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5fdfaaf1af2b74fe15530095700005a422b64986
ms.sourcegitcommit: a3958dba4c2318eaf2e89c7532e36c78b1a76644
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719627"
---
# <a name="setting-up-update-synchronizations"></a>Einrichten von Updatesynchronisierungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Während der Synchronisierung lädt ein WSUS-Server Updates (Aktualisieren von Metadaten und Dateien) von einer Updatequelle herunter. Es lädt ebenfalls herunter neue produktklassifikationen und Kategorien, sofern vorhanden. Wenn Ihr WSUS-Server zum ersten Mal synchronisiert wird, werden alle Updates heruntergeladen, die Sie angegeben werden, wenn Sie Optionen für die Synchronisierung konfiguriert. Nach der ersten Synchronisierung lädt Ihr WSUS-Server nur Updates aus der Quelle aktualisieren sowie Änderungen in den Metadaten für vorhandene Updates und Ablaufzeiten für Updates herunter.

Beim ersten ein WSUS-Server Updates herunterlädt dauert sehr lange. Wenn Sie mehrere WSUS-Server einrichten, können Sie den Prozess zu einem gewissen Grad beschleunigen von alle Updates auf einem WSUS-Server herunterladen, und klicken Sie dann die Updates in die Verzeichnisse der WSUS-Server kopiert.

Sie können Inhalte aus dem Verzeichnis des Websiteinhalts ein WSUS-Server auf einen anderen kopieren. Der Speicherort des Inhaltsverzeichnisses wird angegeben, wenn Sie die WSUS-Post-Installationsvorgang ausführen. Sie können die wsusutil.exe-Tools verwenden, Softwareupdate-Metadaten von einem WSUS-Server in einer Datei zu exportieren. Sie können diese Datei dann in andere WSUS-Server importieren.

## <a name="setting-up-update-synchronizations"></a>Einrichten von Updatesynchronisierungen
Die **Optionen** Seite ist der zentrale Punkt in der WSUS-Verwaltungskonsole zum Anpassen, wie Updates auf dem WSUS-Server synchronisiert wird. Sie können angeben, welche Updates automatisch synchronisiert werden, in dem Ihre Server erhält, Updates, Einstellungen und den Synchronisierungszeitplan festgelegt. Sie können auch den Konfigurations-Assistenten aus der **Optionen** Seite zu konfigurieren, oder konfigurieren Sie den WSUS-Server zu einem beliebigen Zeitpunkt neu.

### <a name="synchronizing-update-by-product-and-classification"></a>Synchronisieren von Updates nach Produkt und Klassifizierung
Ein WSUS-Server lädt die Updates, die anhand der Produkte oder Produktfamilien (z.B. Windows oder Windows Server 2008 Datacenter Edition) herunter und Klassifizierungen (z. B. kritische Updates oder Sicherheitsupdates), die Sie angeben. auf der ersten Synchronisierung lädt der WSUS-Server alle Updates zur Verfügung, in den Kategorien, die Sie angegeben haben. In folgenden Synchronisierungen Ihrer WSUS nur die neuesten Updates für Server-Downloads (oder Änderungen an die Updates bereits auf dem WSUS-Server verfügbar) für die Kategorien angegebenen.

Sie können die Update-Produkte und Klassifizierungen angeben, auf die **Optionen** Seite **Produkte und Klassifikationen**. Produkte werden in einer Hierarchie gruppiert nach Produktfamilie aufgelistet. Wenn Sie Windows auswählen, wählen Sie automatisch jedes Produkt, das unter diesem Produkthierarchie fällt. Durch Aktivieren des Kontrollkästchens für die übergeordnete wählen Sie alle Elemente unter dieser sowie allen zukünftigen Versionen. Wählen die untergeordneten Kontrollkästchen wird nicht die übergeordnete Kontrollkästchen. Die Standardeinstellung für Produkte sind alle Windows-Produkte und die Standardeinstellung für Klassifizierungen wichtig ist und Sicherheitsupdates.

Wenn ein WSUS-Server im Replikatmodus ausgeführt wird, werden Sie nicht zum Ausführen dieser Aufgabe können. Weitere Informationen zum Replikatmodus finden Sie unter [ausgeführten WSUS Replikatmodus](running-wsus-replica-mode.md), und [Schritt 1: Vorbereiten der WSUS-Bereitstellung](../plan/plan-your-wsus-deployment.md).

##### <a name="to-specify-update-products-and-classifications-for-synchronization"></a>Angeben von Updateprodukten und-Klassifizierungen für die Synchronisierung

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf der **Optionen** Knoten.

2.  Klicken Sie auf **Produkte und Klassifikationen**, und klicken Sie dann auf die **Produkte** Registerkarte.

3.  Wählen Sie die Kontrollkästchen für die Produkte und Produktfamilien, die Sie aktualisieren möchten mit WSUS, und klicken Sie dann auf **OK**.

4.  Auf der **Klassifizierungen** Registerkarte, die Kontrollkästchen der updateklassifizierungen, Sie möchten Ihre WSUS-Server synchronisieren, und klicken Sie dann auf **OK**.

> [!NOTE]
> Sie können die Produkte oder Klassifizierungen auf die gleiche Weise entfernen. Ihr WSUS-Server wird beendet, synchronisieren neue Updates für die Produkte, die Auswahl Sie aufgehoben haben. Updates, die für diese Produkte synchronisiert wurden, bevor Sie sie gelöscht wird allerdings bleibt auf dem WSUS-Server und werden als verfügbar aufgeführter.
> 
> Um diese Produkte zu entfernen, Ablehnen des Updates, wie im [Vorgänge für Updates](updates-operations.md), und verwenden Sie dann die [des Servers Bereinigung Assistenten](the-server-cleanup-wizard.md) um sie zu entfernen.

### <a name="synchronizing-updates-by-language"></a>Synchronisieren von Updates nach Sprache
Ihr WSUS-Server lädt die Updates, die auf Basis der Sprachen, die Sie angeben. Können Sie Updates in allen Sprachen, in denen sie verfügbar sind, synchronisieren, oder Sie können eine Teilmenge von Sprachen angeben. Wenn Sie eine Hierarchie von WSUS-Server verfügen, und Sie zum Herunterladen von Updates in verschiedenen Sprachen müssen, stellen Sie sicher, dass Sie alle benötigten Sprachen auf dem Upstreamserver angegeben haben. Auf eine downstream-Server können Sie eine Teilmenge von Sprachen angeben, die Sie auf dem Upstreamserver angegeben.

### <a name="synchronizing-updates-from-the-microsoft-update-catalog"></a>Synchronisieren von Updates von Microsoft Update-Katalog
Weitere Informationen zum Synchronisieren von Updates auf der Website von Microsoft Update-Katalog finden Sie unter: [WSUS und Katalog-Website](wsus-and-the-catalog-site.md).

## <a name="configuring-proxy-server-settings"></a>Konfigurieren von Proxyservereinstellungen
Sie können Ihr WSUS-Server um einen Proxyserver verwenden, während der Synchronisierung mit einem Upstreamserver oder Microsoft Update konfigurieren. Diese Einstellung gilt nur, wenn Ihr WSUS-Server Synchronisierungen ausgeführt wird. Standardmäßig versucht der WSUS-Server, die direkt mit dem Upstreamserver oder Microsoft Update herstellen.

#### <a name="to-specify-a-proxy-server-for-synchronization"></a>Zum Angeben eines Proxyservers zur Synchronisierung

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **Updatequelle und Proxyserver**.

2.  Auf der **Proxyserver** Registerkarte die **Proxyserver beim Synchronisieren von** Kontrollkästchen, und klicken Sie dann geben Sie den Namen des Servers und die Portnummer des Proxyservers.

    > [!NOTE]
    > Konfigurieren von WSUS mit die gleiche Portnummer, die den Proxyserver so konfiguriert ist, zu verwenden.

    -   Wenn Sie mit dem Proxyserver bestimmte Benutzeranmeldeinformationen eine Verbindung herstellen möchten, wählen Sie die **Benutzeranmeldeinformationen für die Verbindung mit dem Proxyserver verwenden** Kontrollkästchen, und geben Sie dann der Benutzername, Domäne und das Kennwort des Benutzers in die entsprechenden Felder .

    -   Wenn Sie die Standardauthentifizierung für den Benutzer, Herstellen einer Verbindung mit dem Proxyserver aktivieren möchten die **Standardauthentifizierung zulassen (Kennwort wird in Klartext gesendet)** Kontrollkästchen.

3.  Klicken Sie auf **OK**.

    > [!NOTE]
    > Da WSUS aller Netzwerkverkehr initiiert, besteht keine Notwendigkeit zum Konfigurieren von Windows-Firewall auf einem direkt mit Microsoft Update verbundenen WSUS-Server.

## <a name="configuring-the-update-source"></a>Konfigurieren der Updatequelle
Die Updatequelle ist der Speicherort, der aus dem Ihr WSUS-Server ruft seine Updates ab und Aktualisieren von Metadaten. Sie können angeben, dass die Updatequelle werden soll, entweder Microsoft Update oder einen anderen WSUS-Server (der WSUS-Server, die als Updatequelle der upstream-Server ist und der Server der Downstreamserver ist fungiert).

Die folgenden: Optionen zum Anpassen, wie Ihr WSUS-Server mit der Updatequelle synchronisiert wird

-   Sie können einen benutzerdefinierten Port für die Synchronisierung angeben. Informationen zum Konfigurieren von Ports finden Sie unter [Schritt 3: Konfigurieren von WSUS](../deploy/2-configure-wsus.md) im Bereitstellungshandbuch für WSUS.

-   Sie können Secure Socket Layer (SSL) verwenden, um sichere Synchronisation der Informationen zwischen WSUS-Servern. Weitere Informationen zur Verwendung von SSL finden Sie im Abschnitt "3.5. Sichere WSUS mit dem Secure Sockets Layer-Protokoll"der [Schritt 3: Konfigurieren von WSUS](../deploy/2-configure-wsus.md) im Bereitstellungshandbuch für WSUS.

## <a name="synchronizing-manually-or-automatically"></a>Synchronisieren manuell oder automatisch
Sie können den WSUS-Server manuell synchronisieren oder geben Sie eine Uhrzeit für sie automatisch zu synchronisieren.

#### <a name="to-manually-synchronize-the-wsus-server"></a>So synchronisieren Sie manuell auf den WSUS-server

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, und klicken Sie dann auf **Synchronisierungszeitplan**.

2.  Klicken Sie auf **manuell synchronisieren**, und klicken Sie dann auf **OK**.

#### <a name="to-set-up-an-automatic-synchronization-schedule"></a>Zum Einrichten eines Zeitplans für die automatische Synchronisierung

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**, klicken Sie dann auf **Synchronisierungszeitplan**.

2.  Klicken Sie auf **automatisch synchronisieren**.

3.  Für **erstsynchronisierung**, wählen Sie die Synchronisierung am Anfang jedes Tages angezeigt werden sollen.

4.  für **Synchronisierungen pro Tag**, wählen Sie die Anzahl der Synchronisierungen, die Sie täglich tun möchten. Beispielsweise sollten Sie vier Synchronisierungen ein Tag, die um 3:00 Uhr ab, dann wird Synchronisierungen um 3:00 Uhr, 9:00 Uhr, 15:00 Uhr und 21:00 Uhr jeden Tag. (Beachten Sie, dass es sich bei einem zufälligen Zeitpunkt Offset bis zum Zeitpunkt der geplanten Synchronisierung hinzugefügt werden wird, um Speicherplatz, die Server-Verbindungen zu Microsoft Update.)

5.  Klicken Sie auf **OK**.

#### <a name="to-synchronize-your-wsus-server-immediately"></a>So synchronisieren Sie sofort den WSUS-server

1.  Wählen Sie den obersten Serverknoten, klicken Sie auf der WSUS-Verwaltungskonsole.

2.  In der **Übersicht** Bereich unter **Synchronisierungsstatus**, klicken Sie auf **jetzt synchronisieren**.

> [!NOTE]
> Die Synchronisierung wird von der Downstreamserver initiiert.
