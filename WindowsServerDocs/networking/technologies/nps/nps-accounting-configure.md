---
title: Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver Netzwerk
description: Dieses Thema enthält Informationen zur Textdatei und SQL Server-Protokollierung für Netzwerkrichtlinienserver in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: dfde2e21-f3d5-41e8-8492-cb3f0d028afb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 69341e30d90ee1be29c40d835a4f71fe433c11dc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver Netzwerk

Es gibt drei Arten der Protokollierung für den Netzwerkrichtlinienserver \(NPS\):

- **Ereignisprotokollierung**. In erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen verwendet. Sie können NPS-Ereignis Protokollierung, indem Sie die Eigenschaften des NPS-Server in der NPS-Konsole abrufen konfigurieren.

- **Protokollierung der Benutzerauthentifizierung und kontoführungsanforderungen in einer lokalen Datei**. Wird in erster Linie für Verbindung Analyse und Abrechnung verwendet. Auch hilfreich, als ein Sicherheitstool für die Untersuchung, da Sie eine Methode für das Überwachen der Aktivitäten eines böswilligen Benutzers nach einem Angriff erhalten. Sie können lokale dateiprotokollierung mithilfe des Assistenten Kontoführung konfigurieren.

- **Protokollierung der Benutzerauthentifizierung und kontoführungsanforderungen mit einer Microsoft SQL Server-XML-kompatiblen Datenbank**. Wird verwendet, um mehrere Server mit NPS an eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server-Protokollierung mithilfe des Accounting Konfigurations-Assistenten konfigurieren.

## <a name="use-the-accounting-configuration-wizard"></a>Verwenden der Buchhaltung Konfigurations-Assistenten

Mithilfe der Buchhaltung Konfigurations-Assistenten können Sie die folgenden vier Buchhaltung Einstellungen konfigurieren:

- **Nur SQL-Protokollierung**. Mit dieser Einstellung können Sie einen Datenlink zu einer SQL Server konfigurieren, mit dem NPS herstellen und Kontoführungsdaten an SQLServer senden können. Darüber hinaus kann der Assistent die Datenbank konfigurieren, auf dem SQL Server, um sicherzustellen, dass die Datenbank mit NPS-SQL Server-Protokollierung kompatibel ist.
- **Text Protokollierung nur**. Mit dieser Einstellung können Sie NPS zum Protokollieren von Ressourcenerfassungsdaten in einer Textdatei konfigurieren.
- **Parallele Protokollierung**. Mit dieser Einstellung können Sie den Link für SQL Server-Daten und die Datenbank konfigurieren. Sie können auch konfigurieren, Text Datei protokolliert, sodass NPS gleichzeitig an die Textdatei und SQL Server-Datenbank protokolliert. 
- **SQL-Protokollierung mit Sicherung**. Mit dieser Einstellung können Sie den Link für SQL Server-Daten und die Datenbank konfigurieren. Darüber hinaus können Sie Text dateiprotokollierung konfigurieren, die NPS verwendet, wenn SQL Server-Protokollierung ein Fehler auftritt.

Zusätzlich zu diesen Einstellungen können SQL Server-Protokollierung und textprotokollierungs-Sie angeben, ob weiterhin NPS verbindungsanforderungen zu verarbeiten, falls die Protokollierung ein Fehler auftritt. Geben Sie diese in der **Protokollierung Fehler aktionsabschnitt** in lokalen Protokollierung Dateieigenschaften ist in SQL Server-Protokollierungseigenschaften und während der Buchhaltung Konfigurations-Assistent ausgeführt wird.

### <a name="to-run-the-accounting-configuration-wizard"></a>Zum Ausführen des Assistenten Accounting

Führen Sie den Accounting Konfigurations-Assistenten führen Sie die folgenden Schritte aus:

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Detailbereich in **Accounting**, klicken Sie auf **Kontoführung konfigurieren**.

## <a name="configure-nps-log-file-properties"></a>Konfigurieren von NPS-Protokolldateieigenschaften

Sie können (Network Policy Server, NPS) zum Ausführen von Remote Authentication Dial-in User Service (RADIUS) Kontoführung für Benutzer authentifizierungsanforderungen, Access-Accept-Nachrichten, Nachrichten Zugriff ablehnen, kontoführungsanforderungen und Antworten und regelmäßige Statusupdates konfigurieren. Dieses Verfahrens können Sie die Protokolldateien konfigurieren, in denen Sie Daten speichern möchten.

Weitere Informationen zur Interpretation von Protokolldateien finden Sie unter [interpretieren NPS Format Datenbankprotokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

Um zu verhindern, dass die Protokolldateien die Festplatte ausfüllen, wird dringend empfohlen, dass Sie sie auf einer Partition gespeichert, die von der Systempartition getrennt ist. Im folgenden finden Sie weitere Informationen zum Konfigurieren der Kontoführung für den NPS:

- Um die Protokolldateien für die Sammlung von einem anderen Prozess zu senden, können Sie NPS zum Schreiben einer named Pipe konfigurieren. Um named Pipes verwenden, legen Sie Ordner für die Protokolldatei auf \\.\pipe oder \\ComputerName\pipe. Named Pipe erstellt-Server eine named Pipe namens \\.\pipe\iaslog.log um die Daten zu akzeptieren. Klicken Sie im Dialogfeld Eigenschaften lokale Datei im Erstellen einer neuen Protokolldatei, wählen Sie niemals (unbegrenzte Dateigröße) Wenn Sie named Pipes verwenden.

- Das Verzeichnis für Protokolldateien kann mithilfe von Systemumgebungsvariablen (anstelle von Benutzervariablen), z. B. % SystemDrive%, %SystemRoot% und % Windir% erstellt werden. Die folgende Pfad und die Umgebung Variable windir%, sucht z. B. das Verzeichnis die Protokolldatei in den Unterordner \System32\Logs (d. h. % windir%\System32\Logs\).

- Wechseln zwischen Protokolldateiformate bewirkt nicht, eine neue Protokolldatei erstellt werden soll. Wenn Sie die Protokolldateiformate ändern, enthält die Datei, die zum Zeitpunkt der Änderung aktiv ist eine Mischung aus den beiden Formaten (Einträge am Anfang des Protokolls haben das vorherige Format und Einträge am Ende des Protokolls werden das neue Format haben).

- Wenn RADIUS-Kontoführung aufgrund einer vollständigen Festplatte oder aus anderen Gründen ein Fehler auftritt, beendet NPS verbindungsanforderungen, verhindert, dass Benutzer den Zugriff auf Netzwerkressourcen.

- NPS bietet die Möglichkeit zur Anmeldung an eine Microsoft® SQL Server™-Datenbank zusätzlich oder anstelle der Protokollierung in einer lokalen Datei.

Mitgliedschaft in der **Domänen-Admins** Gruppe ist mindestens erforderlich, um dieses Verfahren auszuführen.


### <a name="to-configure-nps-log-file-properties"></a>So konfigurieren Sie die Eigenschaften der NPS-Protokolldatei

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Detailbereich in **Protokolldateieigenschaften**, klicken Sie auf **Protokolldateieigenschaften ändern**. Die **Protokolldateieigenschaften** Dialogfeld wird geöffnet.
4. In **Protokolldateieigenschaften**auf die **Einstellungen** Registerkarte **melden Sie sich die folgende Informationen**, stellen Sie sicher, dass Sie ausreichend Informationen zum Erreichen Ihrer Ziele Kontoführung melden möchten. Wenn die Protokolle Sitzungskorrelation ausführen, wählen Sie z. B. alle Kontrollkästchen.
5. In **Fehler bei der Aktion**Option **Protokollierung ein Fehler auftritt, verwerfen verbindungsanforderungen** Sie ggf. auf hält die Verarbeitung der Zugriffsanforderung Nachrichten bei der Protokolldateien aus irgendeinem Grund vollständig oder nicht verfügbar sind. Wenn NPS weiter Verbindungsanfragen verarbeitet, wenn Fehler protokolliert werden sollen, wählen Sie dieses Kontrollkästchen nicht.
6. In der **Protokolldateieigenschaften** Dialogfeld, klicken Sie auf die **Protokolldatei** Registerkarte.
7. Auf der **Protokolldatei** Registerkarte **Verzeichnis**, geben Sie den Speicherort, in denen NPS-Protokolldateien gespeichert werden sollen. Der Standardspeicherort ist der Ordner systemroot\System32\LogFiles.
    >[!NOTE]
    >Wenn Sie eine vollständigen Pfad-Anweisung in nicht angeben **Protokolldateiverzeichnis**, wird der Standardpfad verwendet. Angenommen, Sie geben **NPSLogFile** in **Protokolldateiverzeichnis**, die Datei befindet sich unter systemroot%\System32\NPSLogFile.
8. In **Format**, klicken Sie auf **DTS-kompatiblen**. Wenn Sie es vorziehen, können Sie stattdessen auswählen legacy-Dateiformat, z. B. **ODBC-\(Legacy\)** oder **IAS \(Legacy\)**.
    >[!NOTE]
    >**ODBC** und **IAS** ältere Dateitypen enthalten eine Teilmenge der Informationen, die NPS an die SQL Server-Datenbank gesendet. Die **DTS-kompatiblen** Dateityp des XML-Format ist identisch mit der XML-Format, die NPS verwendet, um Daten in der SQL Server-Datenbank importieren. Aus diesem Grund die **DTS-kompatiblen** Dateiformat bietet mehr effiziente und vollständige Übertragung von Daten in der standardmäßigen SQL Server-Datenbank für den NPS.
9. In **erstellen Sie eine neue Protokolldatei**, zum Konfigurieren von NPS Starten neuer Protokolldateien in festgelegten Intervallen, klicken Sie auf das Intervall, das Sie verwenden möchten:
    - Für hohe Volumen und Protokollierung von Aktivitäten, klicken Sie auf **tägliche**.
    - Für weniger Transaktions- und Protokollierung von Aktivitäten, klicken Sie auf **wöchentlichen** oder **monatlichen**.
    - Um alle Transaktionen in eine Protokolldatei zu speichern, klicken Sie auf **nie \(unlimited file size\)**.
    - Um die Größe der Protokolldateien zu begrenzen, klicken Sie auf **Wenn diese Größe erreicht**, und geben Sie dann eine Größe, nach denen ein neues Protokoll erstellt wird. Die Standardgröße beträgt 10 Megabyte (MB).
10. Wenn Sie möchten NPS So löschen Sie alte Protokolldateien, um Speicherplatz für neue Protokolldateien zu erstellen, wenn die Festplatte in der Nähe Kapazität ist, stellen Sie sicher, dass **beim Datenträger ist voll Löschen alte Protokolldateien** ausgewählt ist. Diese Option ist verfügbar, jedoch nicht, wenn der Wert der **erstellen Sie eine neue Protokolldatei** ist **nie \(unlimited file size\)**. Auch wenn die älteste Protokolldatei die aktuelle Protokolldatei ist, wird es nicht gelöscht.

## <a name="configure-nps-sql-server-logging"></a>Konfigurieren von NPS-SQL Server-Protokollierung

Sie können dieses Verfahren auf RADIUS-Kontoführungsdaten in eine lokale oder remote-Datenbank, die mit Microsoft SQL Server verwenden.

>[!NOTE]
>NPS-Formate Buchhaltungsdaten als XML-Dokument, die gesendet, die **Report_event** gespeicherte Prozedur in der SQL Server-Datenbank, die Sie auf dem Netzwerkrichtlinienserver festlegen. Für SQL Server-Protokollierung, um ordnungsgemäß zu funktionieren, benötigen Sie eine gespeicherte Prozedur namens **Report_event** in der SQL Server-Datenbank, die empfangen und analysieren die XML-Dokumente vom Netzwerkrichtlinienserver kann.

Mitglied der Gruppe Domänen-Admins oder einer entsprechenden Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-configure-sql-server-logging-in-nps"></a>So konfigurieren Sie SQL Server-Protokollierung im NPS

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Detailbereich in **SQL Server-Protokollierungseigenschaften**, klicken Sie auf **SQL Server-Protokollierungseigenschaften ändern**. Die **SQL Server-Protokollierungseigenschaften** Dialogfeld wird geöffnet.
4. In **melden Sie sich die folgende Informationen**, wählen Sie die Informationen, die Sie sich anmelden möchten: 
    - Um alle kontoführungsanforderungen protokollieren möchten, klicken Sie auf **kontoführungsanforderungen**.
    - Melden Sie sich authentifizierungsanforderungen, klicken Sie auf **authentifizierungsanforderungen**.
    - Wenn regelmäßigen kontoführungsstatus, klicken Sie auf **regelmäßigen kontoführungsstatus**.
    - Klicken Sie auf periodische Status, z. B. vorläufige kontoführungsanforderungen, melden Sie sich auf **periodische Status**.
5. Um die Anzahl gleichzeitiger Sitzungen, die zwischen des Servers mit NPS und SQL Server zu konfigurieren, geben Sie eine Zahl in **maximale Anzahl gleichzeitiger Sitzungen**.
6. So konfigurieren Sie die SQL Server-Datenquelle in **SQL Server-Protokollierung**, klicken Sie auf **konfigurieren**. Die **Datenverknüpfungseigenschaften** Dialogfeld wird geöffnet. Auf der **Verbindung** Registerkarte, geben Sie Folgendes: 
    - Geben Sie zum Angeben des Namens des Servers, auf dem die Datenbank gespeichert ist, oder wählen Sie einen Namen in **wählen, oder geben Sie einen Namen**.
    - Um die Authentifizierungsmethode für die Anmeldung an den Server anzugeben, klicken Sie auf **integrierte Sicherheit von Windows NT verwenden**. Klicken Sie auf **verwenden eine bestimmte Kombination aus Benutzername und Kennwort**, und geben Sie dann die Anmeldeinformationen in **Benutzernamen** und **Kennwort**.
    - Um ein leeres Kennwort zuzulassen, klicken Sie auf **leeres Kennwort**.
    - Um das Kennwort zu speichern, klicken Sie auf **Speichern des Kennworts zulassen**.
    - Um die Datenbank auf dem Computer mit SQL Server eine Verbindung mit anzugeben, klicken Sie auf **wählen Sie die Datenbank auf dem Server**, und wählen Sie dann aus der Liste einen Datenbanknamen an.
7. Um die Verbindung zwischen dem Netzwerkrichtlinienserver und SQL Server zu testen, klicken Sie auf **Verbindung testen**. Klicken Sie auf **OK** schließen **Datenverknüpfungseigenschaften**.
8. In **Fehler bei der Aktion**Option **Aktivieren der Protokollierung von Text-Datei für das Failover** ggf. NPS weiterhin mit Text Datei Protokollierung, wenn SQL Server-Protokollierung ein Fehler auftritt. 
9. In **Fehler bei der Aktion**Option **Protokollierung ein Fehler auftritt, verwerfen verbindungsanforderungen** Sie ggf. auf hält die Verarbeitung der Zugriffsanforderung Nachrichten bei der Protokolldateien aus irgendeinem Grund vollständig oder nicht verfügbar sind. Wenn NPS weiter Verbindungsanfragen verarbeitet, wenn Fehler protokolliert werden sollen, wählen Sie dieses Kontrollkästchen nicht.

## <a name="ping-user-name"></a>Ping-Benutzernamen

Einige RADIUS-Proxyserver und Netzwerkzugriffsserver senden-Authentifizierung und-Kontoführung Anforderungen (bekannt als pinganforderungen) in regelmäßigen Abständen zu überprüfen, ob der NPS-Server im Netzwerk vorhanden ist. Diese pinganforderungen enthalten fiktiven Benutzernamen. Wenn NPS diese Anforderungen verarbeitet werden, werden die Protokolle Ereignis und Kontoführung Zugriff ablehnen Datensätze, erschweren sie gültige Datensätze nachzuverfolgen gefüllt.

Wenn Sie einen Registrierungseintrag für konfigurieren **ping Benutzername**, NPS entspricht der Wert des Registrierungseintrags mit dem Benutzer Name-Wert in Pingen von Anforderungen von anderen Servern. Ein **ping Benutzername** Registrierungseintrag gibt den Namen des fiktiven Benutzer (oder ein Benutzer ein Namensmuster ein, mit Variablen, die den erfundenen Benutzernamen entspricht) gesendet werden, indem Sie RADIUS-Proxyserver und Netzwerkzugriffsserver. Wenn NPS Pingen von Anforderungen, die entsprechen erhält die **Benutzernamen ein ping** Wert des Registrierungseintrags, lehnt NPS die authentifizierungsanforderungen ohne Verarbeitung der Anforderung. NPS zeichnet Transaktionen im Zusammenhang mit dem erfundenen Benutzernamen in Protokolldateien, mit dessen Hilfe das Ereignisprotokoll einfacher zu interpretieren.

**Ping Benutzername** wird nicht standardmäßig installiert. Sie müssen hinzufügen **Benutzernamen ein ping** an der Registrierung. Sie können einen Eintrag in die Registrierung mithilfe des Registrierungs-Editor Hinzufügen.

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierungs kann schwere Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Daten auf dem Computer sichern.

### <a name="to-add-ping-user-name-to-the-registry"></a>Ping-Benutzername an der Registrierung hinzu

Ping-Benutzernamen kann den folgenden Registrierungsschlüssel einen Zeichenfolgenwert von einem Mitglied der lokalen Administratorgruppe hinzugefügt werden:

`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\IAS\Parameters`

- **Namen**: `ping user-name`
- **Typ**: `REG_SZ`
- **Daten**: *Benutzername*

>[!TIP]
>An, dass mehr als einen Benutzernamen für ein **ping Benutzername** Wert, geben Sie ein Namensmuster ein, z. B. einen DNS-Namen, einschließlich Platzhalterzeichen in **Daten**.
