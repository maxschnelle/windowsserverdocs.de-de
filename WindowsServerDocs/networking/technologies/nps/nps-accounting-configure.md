---
title: Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver
description: Dieses Thema enthält Informationen zur Textdatei und SQL Server Protokollierung für den Netzwerk Richtlinien Server unter Windows Server 2016.
manager: dougkim
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: dfde2e21-f3d5-41e8-8492-cb3f0d028afb
ms.author: pashort
author: shortpatti
ms.date: 05/25/2018
ms.openlocfilehash: 0c154d4d4534f4c343107eecd158974b92903e39
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405571"
---
# <a name="configure-network-policy-server-accounting"></a>Konfigurieren der Kontoführung für den Netzwerkrichtlinienserver

Es gibt drei Arten der Protokollierung für den Netzwerk \(Richtlinien Server\)-NPS:

- **Ereignisprotokollierung**. Wird hauptsächlich für die Überwachung und Problembehandlung von Verbindungs versuchen verwendet. Sie können die NPS-Ereignisprotokollierung konfigurieren, indem Sie die NPS-Eigenschaften in der NPS-Konsole abrufen.

- **Protokollieren von Benutzerauthentifizierung und Buchhaltungs Anforderungen in einer lokalen Datei**. Wird hauptsächlich für Verbindungs Analyse und Abrechnungszwecke verwendet. Auch als Sicherheitsuntersuchung nützlich, da Sie eine Methode zum Nachverfolgen der Aktivität eines böswilligen Benutzers nach einem Angriff bereitstellt. Sie können die lokale Datei Protokollierung mit dem Konfigurations-Assistenten für die Buchhaltung konfigurieren.

- **Protokollieren von Benutzer Authentifizierungs-und Buchhaltungs Anforderungen in einer Microsoft SQL Server XML-kompatiblen Datenbank**. Wird verwendet, um mehreren Servern, auf denen NPS ausgeführt wird, eine Datenquelle zu ermöglichen. Bietet außerdem die Vorteile der Verwendung einer relationalen Datenbank. Sie können SQL Server Protokollierung mit dem Konfigurations-Assistenten für die Buchhaltung konfigurieren.

## <a name="use-the-accounting-configuration-wizard"></a>Verwenden des Buchhaltungs Konfigurations-Assistenten

Mit dem Konfigurations-Assistenten für die Buchhaltung können Sie die folgenden vier Buchhaltungs Einstellungen konfigurieren:

- **Nur SQL-Protokollierung**. Mit dieser Einstellung können Sie einen Daten Link zu einer SQL Server konfigurieren, die es NPS ermöglicht, eine Verbindung mit dem SQL-Server herzustellen und Buchhaltungsdaten zu senden. Außerdem kann der Assistent die Datenbank auf dem SQL Server konfigurieren, um sicherzustellen, dass die Datenbank mit der NPS SQL Server-Protokollierung kompatibel ist.
- **Nur Text Protokollierung**. Mit dieser Einstellung können Sie NPS so konfigurieren, dass Buchhaltungsdaten in einer Textdatei protokolliert werden.
- **Parallele Protokollierung**. Wenn Sie diese Einstellung verwenden, können Sie den SQL Server Daten Link und die Datenbank konfigurieren. Sie können auch die Protokollierung von Textdateien so konfigurieren, dass NPS sich gleichzeitig in der Textdatei und der SQL Server-Datenbank anmeldet. 
- **SQL-Protokollierung mit Backup**. Wenn Sie diese Einstellung verwenden, können Sie den SQL Server Daten Link und die Datenbank konfigurieren. Außerdem können Sie die Protokollierung von Textdateien konfigurieren, die NPS verwendet, wenn SQL Server Protokollierung fehlschlägt.

Zusätzlich zu diesen Einstellungen können Sie mit SQL Server Protokollierung und Text Protokollierung angeben, ob NPS weiterhin Verbindungsanforderungen verarbeitet, wenn die Protokollierung fehlschlägt. Sie können dies im **Abschnitt Protokollierungs Fehler Aktion** unter lokale Datei Protokollierungs Eigenschaften, in SQL Server-Protokollierungs Eigenschaften und während der Ausführung des Konfigurations-Assistenten für die Buchhaltung angeben.

### <a name="to-run-the-accounting-configuration-wizard"></a>So führen Sie den konfigurationskonfigurations-Assistenten aus

Führen Sie die folgenden Schritte aus, um den Konfigurations-Assistenten für die Buchhaltung auszuführen:

1. Öffnen Sie die NPS-Konsole oder das NPS-MMC-Snap-in (Microsoft Management Console).
2. Klicken Sie in der Konsolen Struktur auf **Buchhaltung**.
3. Klicken Sie im Detailbereich unter **Buchhaltung**auf Konto **Führung konfigurieren**.

## <a name="configure-nps-log-file-properties"></a>Konfigurieren von NPS-Protokolldatei Eigenschaften

Sie können den Netzwerk Richtlinien Server (Network Policy Server, NPS) für die Durchführung von Remote Authentication Dial-in User Service (RADIUS) für Benutzer Authentifizierungsanforderungen, Zugriffs Accept-Nachrichten, Zugriffs Ablehnungs Meldungen, Buchhaltungs Anforderungen und-Antworten sowie regelmäßige Statusaktualisierungen. Mit diesem Verfahren können Sie die Protokolldateien konfigurieren, in denen die Buchhaltungsdaten gespeichert werden sollen.

Weitere Informationen zum Interpretieren von Protokolldateien finden Sie unter [Interpretieren von NPS-Daten Bank Format-Protokolldateien](https://technet.microsoft.com/library/cc771748.aspx).

Um zu verhindern, dass die Protokolldateien die Festplatte auffüllen, wird dringend empfohlen, dass Sie Sie auf einer Partition aufbewahren, die von der Systempartition getrennt ist. Im folgenden finden Sie weitere Informationen zum Konfigurieren der Kontoführung für NPS:

- Um die Protokolldatei Daten für die Sammlung von einem anderen Prozess zu senden, können Sie NPS so konfigurieren, dass er in eine Named Pipe schreibt. Um Named Pipes zu verwenden, legen Sie den Protokolldatei \\Ordner auf .\pipe oder \\computername\pipefest. Das Named Pipe Server-Programm erstellt eine Named Pipe \\mit dem Namen .\pipe\iaslog.log, um die Daten zu akzeptieren. Wählen Sie im Dialogfeld Eigenschaften der lokalen Datei in neue Protokolldatei erstellen die Option nie (unbegrenzte Dateigröße) aus, wenn Sie Named Pipes verwenden.

- Das Protokoll Dateiverzeichnis kann mithilfe von System Umgebungsvariablen (anstelle von Benutzervariablen) erstellt werden, z. b. "% System Drive%", "% SystemRoot%" und "% windir%". Beispielsweise sucht der folgende Pfad unter Verwendung der Umgebungsvariablen "% windir%" die Protokolldatei im Verzeichnis "System" im Unterordner "\System32\Logs" (d. h. "%windir%\System32\Logs @ no__t-0".

- Das Wechseln von Protokolldatei Formaten führt nicht dazu, dass ein neues Protokoll erstellt wird. Wenn Sie die Protokolldatei Formate ändern, enthält die Datei, die zum Zeitpunkt der Änderung aktiv ist, eine Mischung der beiden Formate (Datensätze am Anfang des Protokolls haben das vorherige Format, und Datensätze am Ende des Protokolls haben das neue Format).

- Wenn die RADIUS-Kontoführung aufgrund eines vollständigen Festplatten Laufwerks oder anderer Ursachen ausfällt, hält NPS die Verarbeitung von Verbindungsanforderungen an und hindert Benutzer am Zugriff auf Netzwerkressourcen.

- NPS bietet die Möglichkeit, sich an eine Microsoft® SQL Server™ Datenbank zu protokollieren, zusätzlich zu oder nicht in einer lokalen Datei.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Domänen-Admins** erforderlich.


### <a name="to-configure-nps-log-file-properties"></a>So konfigurieren Sie die NPS-Protokolldatei Eigenschaften

1. Öffnen Sie die NPS-Konsole oder das NPS-MMC-Snap-in (Microsoft Management Console).
2. Klicken Sie in der Konsolen Struktur auf **Buchhaltung**.
3. Klicken Sie im Detailbereich unter **Protokolldatei Eigenschaften**auf **Protokolldatei Eigenschaften ändern**. Das Dialogfeld **Eigenschaften der Protokolldatei** wird geöffnet.
4. Stellen Sie sicher, dass Sie in den **Eigenschaften der Protokolldatei**auf der Registerkarte **Einstellungen** unter **folgende Informationen protokollieren**auswählen, dass Sie genügend Informationen protokollieren möchten, um Ihre Buchhaltungs Ziele zu erreichen. Wenn Ihre Protokolle z. b. Sitzungs Korrelation ausführen müssen, aktivieren Sie alle Kontrollkästchen.
5. Wählen Sie unter **Protokollierungs Fehler Aktion**aus, **ob die Protokollierung fehlschlägt, Verbindungsanforderungen verwerfen,** wenn die Verarbeitung von Zugriffs Anforderungs Nachrichten durch NPS beendet werden soll, wenn Protokolldateien vollständig oder nicht verfügbar sind. Wenn Sie möchten, dass der NPS die Verarbeitung von Verbindungsanforderungen fortsetzt, wenn die Protokollierung fehlschlägt, aktivieren Sie dieses Kontrollkästchen nicht.
6. Klicken Sie im Dialogfeld **Eigenschaften der Protokolldatei** auf die Registerkarte **Protokolldatei** .
7. Geben Sie auf der Registerkarte **Protokolldatei** unter **Verzeichnis**den Speicherort ein, an dem die NPS-Protokolldateien gespeichert werden sollen. Der Standard Speicherort ist der Ordner systemroot\System32\LogFiles.<br>Wenn Sie im **Protokoll Dateiverzeichnis**keine vollständige Pfad Anweisung angeben, wird der Standardpfad verwendet. Wenn Sie z. b. **NPSLogFile** in das **Protokoll Dateiverzeichnis**eingeben, befindet sich die Datei unter%systemroot%\System32\NPSLogFile.
8. Klicken Sie unter **Format**auf **DTS-kompatibel**. Wenn Sie möchten, können Sie stattdessen ein Legacy Dateiformat auswählen, z. b.  **\(ODBC-\) Legacy** oder IAS  **\(-Legacy.\)**<br>**ODBC** -und **IAS** -Legacy Dateitypen enthalten eine Teilmenge der Informationen, die von NPS an die SQL Server Datenbank gesendet werden. Das XML-Format des **DTS-kompatiblen** Dateityps ist mit dem XML-Format identisch, das NPS zum Importieren von Daten in die SQL Server Datenbank verwendet. Aus diesem Grund bietet das **DTS-kompatible** Dateiformat eine effizientere und umfassende Übertragung von Daten in die Standard-SQL Server-Datenbank für NPS.
9. Klicken Sie in **neue Protokolldatei erstellen**, um NPS so zu konfigurieren, dass in angegebenen Intervallen neue Protokolldateien gestartet werden. Klicken Sie dann auf das gewünschte Intervall:
    - Klicken Sie bei umfangreichen Transaktionsvolumen-und Protokollierungs Aktivitäten auf **täglich**.
    - Klicken Sie für kleinere Transaktions Volumes und Protokollierungs Aktivitäten auf **wöchentlich** oder **monatlich**.
    - Um alle Transaktionen in einer Protokolldatei zu speichern, klicken Sie auf  **\(nie\)unbegrenzte Dateigröße**.
    - Um die Größe der einzelnen Protokolldateien einzuschränken, klicken Sie auf **Wenn die Protokolldatei diese Größe erreicht**, und geben Sie dann eine Dateigröße ein, nach der ein neues Protokoll erstellt wird. Die Standardgröße ist 10 Megabyte (MB).
10. Wenn Sie möchten, dass der NPS alte Protokolldateien löscht, um Speicherplatz für neue Protokolldateien zu erstellen, wenn die Festplatte fast ausgelastet ist, stellen Sie sicher, dass beim vollständigen Löschen der Datenträger die Option **ältere Protokolldateien löschen** ausgewählt ist Diese Option ist jedoch nicht verfügbar, wenn der Wert von **neue Protokolldatei erstellen**  **\(niemals unbegrenzt\)** ist. Auch wenn die älteste Protokolldatei die aktuelle Protokolldatei ist, wird Sie nicht gelöscht.

## <a name="configure-nps-sql-server-logging"></a>Konfigurieren der NPS-SQL Server Protokollierung

Mit diesem Verfahren können Sie die RADIUS-Buchhaltungsdaten in einer lokalen oder Remote Datenbank protokollieren, die Microsoft SQL Server ausgeführt wird.

>[!NOTE]
>NPS formatiert Buchhaltungsdaten als XML-Dokument, das an die gespeicherte Prozedur **report_event** in der SQL Server Datenbank gesendet wird, die Sie in NPS festlegen. Damit SQL Server Protokollierung ordnungsgemäß funktioniert, müssen Sie über eine gespeicherte Prozedur mit dem Namen **report_event** in der SQL Server-Datenbank verfügen, die die XML-Dokumente von NPS empfangen und analysieren kann.

Um dieses Verfahren auszuführen, ist mindestens die Mitgliedschaft in "Domänen-Admins" oder eine entsprechende Berechtigung erforderlich.

### <a name="to-configure-sql-server-logging-in-nps"></a>So konfigurieren Sie SQL Server Protokollierung in NPS

1. Öffnen Sie die NPS-Konsole oder das NPS-MMC-Snap-in (Microsoft Management Console).
2. Klicken Sie in der Konsolen Struktur auf **Buchhaltung**.
3. Klicken Sie im Detailfenster in **SQL Server Protokollierungs Eigenschaften**auf **SQL Server Protokollierungs Eigenschaften ändern**. Das Dialogfeld **Eigenschaften für SQL Server Protokollierung** wird geöffnet.
4. Wählen Sie unter **folgende Informationen protokollieren**die Informationen aus, die Sie protokollieren möchten: 
    - Wenn Sie alle Buchhaltungs Anforderungen protokollieren möchten, klicken Sie auf **Buchhaltungs Anforderungen**.
    - Um Authentifizierungsanforderungen zu protokollieren, klicken Sie auf **Authentifizierungsanforderungen**.
    - Zum Protokollieren des regelmäßigen Buchhaltungs Status klicken Sie auf **regelmäßiger Buchhaltungs Status**.
    - Zum Protokollieren des regelmäßigen Status, z. b. von zwischenbuchhaltungs Anforderungen, klicken Sie auf **regelmäßig**
5. Um die Anzahl der gleichzeitigen Sitzungen zwischen dem Server, auf dem NPS ausgeführt wird, und dem SQL Server zu konfigurieren, geben Sie eine Zahl in **Maximale Anzahl gleichzeitiger Sitzungen**ein.
6. Klicken Sie zum Konfigurieren der SQL Server Datenquelle in **SQL Server Protokollierung**auf **Konfigurieren**. Das Dialogfeld **Daten Link Eigenschaften** wird geöffnet. Geben Sie auf der Registerkarte **Verbindung** Folgendes an: 
    - Um den Namen des Servers anzugeben, auf dem die Datenbank gespeichert ist, geben Sie einen Namen ein, oder wählen Sie einen Namen aus, **oder geben Sie einen Servernamen ein**.
    - Um die Authentifizierungsmethode anzugeben, mit der Sie sich beim Server anmelden möchten, klicken Sie auf **Windows NT Integrated Security verwenden**. Oder klicken Sie auf **bestimmten Benutzernamen und Kennwort verwenden**, und geben Sie dann Anmelde Informationen in **Benutzername** und **Kennwort**ein.
    - Um ein leeres Kennwort zuzulassen, klicken Sie auf **leeres Kennwort**.
    - Um das Kennwort zu speichern, klicken Sie auf **Kennwort speichern**.
    - Um anzugeben, mit welcher Datenbank auf dem SQL Server Computer eine Verbindung hergestellt werden soll, klicken Sie auf **Datenbank auf dem Server auswählen**, und wählen Sie dann einen Datenbanknamen aus der Liste aus.
7. Um die Verbindung zwischen NPS und SQL Server zu testen, klicken Sie auf **Verbindung testen**. Klicken Sie auf **OK** , um die **Daten Link Eigenschaften**zu schließen
8. Wählen Sie unter **Protokollierungs Fehler Aktion**die Option **Text Datei Protokollierung für Failover aktivieren aus** , wenn der NPS die Text Datei Protokollierung fortsetzen soll, wenn SQL Server Protokollierung fehlschlägt. 
9. Wählen Sie unter **Protokollierungs Fehler Aktion**aus, **ob die Protokollierung fehlschlägt, Verbindungsanforderungen verwerfen,** wenn die Verarbeitung von Zugriffs Anforderungs Nachrichten durch NPS beendet werden soll, wenn Protokolldateien vollständig oder nicht verfügbar sind. Wenn Sie möchten, dass der NPS die Verarbeitung von Verbindungsanforderungen fortsetzt, wenn die Protokollierung fehlschlägt, aktivieren Sie dieses Kontrollkästchen nicht.

## <a name="ping-user-name"></a>Ping-Benutzername

Einige RADIUS-Proxy Server und Netzwerk Zugriffs Server senden regelmäßig Authentifizierungs-und Buchhaltungs Anforderungen (als Ping-Anforderungen bezeichnet), um zu überprüfen, ob der NPS im Netzwerk vorhanden ist. Diese Ping-Anforderungen enthalten fiktive Benutzernamen. Wenn NPS diese Anforderungen verarbeitet, werden die Ereignis-und Buchhaltungs Protokolle mit Zugriffs Ablehnungs Datensätzen gefüllt, sodass es schwieriger ist, gültige Datensätze nachzuverfolgen.

Wenn Sie einen Registrierungs Eintrag für **Ping User-Name**konfigurieren, gleicht NPS den Registrierungs Eintrags Wert mit dem Wert des Benutzernamens in Ping-Anforderungen durch andere Server ab. Ein **Ping User-Name Registry-** Eintrag gibt den fiktiven Benutzernamen (oder ein Benutzernamens Muster mit Variablen, die mit dem fiktiven Benutzernamen übereinstimmen) an, die von RADIUS-Proxy Servern und Netzwerk Zugriffs Servern gesendet werden. Wenn NPS Ping-Anforderungen erhält, die mit dem Registrierungs Eintrags Wert **Ping User-Name** identisch sind, lehnt NPS die Authentifizierungsanforderungen ab, ohne die Anforderung zu verarbeiten. NPS zeichnet keine Transaktionen auf, die den fiktiven Benutzernamen in Protokolldateien einschließen, wodurch das Ereignisprotokoll leichter interpretiert werden kann.

**Ping User-Name** wird nicht standardmäßig installiert. Sie müssen **Ping User-Name** der Registrierung hinzufügen. Mithilfe des Registrierungs-Editors können Sie der Registrierung einen Eintrag hinzufügen.

>[!CAUTION]
>Durch eine fehlerhafte Bearbeitung der Registrierung können ernsthafte Systemschäden verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.

### <a name="to-add-ping-user-name-to-the-registry"></a>So fügen Sie Ping User-Name zur Registrierung hinzu

Ein Ping-Benutzername kann dem folgenden Registrierungsschlüssel als Zeichen folgen Wert von einem Mitglied der lokalen Administratoren Gruppe hinzugefügt werden:

`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\IAS\Parameters`

- **Name**:`ping user-name`
- **Typ**:`REG_SZ`
- **Daten**:  *Benutzername*

>[!TIP]
>Geben Sie ein Namensmuster (z. b. einen DNS-Namen, einschließlich Platzhalter Zeichen) in **Daten**ein, um mehr als einen Benutzernamen für einen **Ping-Benutzernamen** Wert anzugeben.
