---
title: Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver
description: Dieses Thema enthält Informationen zum Text-Datei und SQL Server-Protokollierung für Netzwerkrichtlinienserver unter Windows Server 2016.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: dfde2e21-f3d5-41e8-8492-cb3f0d028afb
ms.author: pashort
author: shortpatti
ms.date: 05/25/2018
ms.openlocfilehash: c732a9f42d942ad579468d1dd15d30324d6fea87
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839701"
---
# <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

Es gibt drei Arten der Protokollierung für Netzwerkrichtlinienserver \(NPS\):

- **Protokollierung von Komponentenereignissen**. Verwendet in erster Linie für die Überwachung und Problembehandlung von Verbindungsversuchen. Sie können NPS-ereignisprotokollierung durch Abrufen der NPS-Eigenschaften in der NPS-Konsole konfigurieren.

- **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in einer lokalen Datei**. In erster Linie für verbindungszwecke für Analyse und die Abrechnung verwendet. Auch hilfreich, als ein Sicherheitstool für die Untersuchung da er eine Methode zum Nachverfolgen der Aktivität von einem böswilligen Benutzer nach einem Angriff enthält. Sie können lokale dateiprotokollierung mithilfe des Assistenten Ressourcenerfassung konfigurieren.

- **Protokollierung von Benutzerauthentifizierung und kontoführungsanforderungen in eine Microsoft SQL Server-XML-kompatiblen Datenbank**. Wird verwendet, um mehrere Server mit NPS, damit eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server-Protokollierung konfigurieren, mit der Buchhaltung Konfigurations-Assistent.

## <a name="use-the-accounting-configuration-wizard"></a>Verwenden der Accounting-Konfigurations-Assistenten

Mit der Buchhaltung Konfigurations-Assistent, können Sie die folgenden vier buchhaltungs-Einstellungen konfigurieren:

- **Nur SQL-Protokollierung**. Mit dieser Einstellung können Sie eine datenverknüpfung mit einem SQL Server konfigurieren, die NPS zum Herstellen einer Verbindung mit und Senden von Ressourcenerfassungsdaten mit SQLServer ermöglicht. Darüber hinaus kann der Assistent die Datenbank konfigurieren, auf dem SQL Server, um sicherzustellen, dass die Datenbank mit der NPS-SQL Server-Protokollierung kompatibel ist.
- **Nur Text eine Protokollierung**. Mit dieser Einstellung können Sie NPS zum Protokollieren von Ressourcenerfassungsdaten in einer Textdatei konfigurieren.
- **Parallele Protokollierung**. Mit dieser Einstellung können Sie den Link für SQL Server-Daten und die Datenbank konfigurieren. Sie können auch konfigurieren, Text Datei protokolliert, sodass NPS gleichzeitig auf die Textdatei und der SQL Server-Datenbank protokolliert werden sollen. 
- **SQL-Protokollierung mit der Sicherung**. Mit dieser Einstellung können Sie den Link für SQL Server-Daten und die Datenbank konfigurieren. Darüber hinaus können Sie Text dateiprotokollierung konfigurieren, die NPS verwendet, wenn SQL Server-Protokollierung ein Fehler auftritt.

Zusätzlich zu diesen Einstellungen können sowohl SQL Server-Protokollierung und textprotokollierungs-Sie angeben, ob weiterhin, dass NPS verbindungsanforderungen zu verarbeiten, wenn die Protokollierung ein Fehler auftritt. Können Sie angeben, in der **protokollieren Fehler aktionsabschnitt** in lokale Protokollierungseigenschaften der Datei, in SQL Server-Protokollierungseigenschaften und während der Accounting-Konfigurations-Assistent ausgeführt wird.

### <a name="to-run-the-accounting-configuration-wizard"></a>Zum Ausführen des Assistenten für die Kontoführung-Konfiguration

Um den Konfigurations-Assistenten Ressourcenerfassung auszuführen, führen Sie die folgenden Schritte aus:

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Bereich "Details" im **Accounting**, klicken Sie auf **Kontoführung konfigurieren**.

## <a name="configure-nps-log-file-properties"></a>Konfigurieren von NPS Protokolldateieigenschaften

Sie können (Network Policy Server, NPS) zum Ausführen Remote Authentication Dial-In User Service (RADIUS) für authentifizierungsanforderungen, Access-Accept-Nachrichten, Access-Reject-Nachrichten, kontoführungsanforderungen gesendet und Antworten, Buchhaltung und regelmäßige konfigurieren. statusaktualisierungen. Sie können dieses Verfahren verwenden, so konfigurieren Sie die Protokolldateien in denen zum Speichern der Daten berücksichtigt werden sollen.

Weitere Informationen zur Interpretation der Protokolldateien finden Sie unter [Interpretieren von NPS-Format Protokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

Um zu verhindern, dass die Protokolldateien die Festplatte zu füllen, wird dringend empfohlen, dass Sie eine Partition behalten möchten, die von der Systempartition getrennt ist. Nachfolgend erhalten Sie weitere Informationen zum Konfigurieren von NPS berücksichtigt:

- Um die Protokolldaten für die Datei für die Sammlung von einem anderen Prozess zu senden, können Sie NPS zum Schreiben in eine benannte Pipe konfigurieren. Um die named Pipes verwenden, legen Sie Ordner für die Protokolldatei auf \\. \pipe oder \\ComputerName\pipe. Die named Pipe-Server-Anwendung erstellt eine benannte Pipe namens \\.\pipe\iaslog.log, die Daten anzunehmen. Im Dialogfeld Eigenschaften von lokalen Datei in das Erstellen einer neuen Protokolldatei nie wählen (unbegrenzte Dateigröße) bei Verwendung von named Pipes verwenden.

- Das Protokolldateiverzeichnis kann mithilfe von Umgebungsvariablen des Systems (anstelle von Benutzervariablen), z. B. %SystemDrive% %SystemRoot% und %Windir% erstellt werden. Z. B. mit der folgende Pfad an, mit der Umgebung Variable windir%, die Protokolldatei des Systemverzeichnisses sucht, in den Unterordner \System32\Logs (d. h. %windir%\System32\Logs\).

- Wechseln von Dateiformaten bewirkt nicht, ein neues Protokoll erstellt werden. Wenn Sie die Protokolldateiformate ändern, enthält die Datei, die zum Zeitpunkt der Änderung aktiv ist eine Mischung aus den beiden Formaten (Einträge am Anfang des Protokolls werden das vorherige Format, und Datensätze am Ende des Protokolls erhalten das neue Format).

- Wenn der RADIUS-Kontoführung aufgrund von einem vollständigen Festplattenlaufwerk oder andere Ursachen, die ein Fehler auftritt, beendet die NPS Verarbeitung verbindungsanforderungen, verhindert, dass Benutzer den Zugriff auf Netzwerkressourcen.

- NPS ermöglicht das in einer Microsoft® SQL Server™-Datenbank anstelle von oder zusätzlich zum Protokollieren in eine lokale Datei protokollieren.

Mitgliedschaft in der **Domänen-Admins** Gruppe ist die mindestvoraussetzung, um dieses Verfahren auszuführen.


### <a name="to-configure-nps-log-file-properties"></a>So konfigurieren Sie die Eigenschaften der NPS-Protokolldatei

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Bereich "Details" im **Protokolldateieigenschaften**, klicken Sie auf **Protokolldateieigenschaften ändern**. Die **Protokolldateieigenschaften** Dialogfeld wird geöffnet.
4. In **Protokolldateieigenschaften**auf die **Einstellungen** Registerkarte **melden Sie sich die folgende Informationen**, stellen Sie sicher, dass Sie genügend Informationen zum Erreichen Ihrer Ziele Buchhaltung protokollieren möchten. Falls Ihre Protokolle Sitzungskorrelation durchführen müssen, wählen Sie zum Beispiel alle Kontrollkästchen.
5. In **Protokollierung Fehleraktion**Option **Wenn Anmelden ein Fehler auftritt, verwerfen Sie verbindungsanforderungen** Wunsch NPS zum Beenden der Verarbeitung von Access-Request-Nachrichten, wenn Protokolldateien aus irgendeinem Grund vollständig oder nicht verfügbar sind. Wenn Sie NPS und weiter verarbeitet verbindungsanforderungen an, wenn ein Fehler auftritt anmelden möchten, aktivieren Sie dieses Kontrollkästchen nicht.
6. In der **Protokolldateieigenschaften** Dialogfeld klicken Sie auf die **Protokolldatei** Registerkarte.
7. Auf der **Protokolldatei** Registerkarte **Directory**, geben Sie den Speicherort, in denen NPS-Protokolldateien gespeichert werden sollen. Der Standardspeicherort ist der Ordner "systemroot\System32\LogFiles".<br>Wenn Sie keine vollständige Anweisung in angeben **Protokolldateiverzeichnis**, wird der Standardpfad verwendet. Angenommen, Sie geben ein **NPSLogFile** in **Protokolldateiverzeichnis**, die Datei befindet sich unter systemroot%\System32\NPSLogFile.
8. In **Format**, klicken Sie auf **DTS-kompatible**. Wenn Sie es vorziehen, können Sie stattdessen auswählen ein legacy-Dateiformat wie z. B. **ODBC \(ältere\)**  oder **IAS \(ältere\)**.<br>**ODBC** und **IAS** Legacydatei Typen enthalten, die eine Teilmenge der Informationen, die NPS an die SQL Server-Datenbank sendet. Die **DTS-kompatible** Dateityp des XML-Format ist identisch mit der XML-Format, mit denen NPS zum Importieren von Daten in einer SQL Server-Datenbank. Aus diesem Grund die **DTS-kompatible** -Dateiformat bietet eine effizientere und vollständige Übertragung von Daten in der standardmäßigen SQL Server-Datenbank für den NPS.
9. In **erstellen Sie eine neue Protokolldatei**, zum Konfigurieren von NPS neue Protokolldateien in festgelegten Intervallen zu starten, klicken Sie auf das Intervall, das Sie verwenden möchten:
    - Für umfangreichen Transaktions- und Protokollieren von Aktivitäten, klicken Sie auf **tägliche**.
    - Für kleinere Transaktionsvolumen und Protokollieren von Aktivitäten, klicken Sie auf **wöchentlichen** oder **monatliche**.
    - Um alle Transaktionen in einer Protokolldatei zu speichern, klicken Sie auf **nie \(unbegrenzte Dateigröße\)**.
    - Um die Größe der einzelnen Protokolldateien zu beschränken, klicken Sie auf **Wenn Protokolldatei diese Größe erreicht**, und geben Sie dann auf eine Größe, nach dem ein neues Protokoll erstellt wird. Die Standardgröße beträgt 10 Megabyte (MB).
10. Sollten Sie NPS So löschen Sie alte Protokolldateien, um Speicherplatz für neue Protokolldateien erstellen, wenn die Festplatte fast mit voller Kapazität ist, stellen Sie sicher, dass **beim Datenträger ist voll Löschen älterer-Protokolldateien** ausgewählt ist. Diese Option ist verfügbar, jedoch nicht, wenn der Wert des **erstellen Sie eine neue Protokolldatei** ist **nie \(unbegrenzte Dateigröße\)**. Darüber hinaus ist die älteste Protokolldatei die aktuelle Protokolldatei, wird er nicht gelöscht.

## <a name="configure-nps-sql-server-logging"></a>Konfigurieren von NPS SQL Server-Protokollierung

Sie können dieses Verfahren, um die Protokolldaten RADIUS-Kontoführung mit einer lokalen oder remote-Datenbank, die mit Microsoft SQL Server zu verwenden.

>[!NOTE]
>NPS-Buchhaltungsdaten Formate als XML-Dokument, die an gesendet der **Report_event** gespeicherten Prozedur in SQL Server-Datenbank, die Sie auf dem Netzwerkrichtlinienserver bestimmen. Für SQL Server-Protokollierung, um ordnungsgemäß zu funktionieren, müssen Sie eine gespeicherte Prozedur namens **Report_event** in der SQL Server-Datenbank, die empfangen und analysiert die XML-Dokumente von NPS kann.

Um dieses Verfahren auszuführen, ist mindestens die Mitgliedschaft in "Domänen-Admins" oder eine entsprechende Berechtigung erforderlich.

### <a name="to-configure-sql-server-logging-in-nps"></a>So konfigurieren Sie SQL Server-Protokollierung im NPS

1. Öffnen Sie die NPS-Konsole oder das NPS Microsoft Management Console (MMC)-Snap-in.
2. Klicken Sie in der Konsolenstruktur auf **Accounting**.
3. Klicken Sie im Bereich "Details" im **SQL Server-Protokollierungseigenschaften**, klicken Sie auf **SQL Server-Protokollierungseigenschaften ändern**. Die **SQL Server-Protokollierungseigenschaften** Dialogfeld wird geöffnet.
4. In **melden Sie sich die folgende Informationen**, wählen Sie die Informationen, die Sie protokollieren möchten: 
    - Um alle kontoführungsanforderungen protokollieren möchten, klicken Sie auf **kontoführungsanforderungen**.
    - Klicken Sie zum Protokollieren von authentifizierungsanforderungen **authentifizierungsanforderungen**.
    - Klicken Sie zum Protokollieren von regelmäßigen kontoführungsstatus auf **regelmäßigen kontoführungsstatus**.
    - Klicken Sie auf der periodische Status, z. B. vorläufigen kontoführungsanforderungen, melden Sie sich auf **periodische Status**.
5. Um die Anzahl gleichzeitiger Sitzungen zwischen dem Server mit NPS und der SQL Server zu konfigurieren, geben Sie eine Zahl im **maximale Anzahl gleichzeitiger Sitzungen**.
6. So konfigurieren Sie die SQL Server-Datenquelle in **SQL Server-Protokollierung**, klicken Sie auf **konfigurieren**. Die **Datenlinkeigenschaften** Dialogfeld wird geöffnet. Auf der **Verbindung** Registerkarte, geben Sie Folgendes: 
    - Um den Namen des Servers angeben, auf dem die Datenbank gespeichert ist, geben Sie ein, oder wählen Sie einen Namen in **wählen, oder geben Sie einen Servernamen**.
    - Um die Authentifizierungsmethode mit dem Melden Sie sich an den Server anzugeben, klicken Sie auf **Windows NT integrated Security verwenden**. Oder klicken Sie auf **bestimmten Benutzernamen und bestimmtes Kennwort**, und geben Sie dann die Anmeldeinformationen in **Benutzernamen** und **Kennwort**.
    - Um ein leeres Kennwort zu ermöglichen, klicken Sie auf **leeres Kennwort**.
    - Um das Kennwort zu speichern, klicken Sie auf **Speichern von Kennwort zulassen**.
    - Klicken Sie zum Angeben der Datenbank auf dem Computer mit SQL Server eine Verbindung mit **wählen Sie die Datenbank auf dem Server**, und wählen Sie dann einen Datenbanknamen aus der Liste.
7. Um die Verbindung zwischen NPS- und SQL Server zu testen, klicken Sie auf **Verbindung testen**. Klicken Sie auf **OK** schließen **Datenlinkeigenschaften**.
8. In **Protokollierung Fehleraktion**Option **Aktivieren der Protokollierung von Text-Datei für das Failover** Wunsch NPS, um den Vorgang fortzusetzen, mit Text Datei Protokollierung, wenn SQL Server-Protokollierung ein Fehler auftritt. 
9. In **Protokollierung Fehleraktion**Option **Wenn Anmelden ein Fehler auftritt, verwerfen Sie verbindungsanforderungen** Wunsch NPS zum Beenden der Verarbeitung von Access-Request-Nachrichten, wenn Protokolldateien aus irgendeinem Grund vollständig oder nicht verfügbar sind. Wenn Sie NPS und weiter verarbeitet verbindungsanforderungen an, wenn ein Fehler auftritt anmelden möchten, aktivieren Sie dieses Kontrollkästchen nicht.

## <a name="ping-user-name"></a>Ping-Benutzername

Einige RADIUS-Proxyserver und Netzwerkzugriffsserver sendeanforderungen in regelmäßigen Abständen Authentifizierung und Kontoführung (bekannt als Ping-Anforderungen), stellen Sie sicher, dass der NPS auf dem Netzwerk vorhanden ist. Diese Ping-Anforderungen werden fiktive Benutzernamen enthalten. Wenn NPS dieser Anforderungen verarbeitet, werden die Ereignis- und Kontoführung Protokolle mit Access-Reject-Datensätze, schwieriger zu verfolgen gültigen Datensätze gefüllt.

Bei der Konfiguration eines Registrierungseintrags für **Pingen Benutzername**, NPS entspricht der Wert des Registrierungseintrags für den Wert für den Benutzernamen in der Ping-Anforderungen von anderen Servern. Ein **Pingen Benutzername** Registrierungseintrag gibt den Benutzernamen der fiktiven (oder ein Benutzer ein Namensmuster ein, mit Variablen, die den Benutzernamen der fiktiven entspricht) gesendet werden, indem Sie RADIUS-Proxyserver und Netzwerkzugriffsserver. NPS empfängt beim Ping-Anforderungen, die entsprechen der **Pingen Benutzername** registrierungseintragswert, weist NPS den authentifizierungsanforderungen ohne Verarbeitung der Anforderung zurück. NPS zeichnet keine Transaktionen im Zusammenhang mit der fiktive Benutzername in der alle Protokolldateien im Ereignisprotokoll leichter interpretiert werden.

**Pingen Sie Benutzername** ist nicht standardmäßig installiert. Müssen Sie hinzufügen, **Pingen Benutzername** an der Registrierung. Sie können einen Eintrag in die Registrierung mithilfe des Registrierungs-Editor Hinzufügen.

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierung können ernsthafte Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

### <a name="to-add-ping-user-name-to-the-registry"></a>Ping-Benutzername in der Registrierung hinzufügen

Ping-Benutzername kann den folgenden Registrierungsschlüssel ein String-Wert von einem Mitglied der lokalen Gruppe "Administratoren" hinzugefügt werden:

`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\IAS\Parameters`

- **Namen**: `ping user-name`
- **Typ**: `REG_SZ`
- **Daten**:  *Benutzername*

>[!TIP]
>An mehr als einen Benutzernamen für ein **Pingen Benutzername** -Wert, geben Sie ein Namensmuster ein, z. B. einen DNS-Namen, einschließlich Platzhalterzeichen in **Daten**.
