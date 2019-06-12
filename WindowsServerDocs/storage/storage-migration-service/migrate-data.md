---
title: Migrieren eines Dateiservers mit Storage-Migration-Dienst
description: Kurze Beschreibung des Thema suchmaschinenergebnissen
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 856eb7c2c2dfe0e0e3300fcf826e75b56258dc1b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447651"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Verwenden von Storage-Migration-Dienst zum Migrieren eines Servers

In diesem Thema wird erläutert, wie zum Migrieren eines Servers, einschließlich der Dateien und die Konfiguration zu einem anderen Server mit [Speicherung Datenbankmigrationsdienst](overview.md) und Windows Admin Center. Drei Schritte Migration verwendet werden, sobald Sie den Dienst installiert und alle erforderlichen Firewallports geöffnet haben: inventarisieren Sie Ihre Server, Übertragen von Daten und Übernahme in den neuen Servern.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>Dies ist Schritt 0: Installieren Sie Storage Migration-Dienst und überprüfen Sie die Firewall-ports

Bevor Sie beginnen, installieren Sie Storage Migration-Dienst aus, und stellen Sie sicher, dass die erforderlichen Firewallports geöffnet sind.

1. Überprüfen Sie die [Speicherung Datenbankmigrationsdienst Anforderungen](overview.md#requirements) und installieren Sie [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) auf dem PC oder einem Verwaltungsserver, sofern Sie noch nicht geschehen.
2. Verbinden Sie in Windows Admin Center mit der Orchestrator-Server unter Windows Server-2019. <br>Dies ist der Server, den Sie auf Storage-Migration-Dienst installieren und verwenden, um die Migration zu verwalten. Wenn Sie nur einen Server migrieren, können Sie den Zielserver, solange sie Windows Server-2019 ausgeführt wird. Es wird empfohlen, dass Sie einen separaten Orchestrierung-Server für alle Migrationen mit mehreren Servern verwenden.
1. Wechseln Sie zu **Server-Manager** (in Windows Admin Center) > **Speicherung Datenbankmigrationsdienst** , und wählen Sie **installieren** Storage Migration-Dienst und die erforderlichen Komponenten installieren (siehe Abbildung 1).
    ![Screenshot der Seite mit der Schaltfläche "installieren" Speicherung Datenbankmigrationsdienst](media/migrate/install.png) **Abbildung 1: Installieren von Storage-Migration-Dienst**
1. Installieren Sie den Storage-Migration-Dienst-Proxy auf alle Zielservern, die mit Windows Server-2019. Dies verdoppelt die Geschwindigkeit von dateiübertragungen bei der Installation auf den Zielservern. <br>Klicken Sie zu diesem Zweck eine Verbindung herstellen, auf den Zielserver in Windows Admin Center, und fahren Sie mit **Server-Manager** (in Windows Admin Center) > **Rollen und Features**Option **Storage Migration-Dienst Proxy**, und wählen Sie dann **installieren**.
1. Auf allen Servern source und auf jedem Zielserver unter Windows Server 2012 R2 oder Windows Server 2016 in Windows Admin Center, eine Verbindung mit jedem Server herstellen, wechseln Sie zu **Server-Manager** (in Windows Admin Center) > **Firewall**   >  **Eingehenden Regeln**, und klicken Sie dann überprüfen Sie, dass die folgenden Regeln aktiviert sind:
    - Datei- und Druckerfreigabe (SMB eingehend)
    - Der Netlogon-Dienst (NP eingehend)
    - Windows-Verwaltungsinstrumentation (DCOM-in)
    - Windows-Verwaltungsinstrumentation (WMI-In)

   > [!NOTE]
   > Wenn Sie Firewalls von Drittanbietern verwenden, sind die Bereiche der eingehende Port zu öffnen, TCP/445 (SMB), TCP/135 (RPC/DCOM-endpunktzuordnung) und TCP (kurzlebige Ports der RPC/DCOM) zwischen 1025 und 65535.

1. Wenn Sie einen Orchestrator-Server verwenden sind, um die Migration zu verwalten und Sie herunterladen, Ereignisse oder ein Protokoll darüber, welche Daten Sie übertragen möchten, überprüfen Sie, dass die Datei- und Druckerfreigabe (SMB eingehend)-Firewall-Regel auf dem Server ebenfalls aktiviert ist.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>Schritt 1: Erstellen Sie einen Auftrag und den Bestand Ihrer Server, um herauszufinden, was Sie migrieren

In diesem Schritt geben Sie an welche Server aus, um zu migrieren und dann überprüfen, um Informationen zu erfassen, auf die Dateien und Konfigurationen.

1. Wählen Sie **neuer Auftrag**, benennen Sie den Auftrag, und wählen Sie dann **OK**.
1. Auf der **Geben Sie Anmeldeinformationen** Seite, und geben Sie Administratoranmeldeinformationen, die arbeiten auf den Servern, die Sie aus migrieren möchten, und wählen Sie dann **Weiter**.
1. Wählen Sie **Hinzufügen eines Geräts**, geben Sie einen Quelle Servernamen ein, und wählen Sie dann **OK**. <br>Wiederholen Sie diesen Schritt für alle anderen Server, die Sie inventarisieren möchten.
1. Wählen Sie **Scanvorgang starten**.<br>Die Seite aktualisiert, wird angezeigt, wenn die Überprüfung abgeschlossen ist.
    ![Screenshot mit einem Server bereit, die überprüft werden](media/migrate/inventory.png) **Abbildung 2: Inventarisierung von Servern**
1. Wählen Sie jeden Server, überprüfen die Freigaben, Konfiguration, Netzwerkadapter und Volumes, die inventarisiert wurden. <br><br>Storage-Migration-Dienst wird nicht übertragen, Dateien oder Ordner, in denen wir wissen, dass Windows-Vorgang in dieser Version Sie Warnungen für alle Freigaben, die im Ordner "Windows System" werden also beeinträchtigen könnten. Sie müssen diese Freigaben während der Phase der Datenübertragung zu überspringen. Weitere Informationen finden Sie unter [welche Dateien und Ordner von Übertragungen ausgeschlossen sind](faq.md#excluded-files).
1. Wählen Sie **Weiter** , fahren Sie mit der Übertragung von Daten.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>Schritt 2: Übertragen von Daten von Ihren alten Servern auf dem Zielserver

In diesem Schritt werden die Daten nach dem angeben, wo Sie sie ablegen, auf dem Zielserver übertragen.

1. Auf der **Datenübertragung** > **Geben Sie Anmeldeinformationen** Seite, und geben Sie Administratoranmeldeinformationen, die arbeiten auf dem Zielserver zu migrieren möchten, und wählen Sie dann **Weiter**.
2. Auf der **fügen Sie ein Zielgerät und Zuordnungen hinzu** Seite, dem ersten Quellserver aufgelistet. Geben Sie den Namen des Servers, der Sie migrieren möchten und wählen Sie dann **Gerät überprüfen**.
3. Ordnen Sie die Quellvolumes an Zielvolumes, deaktivieren die **Include** Kontrollkästchen für alle Freigaben nicht möchten (einschließlich administrativen Freigaben, die sich in der Windows-Systemordner befindet) übertragen, und wählen Sie dann **weiter** .
   ![Screenshot mit einem Quellserver und die Volumes und Freigaben und, müssen sie auf übertragen werden, auf dem Ziel](media/migrate/transfer.png) **Abbildung 3: Ein Quell- und dem auf der Speicher übertragen werden sollen**
4. Fügen Sie einen Zielserver und Zuordnungen für alle Weitere Quellserver hinzu, und wählen Sie dann **Weiter**.
5. Optional anpassen, die übertragen von Einstellungen, und wählen Sie dann **Weiter**.
6. Wählen Sie **überprüfen** und wählen Sie dann **Weiter**.
7. Wählen Sie **Übertragung starten** um übertragen von Daten zu starten.<br>Beim ersten, die Sie übertragen, müssen wir alle vorhandenen Dateien in ein Ziel in einen Sicherungsordner verschieben. Für nachfolgende Übertragungen an wird standardmäßig wir das Ziel aktualisieren, ohne zuerst sichern. <br>Speicherung Datenbankmigrationsdienst ist darüber hinaus intelligent genug ist, für den Umgang mit sich überschneidenden Freigaben – es wird nicht die gleichen Ordnern zweimal im selben Auftrag kopieren.
8. Nachdem die Übertragung abgeschlossen ist, checken Sie den Zielserver, um sicherzustellen, dass alle Daten ordnungsgemäß übertragen. Wählen Sie **nur Fehler protokollieren** sollten Sie ein Protokoll aller Dateien herunterladen, die nicht zu übertragen.

   > [!NOTE]
   > Wenn Sie einen Audit-Trail von Übermittlungen beibehalten möchten oder beabsichtigen, mehr als eine Übertragung in einem Auftrag auszuführen, klicken Sie auf **Übertragungsprotokoll** um eine CSV-Kopie zu speichern. Jede nachfolgende Übertragung werden die Informationen von einer vorherigen Ausführung überschrieben. 

An diesem Punkt haben Sie drei Optionen:

- **Wechseln Sie mit dem nächsten Schritt**, über Ausschneiden, so dass der Zielserver die Identitäten der Source Server übernehmen.
- **Berücksichtigen Sie die Migration abgeschlossen** ohne Übernahme der Quellserver Identitäten.
- **Erneut übertragen**, kopieren nur Dateien, die seit der letzten Übertragung aktualisiert wurden.

Wenn Ihr Ziel ist es, die Dateien mit Azure synchronisiert werden, könnten Sie Einrichten der Zielserver mit Azure File Sync nach Übertragung von Dateien oder nach Cutting über auf dem Zielserver (finden Sie unter [Planung für eine Azure File Sync-Bereitstellung](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)).

## <a name="step-3-optionally-cut-over-to-the-new-servers"></a>Schritt 3: Übernahme optional auf die neuen Server

In diesem Schritt Übernahme Sie aus der Quellserver in dem Zielserver die IP-Adressen und die Computernamen auf dem Zielserver verschoben. Nachdem dieser Schritt abgeschlossen ist, Zugriff auf apps und Benutzer die neuen Server über die Namen und Adressen der Server, die, denen Sie migriert haben, aus.

 1. Wenn Sie von den migrationsauftrag aus, in Windows Admin Center, navigiert haben wechseln Sie zu **Server-Manager** > **Speicherung Datenbankmigrationsdienst** und wählen Sie dann den Auftrag, den Sie ausführen möchten. 
 1. Auf der **Übernahme in den neuen Servern** > **Geben Sie Anmeldeinformationen** Seite **Weiter** , die Anmeldeinformationen verwenden Sie zuvor eingegeben haben.
 1. Auf der **konfigurieren, die Umstellung** Seite Geben Sie der Netzwerkadapter jedes Quellgerät Einstellungen übernehmen. Dadurch wird die IP-Adresse aus der Quelle zum Ziel im Rahmen der Übernahme verschoben.
 1. Geben Sie an, welche IP-Adresse, um für den Quellserver nach der Umstellung wechselt die Adresse in das Ziel zu verwenden. Sie können DHCP oder eine statische Adresse verwenden. Eine statische Adresse verwendet, muss das neue Subnetz, dass die identisch mit dem alten Subnetz oder Übernahme fehl.
    ![Screenshot mit einem Quellserver und die IP-Adressen und Computernamen und was sie werden nach der Übernahme durch ersetzt werden](media/migrate/cutover.png)
    **Abbildung 4: Ein Quell- und wie die Netzwerkkonfiguration zum Ziel verschoben werden**
 1. Geben Sie den Quellserver umbenennen, nachdem Sie den Namen der Zielserver übernimmt. Sie können einen zufällig generierten Namen verwenden, oder geben selbst eine. Wählen Sie dann **Weiter**.
 1. Wählen Sie **Weiter** auf die **passen Sie die Umstellung Einstellungen** Seite.
 1. Wählen Sie **überprüfen** auf die **Validate-Quelle und Ziel-Gerät** Seite, und wählen Sie dann **Weiter**.
 1. Wenn Sie die Umstellung durchführen möchten, wählen Sie **Übernahme starten**. <br>Benutzer und apps möglicherweise unterbrochen, während die Adresse und den Namen verschoben werden und die Server neu gestartet mehrere Male jedes wurde, aber andernfalls nicht von der Migration betroffen. Wie lange Umstellung nimmt, hängt wie schnell die Server neu starten, sowie die Replikationszeiten von Active Directory und DNS.

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage-Migration Service](overview.md)
- [Storage Migration Services: häufig gestellte Fragen (FAQ)](faq.md)
- [Planung für eine Azure File Sync-Bereitstellung](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)