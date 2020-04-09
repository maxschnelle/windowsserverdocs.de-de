---
title: Verstehen und Konfigurieren von Azure Monitor
description: Ausführliche Informationen zur Einrichtung der Azure Monitor und zum Konfigurieren von e-Mail-und SMS-Warnungen für den Cluster "direkte Speicherplätze" in Windows Server 2016 und 2019.
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/10/2020
ms.openlocfilehash: fa4d8793c07cabd39ee6cc0d54b5cddc84eac202
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859043"
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Verwenden Sie Azure Monitor, um e-Mails zu Integritätsdienst Fehlern zu senden.

>Gilt für: Windows Server 2019, Windows Server 2016

Azure Monitor maximiert die Verfügbarkeit und Leistung Ihrer Anwendungen durch die Bereitstellung einer umfassenden Lösung zum erfassen, analysieren und beeinflussen von Telemetriedaten aus ihren Cloud-und lokalen Umgebungen. Es hilft Ihnen, zu verstehen, wie Ihre Anwendungen funktionieren, und ermittelt proaktiv Probleme, die Sie betreffen, und die Ressourcen, von denen Sie abhängen.

Dies ist besonders hilfreich für Ihren lokalen hyperkonvergierten Cluster. Wenn Azure Monitor integriert ist, können Sie e-Mail, Text (SMS) und andere Warnungen konfigurieren, um Sie zu pingen, wenn ein Fehler in Ihrem Cluster vorliegt (oder wenn Sie andere Aktivitäten basierend auf den gesammelten Daten markieren möchten). Im folgenden wird kurz erläutert, wie Azure Monitor funktioniert, wie Sie Azure Monitor installieren und wie Sie diese konfigurieren, um Benachrichtigungen zu senden.

Wenn Sie System Center verwenden, sehen Sie sich die [direkte Speicherplätze Management Pack](https://www.microsoft.com/download/details.aspx?id=100782) an, die sowohl Windows Server 2019-als auch Windows Server 2016 direkte Speicherplätze-Cluster überwacht.

Diese Management Pack umfasst Folgendes:

* Integritäts-und Leistungsüberwachung für physische Datenträger
* Integritäts-und Leistungsüberwachung für Speicher Knoten
* Integritäts-und Leistungsüberwachung für den Speicher Pool
* Volumeresilienztyp und deduplizierungsstatus

## <a name="understanding-azure-monitor"></a>Grundlegendes zu Azure Monitor

Alle Daten, die von Azure Monitor gesammelt werden, sind in einen von zwei Grundtypen unterteilt: Metriken und Protokolle.

1. [Metriken](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#metrics) sind numerische Werte, die einen Aspekt eines Systems zu einem bestimmten Zeitpunkt beschreiben. Sie sind einfach und können Near Real-Time-Szenarien unterstützen. Auf der Übersichtsseite des Azure-Portal werden die von Azure Monitor gesammelten Daten angezeigt.

![Abbildung der Metriken im Metrik-Explorer](media/configure-azure-monitor/metrics.png)

2. [Protokolle](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs) enthalten unterschiedliche Arten von Daten, die in Datensätzen mit unterschiedlichen Eigenschaften Sätzen für jeden Typ angeordnet sind. Telemetriedaten wie Ereignisse und Ablauf Verfolgungen werden zusätzlich zu den Leistungsdaten als Protokolle gespeichert, sodass Sie alle zur Analyse kombiniert werden können. Die von Azure Monitor gesammelten Protokolldaten können mit [Abfragen](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) analysiert werden, um gesammelte Daten schnell abzurufen, zu konsolidieren und zu analysieren. Sie können Abfragen mithilfe von [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/portals) in der Azure-Portal erstellen und testen und anschließend entweder die Daten mithilfe dieser Tools direkt analysieren oder Abfragen für die Verwendung mit [Visualisierungen](https://docs.microsoft.com/azure/azure-monitor/visualizations) oder Warnungs [Regeln](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview)speichern.

![Abbildung der Protokolle, die in Log Analytics erfasst werden](media/configure-azure-monitor/logs.png)

Unten finden Sie weitere Details zum Konfigurieren dieser Warnungen.

## <a name="onboarding-your-cluster-using-windows-admin-center"></a>Integrieren Ihres Clusters mithilfe des Windows Admin Centers

Mithilfe des Windows Admin Centers können Sie Ihren Cluster in Azure Monitor integrieren.

![GIF des Onboarding-Clusters in Azure Monitor "](media/configure-azure-monitor/onboarding.gif)

Während dieses onboardingflows werden die folgenden Schritte im Hintergrund ausgeführt. Wir erläutern, wie Sie diese im Detail konfigurieren, wenn Sie Ihren Cluster manuell einrichten möchten. 

### <a name="configuring-health-service"></a>Konfigurieren von Integritätsdienst

Als erstes müssen Sie Ihren Cluster konfigurieren. Wie Sie vielleicht wissen, verbessert das [Integritätsdienst](../../failover-clustering/health-service-overview.md) die tägliche Überwachung und Betriebsabläufe für Cluster, die direkte Speicherplätze ausführen. 

Wie bereits erwähnt, sammelt Azure Monitor Protokolle von jedem Knoten, auf dem Sie in Ihrem Cluster ausgeführt wird. Daher müssen wir die Integritätsdienst so konfigurieren, dass Sie in einen Ereignis Kanal geschrieben wird. Dies geschieht wie folgt:

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

Zum Konfigurieren des Integritätsdienst führen Sie Folgendes aus:

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

Wenn Sie das obige Cmdlet ausführen, um die Integritäts Einstellungen festzulegen, bewirken Sie, dass die Ereignisse, die wir beginnen möchten, in den Ereignis Kanal *Microsoft-Windows-Health/Operational* geschrieben werden.

### <a name="configuring-log-analytics"></a>Konfigurieren von Log Analytics

Nachdem Sie nun die ordnungsgemäße Protokollierung für Ihren Cluster eingerichtet haben, besteht der nächste Schritt in der ordnungsgemäßen Konfiguration von Log Analytics.

Um einen Überblick zu erhalten, kann [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows) Daten direkt von ihren physischen oder virtuellen Windows-Computern in Ihrem Rechenzentrum oder einer anderen cloudumgebung in einem einzigen Repository sammeln, um eine ausführliche Analyse und Korrelation zu erzielen.

Informationen zur unterstützten Konfiguration finden Sie [unter Unterstützte Windows-Betriebssysteme](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und [Netzwerkfirewallkonfiguration](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

Wenn Sie über kein Azure-Abonnement verfügen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

#### <a name="login-in-to-azure-portal"></a>Anmelden beim Azure-Portal

Melden Sie sich bei der Azure-Portal unter [https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)an.

#### <a name="create-a-workspace"></a>Arbeitsbereich erstellen

Weitere Informationen zu den unten aufgeführten Schritten finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/learn/quick-collect-windows-computer).

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen **Log Analytics**ein. Wenn Sie mit der Eingabe beginnen, wird die Liste basierend auf Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**aus.<br><br> 

   ![Azure-Portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. Klicken Sie auf **Erstellen**, und wählen Sie dann die Optionen für die folgenden Elemente aus:

   * Geben Sie einen Namen für den neuen **Log Analytics Arbeitsbereich**ein, z. b. *defaultlaworkspace*. 
   * Wählen Sie ein **Abonnement** aus, zu dem Sie eine Verknüpfung herstellen möchten, indem Sie aus der Dropdown Liste auswählen, wenn die Standardoption ausgewählt ist.
   * Wählen Sie unter **Ressourcengruppe**eine vorhandene Ressourcengruppe aus, die einen oder mehrere virtuelle Azure-Computer enthält. <br><br>

      ![Blatt "Log Analytics Ressource erstellen"](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. Nachdem Sie die erforderlichen Informationen im **Arbeitsbereich Log Analytics** angegeben haben, klicken Sie auf **OK**.  

Während die Informationen überprüft werden und der Arbeitsbereich erstellt wird, können Sie den Fortschritt im Menü unter **Benachrichtigungen** nachverfolgen. 

#### <a name="obtain-workspace-id-and-key"></a>Arbeitsbereichs-ID und Schlüssel abrufen
Bevor Sie die Microsoft Monitoring Agent für Windows installieren, benötigen Sie die Arbeitsbereichs-ID und den Schlüssel für Ihren Log Analytics Arbeitsbereich.  Diese Informationen sind für den Setup-Assistenten erforderlich, um den Agent ordnungsgemäß zu konfigurieren und sicherzustellen, dass er erfolgreich mit log Analytics kommunizieren kann.  

1. Klicken Sie im Azure-Portal in der oberen linken Ecke auf **alle Dienste** . Geben Sie in der Liste der Ressourcen **Log Analytics**ein. Wenn Sie mit der Eingabe beginnen, wird die Liste basierend auf Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**aus.
2. Wählen Sie in der Liste der Log Analytics Arbeitsbereiche den zuvor erstellten *defaultlaworkspace* aus.
3. Wählen Sie **Erweiterte Einstellungen**aus.<br><br> ![Log Analytics Einstellungen](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. Wählen Sie **verbundene Quellen**aus, und wählen Sie dann **Windows-Server**aus.   
5. Der Wert rechts von Arbeitsbereichs- **ID** und **Primärschlüssel**. Speichern Sie beide temporär. Kopieren Sie Sie, und fügen Sie beide in Ihren bevorzugten Editor ein.   

### <a name="installing-the-agent-on-windows"></a>Installieren des Agents unter Windows
Mit den folgenden Schritten wird der Microsoft Monitoring Agent installiert und konfiguriert. **Stellen Sie sicher, dass Sie diesen Agent auf jedem Server im Cluster installieren, und geben Sie an, dass der Agent beim Windows-Systemstart ausgeführt werden soll.**

1. Wählen Sie auf der Seite **Windows-Server** die entsprechende Windows-Agent-Version **herunter** laden aus, die je nach Prozessorarchitektur des Windows-Betriebssystems heruntergeladen werden soll.
2. Führen Sie Setup aus, um den Agent auf dem Computer zu installieren.
2. Klicken Sie auf der **Willkommenseite** auf **Weiter**.
3. Lesen Sie auf der Seite **Lizenzbedingungen** die Lizenz, und klicken Sie dann auf **Ich stimme**zu.
4. Ändern oder behalten Sie auf der Seite **Zielordner** den Standard Installationsordner bei, und klicken Sie dann auf **weiter**.
5. Wählen Sie auf der Seite **Agent-Setup Optionen** aus, dass der Agent mit Azure verbunden werden soll Log Analytics und klicken Sie dann auf **weiter**.   
6. Führen Sie auf der Seite **Azure-Log Analytics** die folgenden Schritte aus:
   1. Fügen Sie die zuvor kopierte Arbeitsbereichs- **ID** und den **Arbeitsbereichs Schlüssel (Primärschlüssel)** ein.    
    a. Wenn der Computer über einen Proxy Server mit dem Log Analytics-Dienst kommunizieren muss, klicken Sie auf **erweitert** , und geben Sie die URL und die Portnummer des Proxy Servers an.  Wenn Ihr Proxy Server eine Authentifizierung erfordert, geben Sie den Benutzernamen und das Kennwort für die Authentifizierung beim Proxy Server ein, und klicken Sie dann auf **weiter**.  
7. Klicken Sie auf **weiter** , sobald Sie die Bereitstellung der erforderlichen Konfigurationseinstellungen abgeschlossen haben.<br><br> ![Arbeitsbereichs-ID und Primärschlüssel](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png) einfügen<br><br>
8. Überprüfen Sie Ihre Auswahl auf der Seite **bereit zum Installieren** , und klicken Sie dann auf **Installieren**.
9. Klicken Sie auf der Seite **Konfiguration wurde erfolgreich abgeschlossen** auf **Fertig**stellen.

Wenn der Vorgang beendet ist, wird der **Microsoft Monitoring Agent** in der **Systemsteuerung**angezeigt. Sie können die Konfiguration überprüfen und sicherstellen, dass der Agent mit log Analytics verbunden ist. Wenn eine Verbindung hergestellt ist, zeigt der Agent auf der Registerkarte **Azure Log Analytics** eine Meldung mit dem Hinweis an, dass **die Microsoft Monitoring Agent erfolgreich eine Verbindung mit dem Microsoft Log Analytics Dienst hergestellt hat.** 

![MMA-Verbindungsstatus zu Log Analytics](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

Informationen zur unterstützten Konfiguration finden Sie [unter Unterstützte Windows-Betriebssysteme](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und [Netzwerkfirewallkonfiguration](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

## <a name="setting-up-alerts-using-windows-admin-center"></a>Einrichten von Warnungen mithilfe des Windows Admin Centers

Im Windows Admin Center können Sie Standard Warnungen konfigurieren, die für alle Server im Log Analytics Arbeitsbereich gelten. 

![GIF der Einrichtung von Warnungen "](media/configure-azure-monitor/setup1.gif)

Dabei handelt es sich um die Warnungen und deren Standardbedingungen, für die Sie sich entscheiden können:

| Warnung                | Standard Bedingung                                  |
|---------------------------|----------------------------------------------------|
| CPU-Auslastung           | Über 85% 10 Minuten                            |
| Auslastung der Datenträger Kapazität | Über 85% 10 Minuten                            |
| Arbeitsspeicherauslastung        | Verfügbarer Arbeitsspeicher von weniger als 100 MB für 10 Minuten   |
| Takt                 | Weniger als 2 Beats für 5 Minuten                   |
| Kritischer System Fehler     | Alle kritischen Warnungen im Cluster System-Ereignisprotokoll |
| Integritäts Dienst Warnung      | Alle Integritäts Dienst Fehler im Cluster            |

Nachdem Sie die Warnungen im Windows Admin Center konfiguriert haben, können Sie die Warnungen in Ihrem Log Analytics-Arbeitsbereich in Azure sehen.

![GIF der Einrichtung von Warnungen "](media/configure-azure-monitor/setup2.gif)

Während dieses onboardingflows werden die folgenden Schritte im Hintergrund ausgeführt. Wir erläutern, wie Sie diese im Detail konfigurieren, wenn Sie Ihren Cluster manuell einrichten möchten. 

### <a name="collecting-event-and-performance-data"></a>Sammeln von Ereignis-und Leistungsdaten

Log Analytics können Ereignisse aus dem Windows-Ereignisprotokoll und Leistungsindikatoren sammeln, die Sie für längerfristige Analysen und Berichte angeben, und Maßnahmen ergreifen, wenn eine bestimmte Bedingung erkannt wird.  Führen Sie die folgenden Schritte aus, um die Erfassung von Ereignissen aus dem Windows-Ereignisprotokoll und einige gängige Leistungsindikatoren zu konfigurieren.  

1. Klicken Sie in der Azure-Portal auf **Weitere Dienste** , die sich in der unteren linken Ecke befinden. Geben Sie in der Liste der Ressourcen **Log Analytics**ein. Wenn Sie mit der Eingabe beginnen, wird die Liste basierend auf Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**aus.
2. Wählen Sie **Erweiterte Einstellungen**aus.<br><br> ![Log Analytics Einstellungen](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. Wählen Sie **Daten**aus, und wählen Sie dann **Windows-Ereignisprotokolle**aus.  
4. Fügen Sie hier den Integritätsdienst Ereignis Kanal hinzu, indem Sie den Namen unten eingeben, und klicken Sie auf das Pluszeichen **+** .  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. Überprüfen Sie in der Tabelle die Schweregrade **Fehler** und **Warnung**.   
6. Klicken Sie oben auf der Seite auf **Speichern** , um die Konfiguration zu speichern.
7. Wählen Sie **Windows-Leistungsindikatoren** aus, um die Erfassung von Leistungsindikatoren auf einem Windows-Computer zu aktivieren. 
8. Wenn Sie die Windows-Leistungsindikatoren zum ersten Mal für einen neuen Log Analytics Arbeitsbereich konfigurieren, haben Sie die Möglichkeit, schnell mehrere allgemeine Indikatoren zu erstellen. Sie werden mit einem Kontrollkästchen neben den einzelnen angezeigt.<br> ![standardmäßig ausgewählte Windows-Leistungsindikatoren](media/configure-azure-monitor/windows-perfcounters-default.png)<br> Klicken Sie auf **ausgewählte Leistungsindikatoren hinzufügen**.  Sie werden hinzugefügt und mit einem Abtast Intervall von zehn Sekunden eingestellt.  
9. Klicken Sie oben auf der Seite auf **Speichern** , um die Konfiguration zu speichern.

## <a name="creating-alerts-based-on-log-data"></a>Erstellen von Warnungen auf der Grundlage von Protokolldaten

Wenn Sie dies bisher vorgenommen haben, sollte Ihr Cluster Ihre Protokolle und Leistungsindikatoren an Log Analytics senden. Der nächste Schritt besteht im Erstellen von Warnungs Regeln, die in regelmäßigen Abständen automatisch Protokoll Suchvorgänge ausführen. Wenn die Ergebnisse der Protokoll Suche bestimmte Kriterien erfüllen, wird eine Warnung ausgelöst, die eine e-Mail oder eine Text Benachrichtigung sendet. Sehen wir uns dies weiter unten an.

### <a name="create-a-query"></a>Erstellen einer Abfrage

Öffnen Sie zunächst das Portal für die Protokoll Suche.   

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen **Monitor**ein. Wenn Sie mit der Eingabe beginnen, wird die Liste basierend auf Ihrer Eingabe gefiltert. Wählen Sie **Monitor**aus.
2. Wählen Sie im Navigationsmenü Monitor **Log Analytics** aus, und wählen Sie dann einen Arbeitsbereich aus.

Die schnellste Methode zum Abrufen einiger Daten, mit denen Sie arbeiten, ist eine einfache Abfrage, die alle Datensätze in der Tabelle zurückgibt. Geben Sie die folgenden Abfragen in das Suchfeld ein, und klicken Sie auf die Schaltfläche Suchen.  

```
Event
```

Die Daten werden in der Standard Listenansicht zurückgegeben, und Sie können sehen, wie viele Datensätze zurückgegeben wurden.

![Einfache Abfrage](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

Auf der linken Seite des Bildschirms befindet sich der Filterbereich, mit dem Sie der Abfrage Filter hinzufügen können, ohne Sie direkt zu ändern.  Für diesen Daten Satz Typen werden mehrere Daten Satz Eigenschaften angezeigt, und Sie können einen oder mehrere Eigenschaftswerte auswählen, um die Suchergebnisse einzugrenzen.

Aktivieren Sie das Kontrollkästchen neben **Fehler** unter **eventlevelname** , oder geben Sie Folgendes ein, um die Ergebnisse auf Fehlerereignisse zu beschränken.

```
Event | where (EventLevelName == "Error")
```

![Filter](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

Nachdem Sie die apprate-Abfragen für Ereignisse erstellt haben, die Sie interessieren, speichern Sie diese für den nächsten Schritt.

### <a name="create-alerts"></a>Erstellen von Warnungen
Sehen wir uns nun ein Beispiel für das Erstellen einer Warnung an.

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen **Log Analytics**ein. Wenn Sie mit der Eingabe beginnen, wird die Liste basierend auf Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics**aus.
2. Wählen Sie im linken Bereich **Warnungen** aus, und klicken Sie dann oben auf der Seite auf **neue Benachrichtigungs Regel** , um eine neue Warnung zu erstellen.<br><br> ![Erstellen einer neuen Warnungs Regel](media/configure-azure-monitor/alert-rule-02.png)<br>
3. Im ersten Schritt wählen Sie im Abschnitt **Warnung erstellen** den Log Analytics Arbeitsbereich als Ressource aus, da es sich hierbei um ein Protokoll basiertes Warnsignal handelt.  Filtern Sie die Ergebnisse, indem Sie in der Dropdown Liste das betreffende Abonnement auswählen, wenn Sie über mehr als ein **Abonnement** verfügen, das Log Analytics zuvor erstellte Arbeitsbereich enthält.  Filtern Sie den **Ressourcentyp** , indem Sie in der Dropdown Liste **Log Analytics** auswählen.  Wählen Sie schließlich die **Ressource** **defaultlaworkspace** aus, und klicken Sie dann auf **done**.<br><br> ![Task "Warnung erstellen, Schritt 1"](media/configure-azure-monitor/alert-rule-03.png)<br>
4. Klicken Sie im Abschnitt Warnungs **Kriterien**auf **Kriterien hinzufügen** , um die gespeicherte Abfrage auszuwählen, und geben Sie dann die Logik an, der die Warnungs Regel folgt.
5. Konfigurieren Sie die Warnung mit den folgenden Informationen:  
   a. Wählen Sie in der Dropdown Liste **basierend auf** die Option **metrikmessung**aus.  Bei einer metrikmessung wird für jedes Objekt in der Abfrage eine Warnung mit einem Wert erstellt, der den angegebenen Schwellenwert überschreitet.  
   b. Wählen Sie **Condition**für die Bedingung **größer als** aus, und geben Sie ein thershold an.  
   c. Legen Sie dann fest, wann die Warnung ausgelöst werden soll. Sie können z. b. **aufeinanderfolgende Sicherheitsverletzungen** auswählen und in der Dropdown Liste den Wert 3 auswählen. **Greater than**  
   d. Ändern Sie im Abschnitt Evaluation based on den **Zeitraum** für den Zeitraum in **30** Minuten und die **Häufigkeit** auf 5. Die Regel wird alle fünf Minuten ausgeführt und gibt Datensätze zurück, die innerhalb der letzten dreißig Minuten ab dem aktuellen Zeitpunkt erstellt wurden.  Wenn Sie den Zeitraum auf ein breiteres Fenster festlegen, wird das Potenzial der Daten Latenz berücksichtigt und sichergestellt, dass die Abfrage Daten zurückgibt, um einen falsch negativen Wert zu vermeiden, bei dem die Warnung nie ausgelöst wird.  
6. Klicken Sie auf **Fertig** , um die Warnungs Regel abzuschließen.<br><br> ![](media/configure-azure-monitor/alert-signal-logic-02.png) Warnsignal konfigurieren<br> 
7. Wechseln Sie nun in den zweiten Schritt, und geben Sie im Feld Name der **Benachrichtigungs Regel** einen Namen für die Warnung ein, z. b. **Warnung für alle Fehlerereignisse**.  Geben Sie eine **Beschreibung** mit den Besonderheiten der Warnung an, und wählen Sie **kritisch (Schweregrad 0)** als **Schweregrad** aus den bereitgestellten Optionen aus.
8. Um die Warnungs Regel bei der Erstellung sofort zu aktivieren, übernehmen Sie bei der Erstellung den Standardwert für **Regel aktivieren**.
9. Für den dritten und letzten Schritt geben Sie eine **Aktionsgruppe**an, mit der sichergestellt wird, dass jedes Mal, wenn eine Warnung ausgelöst wird, die gleichen Aktionen ausgeführt werden und für jede Regel verwendet werden kann, die Sie definieren. Konfigurieren Sie eine neue Aktionsgruppe mit den folgenden Informationen:  
   a. Wählen Sie **neue Aktionsgruppe** aus. der Bereich **Aktionsgruppe hinzufügen** wird angezeigt.  
   b. Geben Sie unter **Aktionsgruppen Name**einen Namen wie z. b. **Benachrichtigungs Benachrichtigung** und einen **kurzen Namen** wie z. b. **itops-n**an.  
   c. Überprüfen Sie, ob die Standardwerte für das **Abonnement** und die **Ressourcengruppe** korrekt sind. Wenn dies nicht der Fall ist, wählen Sie die richtige Option aus der Dropdown Liste aus.   
   d. Geben Sie im Abschnitt Aktionen einen Namen für die Aktion an, z. b. **e-Mail senden** , und wählen Sie unter **Aktionstyp** die Option **e-Mail/SMS/Push/Voice** in der Dropdown Liste aus. Der Bereich **e-Mail/SMS/Push/Voice-** Eigenschaften wird rechts geöffnet, um zusätzliche Informationen bereitzustellen.  
   e. Wählen Sie im Bereich **e-Mail/SMS/Push/Voice** die bevorzugte Einstellung aus, und richten Sie Sie ein. Beispiel: Aktivieren Sie **e-Mail** , und geben Sie eine gültige e-Mail-Adresse an, an die die Nachricht übertragen wird  
   f. Klicken Sie auf **OK**, um die Änderungen zu speichern.<br><br> 

    ![Neue Aktionsgruppe erstellen](media/configure-azure-monitor/action-group-properties-01.png)

10. Klicken Sie auf **OK** , um die Aktionsgruppe abzuschließen. 
11. Klicken Sie auf Warnungs **Regel erstellen** , um die Warnungs Regel abzuschließen. Die Ausführung wird sofort gestartet.<br><br> ![das Erstellen einer neuen Warnungs Regel](media/configure-azure-monitor/alert-rule-01.png)<br> 

### <a name="example-alert"></a>Beispiel Warnung

Als Referenz sehen Sie eine Beispiel Warnung in Azure.

![GIF of Alert in Azure](media/configure-azure-monitor/alert.gif)

Im folgenden finden Sie ein Beispiel für die e-Mail, die Sie Azure Monitor senden:

![Beispiel für eine Warn Benachrichtigung](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>Siehe auch

- [Übersicht über direkte Speicherplätze](storage-spaces-direct-overview.md)
- Ausführlichere Informationen finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-viewdata).
- Lesen Sie diesen Artikel, um eine Übersicht über das [Herstellen einer Verbindung mit anderen Azure-Hybrid Diensten](../../manage/windows-admin-center/azure/index.md)zu erhalten.
