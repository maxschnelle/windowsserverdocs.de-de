---
title: Verstehen und Konfigurieren von Azure Monitor
description: Ausführliche Informationen zur Einrichtung der Azure Monitor und zum Konfigurieren von e-Mail-und SMS-Warnungen für den Cluster "direkte Speicherplätze" in Windows Server 2016 und 2019.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/10/2020
ms.openlocfilehash: 72d08b3e4461eeea07e161de1073f5320830028c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953984"
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Verwenden von Azure Monitor zum Senden von E-Mails über Integritätsdienstfehler

>Gilt für: Windows Server 2019, Windows Server 2016

Azure Monitor maximiert die Verfügbarkeit und Leistung Ihrer Anwendungen durch die Bereitstellung einer umfassenden Lösung für das Sammeln, Analysieren und Reagieren auf Telemetriedaten aus Ihren cloudbasierten und lokalen Umgebungen. Diese Lösung hilft Ihnen, die Leistung Ihrer Anwendungen zu verstehen, und erkennt proaktiv Probleme, die sich auf sie auswirken, und Ressourcen, von denen sie abhängen.

Dies ist besonders hilfreich für Ihren lokalen hyperkonvergierten Cluster. Wenn Azure Monitor integriert ist, können Sie e-Mail, Text (SMS) und andere Warnungen konfigurieren, um Sie zu pingen, wenn ein Fehler in Ihrem Cluster vorliegt (oder wenn Sie andere Aktivitäten basierend auf den gesammelten Daten markieren möchten). Im folgenden wird kurz erläutert, wie Azure Monitor funktioniert, wie Sie Azure Monitor installieren und wie Sie diese konfigurieren, um Benachrichtigungen zu senden.

Wenn Sie System Center verwenden, sehen Sie sich die [direkte Speicherplätze Management Pack](https://www.microsoft.com/download/details.aspx?id=100782) an, die sowohl Windows Server 2019-als auch Windows Server 2016 direkte Speicherplätze-Cluster überwacht.

Diese Management Pack umfasst Folgendes:

* Integritäts-und Leistungsüberwachung für physische Datenträger
* Integritäts-und Leistungsüberwachung für Speicher Knoten
* Integritäts-und Leistungsüberwachung für den Speicher Pool
* Volumeresilienztyp und deduplizierungsstatus

## <a name="understanding-azure-monitor"></a>Grundlegendes zu Azure Monitor

Alle von Azure Monitor gesammelten Daten gehören einem von zwei Grundtypen an: Metriken und Protokollen.

1. [Metriken](/azure/azure-monitor/platform/data-collection#metrics) sind numerische Werte, die einen Aspekt eines Systems zu einem bestimmten Zeitpunkt beschreiben. Sie sind einfach strukturiert und in der Lage, Szenarien nahezu in Echtzeit zu unterstützen. Auf der Übersichtsseite des Azure-Portal werden die von Azure Monitor gesammelten Daten angezeigt.

![Abbildung der Erfassung von Metriken im Metrik-Explorer](media/configure-azure-monitor/metrics.png)

2. [Protokolle](/azure/azure-monitor/platform/data-collection#logs) enthalten verschiedene Arten von Daten, die in Datensätzen mit unterschiedlichen Eigenschaften für jeden Typ organisiert sind. Telemetriedaten wie etwa Ereignisse und Ablaufverfolgungen werden als Protokolle zusätzlich zu Leistungsdaten gespeichert, die alle zur Analyse kombiniert werden können. Die in Azure Monitor gesammelten Protokolldaten können mit [Abfragen](/azure/azure-monitor/log-query/log-query-overview) analysiert werden, die die gesammelten Daten schnell abrufen, konsolidieren und analysieren. Sie können Abfragen mit [Log Analytics](/azure/azure-monitor/log-query/portals) im Azure-Portal erstellen und testen und die Daten dann entweder mit diesen Tools direkt analysieren oder Abfragen zur Verwendung mit [Visualisierungen](/azure/azure-monitor/visualizations) oder [Warnungsregeln](/azure/azure-monitor/platform/alerts-overview) speichern.

![Abbildung der Erfassung von Protokollen in Log Analytics](media/configure-azure-monitor/logs.png)

Unten finden Sie weitere Details zum Konfigurieren dieser Warnungen.

## <a name="onboarding-your-cluster-using-windows-admin-center"></a>Integrieren Ihres Clusters mithilfe des Windows Admin Centers

Mithilfe des Windows Admin Centers können Sie Ihren Cluster in Azure Monitor integrieren.

![GIF des Onboarding-Clusters in Azure Monitor "](media/configure-azure-monitor/onboarding.gif)

Während dieses onboardingflows werden die folgenden Schritte im Hintergrund ausgeführt. Wir erläutern, wie Sie diese im Detail konfigurieren, wenn Sie Ihren Cluster manuell einrichten möchten.

### <a name="configuring-health-service"></a>Konfigurieren von Integritätsdienst

Als Erstes müssen Sie den Cluster konfigurieren. Wie Sie vielleicht wissen, optimiert der [Integritätsdienst](../../failover-clustering/health-service-overview.md) die tägliche Überwachung und den Betrieb von Clustern, auf denen Direkte Speicherplätze ausgeführt wird.

Wie bereits erwähnt, sammelt Azure Monitor Protokolle von jedem Knoten, der in Ihrem Cluster ausgeführt wird. Daher müssen wir den Integritätsdienst für das Schreiben in einen Ereigniskanal konfigurieren, der wie folgt lautet:

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

Zum Konfigurieren des Integritätsdiensts führen Sie Folgendes aus:

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

Wenn Sie das obige Cmdlet ausführen, um die Integritäts Einstellungen festzulegen, bewirken Sie, dass die Ereignisse, die wir beginnen möchten, in den Ereignis Kanal *Microsoft-Windows-Health/Operational* geschrieben werden.

### <a name="configuring-log-analytics"></a>Konfigurieren von Log Analytics

Nachdem Sie nun die ordnungsgemäße Protokollierung für Ihren Cluster eingerichtet haben, besteht der nächste Schritt in der ordnungsgemäßen Konfiguration von Log Analytics.

Um einen Überblick zu erhalten, kann [Azure Log Analytics](/azure/azure-monitor/platform/agent-windows) Daten direkt von ihren physischen oder virtuellen Windows-Computern in Ihrem Rechenzentrum oder einer anderen cloudumgebung in einem einzigen Repository sammeln, um eine ausführliche Analyse und Korrelation zu erzielen.

Informationen zur unterstützten Konfiguration finden Sie in den Abschnitten zu [unterstützten Windows-Betriebssystemen](/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und zur [Netzwerkfirewallkonfiguration](/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

#### <a name="login-in-to-azure-portal"></a>Anmelden beim Azure-Portal

Melden Sie sich unter [https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) beim Azure-Portal an.

#### <a name="create-a-workspace"></a>Erstellen eines Arbeitsbereichs

Weitere Informationen zu den unten aufgeführten Schritten finden Sie in der [Azure Monitor-Dokumentation](/azure/azure-monitor/learn/quick-collect-windows-computer).

1. Klicken Sie im Azure-Portal auf **Alle Dienste**. Geben Sie in der Liste mit den Ressourcen **Log Analytics** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**.<br><br>

   ![Azure-Portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. Klicken Sie auf **Erstellen**, und wählen Sie anschließend Optionen für die folgenden Elemente aus:

   * Geben Sie einen Namen für den neuen **Log Analytics-Arbeitsbereich** ein, etwa *DefaultLAWorkspace*.
   * Wählen Sie ein **Abonnement** aus, mit dem eine Verknüpfung erstellt werden soll, indem Sie in der Dropdownliste einen anderen Eintrag auswählen, falls der Standardeintrag nicht geeignet ist.
   * Wählen Sie für **Ressourcengruppe** eine vorhandene Ressourcengruppe aus, die einen oder mehrere virtuelle Azure-Computer enthält. <br><br>

      ![Erstellen des Log Analytics-Ressourcenblatts](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>

3. Klicken Sie nach dem Bereitstellen der erforderlichen Informationen im Bereich **Log Analytics-Arbeitsbereich** auf **OK**.

Die Informationen werden überprüft, und der Arbeitsbereich wird erstellt. Sie können den Fortschritt im Menü unter **Benachrichtigungen** nachverfolgen.

#### <a name="obtain-workspace-id-and-key"></a>Abrufen von Arbeitsbereichs-ID und -Schlüssel
Vor der Installation von Microsoft Monitoring Agent für Windows benötigen Sie die Arbeitsbereichs-ID und den Schlüssel für Ihren Log Analytics-Arbeitsbereich.  Diese Informationen sind für den Setup-Assistenten erforderlich, um den Agent ordnungsgemäß zu konfigurieren und sicherzustellen, dass er erfolgreich mit Log Analytics kommunizieren kann.

1. Klicken Sie links oben im Azure-Portal auf **Alle Dienste**. Geben Sie in der Liste mit den Ressourcen **Log Analytics** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**.
2. Wählen Sie in der Liste der Log Analytics-Arbeitsbereiche den zuvor erstellten *DefaultLAWorkspace*.
3. Wählen Sie **Erweiterte Einstellungen**.<br><br> ![Erweiterte Einstellungen für Log Analytics](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>
4. Wählen Sie **Verbundene Quellen** und dann **Windows Server** aus.
5. Der Wert rechts von **Arbeitsbereichs-ID** und **Primärschlüssel**. Speichern Sie beide temporär, indem Sie sie kopieren und in Ihren bevorzugten Editor einfügen.

### <a name="installing-the-agent-on-windows"></a>Installieren des Agents unter Windows
Mit den folgenden Schritten wird Microsoft Monitoring Agent installiert und konfiguriert. **Stellen Sie sicher, dass Sie diesen Agent auf jedem Server im Cluster installieren, und geben Sie an, dass der Agent beim Windows-Systemstart ausgeführt werden soll.**

1. Wählen Sie auf der Seite **Windows-Server** die entsprechende Version für **Windows-Agent herunterladen** aus, um in Abhängigkeit von der Prozessorarchitektur des Windows-Betriebssystems herunterzuladen.
2. Führen Sie Setup aus, um den Agent auf Ihrem Computer zu installieren.
2. Klicken Sie auf der Seite **Willkommen**auf **Weiter**.
3. Lesen Sie die Seite **Lizenzbedingungen** durch, und klicken Sie anschließend auf **Ich stimme zu**.
4. Auf der Seite **Zielordner** können Sie den Standardinstallationsordner entweder ändern oder beibehalten. Klicken Sie anschließend auf **Weiter**.
5. Wählen Sie auf der Seite **Agent-Setupoptionen** aus, dass der Agent mit Azure Log Analytics verbunden werden soll, und klicken Sie dann auf **Weiter**.
6. Führen Sie auf der Seite **Azure Log Analytics** die folgenden Schritte aus:
   1. Fügen Sie die **Arbeitsbereichs-ID** und den **Arbeitsbereichsschlüssel (Primärschlüssel)** ein, die Sie zuvor kopiert haben.
    a) Wenn der Computer über einen Proxyserver mit dem Log Analytics-Dienst kommunizieren muss, klicken Sie auf **Erweitert**, und stellen Sie die URL sowie die Portnummer des Proxyservers bereit.  Wenn der Proxyserver eine Authentifizierung erfordert, geben Sie den Benutzernamen und das Kennwort für die Authentifizierung mit dem Proxyserver ein, und klicken Sie dann auf **Weiter**.
7. Klicken Sie auf **Weiter**, nachdem Sie die Bereitstellung der erforderlichen Konfigurationseinstellungen abgeschlossen haben.<br><br> ![Arbeitsbereichs-ID und Primärschlüssel einfügen](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. Überprüfen Sie Ihre Auswahl auf der Seite **Bereit zum Installieren**, und klicken Sie dann auf **Installieren**.
9. Klicken Sie auf der Seite **Die Konfiguration wurde erfolgreich abgeschlossen** auf **Fertig stellen**.

Nach Abschluss wird der **Microsoft Monitoring Agent** in der **Systemsteuerung** angezeigt. Sie können Ihre Konfiguration überprüfen und sicherstellen, dass der Agent mit Log Analytics verbunden ist. Wenn verbunden, zeigt der Agent auf der Registerkarte **Azure Log Analytics** eine Meldung an: **Der Microsoft Monitoring Agent hat erfolgreich eine Verbindung mit dem Microsoft Log Analytics-Dienst hergestellt.**

![MMA-Verbindungsstatus mit Log Analytics](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

Informationen zur unterstützten Konfiguration finden Sie in den Abschnitten zu [unterstützten Windows-Betriebssystemen](/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und zur [Netzwerkfirewallkonfiguration](/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

## <a name="setting-up-alerts-using-windows-admin-center"></a>Einrichten von Warnungen mithilfe von Windows Admin Center

Im Windows Admin Center können Sie Standard Warnungen konfigurieren, die für alle Server im Log Analytics Arbeitsbereich gelten.

![GIF der Einrichtung von Warnungen "](media/configure-azure-monitor/setup1.gif)

Sie können die folgenden Warnungen mit den folgenden Standardbedingungen wählen:

| Name der Warnung                | Standardbedingung                                  |
|---------------------------|----------------------------------------------------|
| CPU-Auslastung           | 10 Minuten lang höher als 85 %                            |
| Datenträger-Kapazitätsauslastung | 10 Minuten lang höher als 85 %                            |
| Arbeitsspeichernutzung        | Verfügbarer Arbeitsspeicher 10 Minuten lang geringer als 100 MB   |
| Heartbeat                 | 5 Minuten lang weniger als 2 Takte                   |
| Schwerwiegender Systemfehler     | Jede kritische Warnung im Cluster-Systemereignisprotokoll |
| Dienstintegritätswarnung      | Jeder Integritätsdienstfehler im Cluster            |

Nachdem Sie die Warnungen im Windows Admin Center konfiguriert haben, können Sie die Warnungen in Ihrem Log Analytics-Arbeitsbereich in Azure sehen.

![GIF der Einrichtung von Warnungen "](media/configure-azure-monitor/setup2.gif)

Während dieses onboardingflows werden die folgenden Schritte im Hintergrund ausgeführt. Wir erläutern, wie Sie diese im Detail konfigurieren, wenn Sie Ihren Cluster manuell einrichten möchten.

### <a name="collecting-event-and-performance-data"></a>Sammeln von Ereignis- und Leistungsdaten

Log Analytics kann Ereignisdaten aus den Windows-Ereignisprotokollen und Leistungsindikatoren sammeln, die Sie für längerfristige Analysen und Berichte angeben, und Maßnahmen einleiten, wenn eine bestimmte Bedingung erkannt wird.  Führen Sie diese Schritte aus, um die Sammlung von Ereignissen aus dem Ereignisprotokoll von Windows sowie mehreren allgemeinen Leistungsindikatoren zu konfigurieren.

1. Klicken Sie im Azure-Portal unten links auf **Weitere Dienste**. Geben Sie in der Liste mit den Ressourcen **Log Analytics** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**.
2. Wählen Sie **Erweiterte Einstellungen**.<br><br> ![Erweiterte Einstellungen für Log Analytics](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>
3. Wählen Sie **Daten** und dann **Windows-Ereignisprotokolle**.
4. Fügen Sie hier den Integritätsdienst-Ereigniskanal hinzu, indem Sie unten den Namen eingeben und auf das Pluszeichen **+** klicken.
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. Aktivieren Sie in der Tabelle die Schweregrade **Fehler** und **Warnung**.
6. Klicken Sie ganz oben auf der Seite auf **Speichern**, um die Konfiguration zu speichern.
7. Wählen Sie **Windows-Leistungsindikatoren** aus, um die Sammlung von Leistungsindikatoren auf einem Windows-Computer zu aktivieren.
8. Wenn Sie die Windows-Leistungsindikatoren zum ersten Mal für einen neuen Log Analytics-Arbeitsbereich konfigurieren, haben Sie die Möglichkeit, schnell mehrere allgemeine Indikatoren zu erstellen. Diese werden in einer Liste aufgeführt, und neben jedem Indikator finden Sie ein Kontrollkästchen.<br> ![Standardmäßige Windows-Leistungsindikatoren ausgewählt](media/configure-azure-monitor/windows-perfcounters-default.png)<br> Klicken Sie auf **Ausgewählte Leistungsindikatoren hinzufügen**.  Sie werden hinzugefügt und mit einem Stichprobenintervall von zehn Sekunden voreingestellt.
9. Klicken Sie ganz oben auf der Seite auf **Speichern**, um die Konfiguration zu speichern.

## <a name="creating-alerts-based-on-log-data"></a>Erstellen von Warnungen auf der Grundlage von Protokolldaten

Wenn Sie die oben beschriebenen Schritte durchgeführt haben, sollte der Cluster die Protokolle und Leistungsindikatoren an Log Analytics senden. Im nächsten Schritt werden Warnungsregeln erstellt, für die in regelmäßigen Abständen automatisch Protokollsuchen durchgeführt werden. Wenn die Ergebnisse der Protokollsuche bestimmte Kriterien erfüllen, wird eine Warnung ausgelöst, durch die eine Benachrichtigung per E-Mail oder SMS gesendet wird. Sehen wir uns dies in den folgenden Abschnitten an.

### <a name="create-a-query"></a>Erstellen einer Abfrage

Öffnen Sie zunächst das Portal für die Protokollsuche.

1. Klicken Sie im Azure-Portal auf **Alle Dienste**. Geben Sie in der Liste mit den Ressourcen **Monitor** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Monitor** aus.
2. Wählen Sie Log Analytics im Navigationsmenü **Monitor** und dann einen Arbeitsbereich aus.

Die schnellste Methode, Daten für die weitere Verwendung abzurufen, besteht in einer einfachen Abfrage, die alle Datensätze aus der Tabelle zurückgibt. Geben Sie die folgenden Abfragen im Suchfeld ein, und klicken Sie auf die Schaltfläche „Suchen“.

```
Event
```

Die Daten werden in der Standardlistenansicht zurückgegeben. Sie können ablesen, wie viele Datensätze insgesamt zurückgegeben wurden.

![Einfache Abfrage](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

Auf der linken Seite des Bildschirms befindet sich der Filterbereich, über den Sie Filter zu Abfragen hinzufügen können, ohne die Abfrage direkt zu verändern.  Mehrere Datensatzeigenschaften werden für diesen Datensatztyp angezeigt, und Sie können einen oder mehrere Eigenschaftenwerte auswählen, um Ihre Suchergebnisse einzugrenzen.

Aktivieren Sie das Kontrollkästchen neben **Fehler** unter **EVENTLEVELNAME**, oder geben Sie Folgendes ein, um die Ergebnisse auf Fehlerereignisse zu beschränken.

```
Event | where (EventLevelName == "Error")
```

![Filtern](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

Nachdem Sie die apprate-Abfragen für Ereignisse erstellt haben, die Sie interessieren, speichern Sie diese für den nächsten Schritt.

### <a name="create-alerts"></a>Erstellen von Warnungen
Sehen wir uns nun ein Beispiel für das Erstellen einer Warnung an.

1. Klicken Sie im Azure-Portal auf **Alle Dienste**. Geben Sie in der Liste mit den Ressourcen **Log Analytics** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**.
2. Klicken Sie im linken Bereich auf **Warnungen** und dann oben auf der Seite auf **Neue Warnungsregel**, um eine neue Warnung zu erstellen.<br><br> ![Erstellen einer neuen Warnungsregel](media/configure-azure-monitor/alert-rule-02.png)<br>
3. Im ersten Schritt wählen Sie im Abschnitt **Warnung erstellen** Ihren Log Analytics-Arbeitsbereich als Ressource aus, da es sich dabei um ein protokollbasiertes Warnungssignal handelt.  Wenn Sie mehrere Abonnements besitzen, filtern Sie die Ergebnisse, indem Sie in der Dropdownliste das gewünschte **Abonnement** auswählen, das den zuvor erstellten Log Analytics-Arbeitsbereich enthält.  Filtern Sie den **Ressourcentyp**, indem Sie in der Dropdownliste **Log Analytics** auswählen.  Wählen Sie abschließend die **Ressource** mit dem Namen **DefaultLAWorkspace** aus, und klicken Sie dann auf **Fertig**.<br><br> ![Schritt 1: Erstellen einer Warnung](media/configure-azure-monitor/alert-rule-03.png)<br>
4. Klicken Sie im Abschnitt **Warnungskriterien** auf **Kriterien hinzufügen**, um die gespeicherte Abfrage auszuwählen, und geben Sie dann eine Logik für die Warnungsregel an.
5. Konfigurieren Sie die Warnung mit den folgenden Informationen: a. Wählen Sie in der Dropdownliste **Basierend auf** die Option **Metrische Maßeinheit** aus.  Mit „Metrische Maßeinheit“ wird eine Warnung für jedes Objekt in der Abfrage mit einem Wert erzeugt, der den angegebenen Schwellenwert überschreitet.
   b) Wählen Sie **Condition**für die Bedingung **größer als** aus, und geben Sie ein thershold an.
   c. Legen Sie dann fest, wann die Warnung ausgelöst werden soll. Sie können beispielsweise **Aufeinanderfolgende Sicherheitsverletzungen** und in der Dropdownliste **Größer als** den Wert 3 auswählen.
   d. Ändern Sie unter „Evaluation based on“ (Auswertung basierend auf) den Wert für **Zeitraum** in **30** Minuten und den Wert für **Häufigkeit** in 5. Die Regel wird alle fünf Minuten ausgeführt und gibt Datensätze zurück, die innerhalb der letzten 30 Minuten erstellt wurden.  Durch die Verwendung eines weiter gefassten Zeitfensters wird potenziellen Datenlatenzen Rechnung getragen und sichergestellt, dass die Abfrage Daten zurückgibt, um ein falsch negatives Ergebnis zu vermeiden, bei dem die Warnung nie ausgelöst wird.
6. Klicken Sie auf **Fertig**, um die Warnungsregel fertig zu stellen.<br><br> ![Konfigurieren eines Warnungssignals](media/configure-azure-monitor/alert-signal-logic-02.png)<br>
7. Geben Sie nun im zweiten Schritt im Feld **Name der Warnungsregel** einen Namen für die Warnung ein, etwa **Warnung bei allen Fehlerereignissen**.  Geben Sie eine **Beschreibung** mit Details zu Ihrer Warnung ein, und wählen Sie für **Schweregrad** aus den angegebenen Optionen **Kritisch (Schweregrad 0)** aus.
8. Um die Warnungsregel direkt bei der Erstellung zu aktivieren, übernehmen Sie den Standardwert für **Regel beim Erstellen aktivieren**.
9. Im dritten und letzten Schritt geben Sie eine **Aktionsgruppe** an. Dadurch wird sichergestellt, dass bei jeder Warnungsauslösung die gleichen Aktionen ausgeführt werden und diese für jede definierte Regel verwendet werden können. Konfigurieren Sie eine neue Aktionsgruppe mit den folgenden Informationen: a. Klicken Sie auf **Neue Aktionsgruppe**, und der Bereich **Aktionsgruppe hinzufügen** wird angezeigt.
   b. Geben Sie unter **Name der Aktionsgruppe** einen Namen wie **IT-Vorgänge – Benachrichtigen** und einen **Kurznamen** wie **itops-n** ein.
   c. Überprüfen Sie, ob die Standardwerte für **Abonnement** und **Ressourcengruppe** richtig sind. Ist dies nicht der Fall, wählen Sie die korrekten Werte in der Dropdownliste aus.
   d. Geben Sie im Bereich „Aktionen“ einen Namen für die Aktion ein, beispielsweise **E-Mail senden**, und wählen Sie unter **Aktionstyp** in der Dropdownliste **E-Mail/SMS/Push/Sprachanruf** aus. Der Eigenschaftenbereich **E-Mail/SMS/Push/Sprachanruf** wird mit weiteren Informationen auf der rechten Seite geöffnet.
   e. Wählen Sie im Bereich **E-Mail/SMS/Push/Sprachanruf** die bevorzugte Einstellung aus, und richten Sie sie ein. Aktivieren Sie beispielsweise **E-Mail**, und geben Sie eine gültige SMTP-E-Mail-Adresse ein, an die die Nachricht gesendet werden soll.
   f. Klicken Sie auf **OK** , um die Änderungen zu speichern.<br><br>

    ![Erstellen der neuen Aktionsgruppe](media/configure-azure-monitor/action-group-properties-01.png)

10. Klicken Sie auf **OK**, um die Aktionsgruppe zu erstellen.
11. Klicken Sie auf **Warnungsregel erstellen**, um die Warnungsregel fertig zu stellen. Die Ausführung beginnt sofort.<br><br> ![Abschließen der Erstellung der neuen Warnungsregel](media/configure-azure-monitor/alert-rule-01.png)<br>

### <a name="example-alert"></a>Beispiel für Warnung

Hier ist ein Beispiel für eine Warnung in Azure dargestellt.

![GIF of Alert in Azure](media/configure-azure-monitor/alert.gif)

Im folgenden finden Sie ein Beispiel für die e-Mail, die Sie Azure Monitor senden:

![Beispiel für eine Warn Benachrichtigung](media/configure-azure-monitor/warning.png)

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- Ausführlichere Informationen finden Sie in der [Azure Monitor-Dokumentation](/azure/azure-monitor/learn/tutorial-viewdata).
- Lesen Sie diesen Artikel, um eine Übersicht über das [Herstellen einer Verbindung mit anderen Azure-Hybrid Diensten](../../manage/windows-admin-center/azure/index.md)zu erhalten.
