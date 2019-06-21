---
title: Verstehen und Konfigurieren von Azure Monitor
description: Ausführliche Setupinformationen für Neuigkeiten von Azure Monitor und Konfigurieren von e-Mail und Sms-Warnungen für den direkten Speicher Speicherplätze-Cluster in Windows Server 2016 und 2019.
keywords: "\"Direkte Speicherplätze\", Azure Monitor, Benachrichtigungen, e-Mail, sms"
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 6b229696e796f176fe89ab250ab48f1d9f0d5666
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280205"
---
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Verwenden von Azure Monitor zum Senden von e-Mails für Health-Dienstfehler

>Gilt für: Windows Server 2019, Windows Server 2016

Azure Monitor maximiert die Verfügbarkeit und Leistung Ihrer Anwendungen durch die Bereitstellung einer umfassenden Lösung für das Sammeln, analysieren und, die auf Telemetriedaten von Ihren cloudbasierten und lokalen Umgebungen. Es hilft Ihnen zu verstehen, wie Ihre Anwendungen ausführen und proaktiv identifiziert Probleme, die Auswirkungen auf diese und die Ressourcen, von denen sie abhängen.

Dies ist besonders hilfreich für Ihren lokalen hyperkonvergenten Cluster. Mit Azure Monitor integriert werden Sie zum Konfigurieren von e-Mail, Textnachricht (SMS) und andere Warnungen, um Sie zu pingen, wenn etwas stimmt nicht mit Ihrem Cluster (oder wenn Sie eine andere Aktivität, die auf Grundlage der gesammelten Daten zu kennzeichnen möchten). Im folgenden wird kurz erläutert die Funktionsweise von Azure Monitor, Vorgehensweise: Installieren von Azure Monitor und wie es zum Senden von Benachrichtigungen konfiguriert.


## <a name="understanding-azure-monitor"></a>Grundlegendes zu Azure Monitor

Alle von Azure Monitor gesammelte Daten in einer von zwei grundlegende Typen entspricht: Metriken und Protokolle.

1. [Metriken](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#metrics) sind numerische Werte, die einen Aspekt eines Systems zu einem bestimmten Zeitpunkt in der Zeit zu beschreiben. Sie sind einfach und nahezu in Echtzeit Szenarien unterstützen. Sie sehen, dass Daten, die von Azure Monitor-direkt in ihre Seite "Übersicht" im Azure-Portal gesammelt.

![Abbildung der Metriken im Metrik-Explorer zu erfassen](media/configure-azure-monitor/metrics.png)

2. [Protokolle](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs) enthalten verschiedene Arten von Daten in Form von Datensätzen mit verschiedenen Sätzen von Eigenschaften für jeden Typ organisiert sind. Telemetriedaten wie Anzahl der Ereignisse und ablaufverfolgungen werden gespeichert wie Protokolle darüber hinaus in Leistungsdaten, damit sie alle für die Analyse kombiniert werden kann. Von Azure Monitor gesammelten Daten analysiert werden können, mit [Abfragen](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) schnell abrufen, konsolidieren und Analysieren der gesammelten Daten. Sie können das Erstellen und Testen von Abfragen mit [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/portals) in das Azure-Portal aus, und klicken Sie dann entweder direkt Analysieren der Daten, die mithilfe dieser Tools oder Speichern von Abfragen für die Verwendung mit [Visualisierungen](https://docs.microsoft.com/azure/azure-monitor/visualizations) oder [Warnung Regeln](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview).

![Bild von Protokollen in Log Analytics erfassen](media/configure-azure-monitor/logs.png)

Weitere Informationen unten haben wir auf diese Warnungen konfigurieren.

## <a name="configuring-health-service"></a>Konfigurieren der Health-Dienst

Als erstes, die Sie tun müssen ist, Ihren Cluster zu konfigurieren. Wie Sie wissen vielleicht, die [Integritätsdienst](../../failover-clustering/health-service-overview.md) verbessert die tägliche Überwachung und Erfahrungen für Cluster "direkte Speicherplätze". 

Wie wir oben gesehen haben, sammelt Azure Monitor Protokolle aus den einzelnen Knoten, die sie in Ihrem Cluster ausgeführt wird. Wir haben also, so konfigurieren Sie den Health-Dienst an einen ereigniskanal zu schreiben, die werden:

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

Um den Health-Dienst zu konfigurieren, führen Sie folgende Aktionen ausführen:

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

Wenn Sie das Cmdlet aus, um die Einstellungen für die Geräteintegrität festgelegt ausführen, Sie dazu führen, dass die Ereignisse, um zu beginnen geschrieben werden soll, die *Microsoft-Windows-Integrität/Operational* Ereignis-Kanal.

## <a name="configuring-log-analytics"></a>Konfigurieren von Log Analytics

Nun, da Sie die richtigen Protokollierung in Ihrem Cluster eingerichtet haben, besteht der nächste Schritt, um ordnungsgemäß zu Log Analytics konfigurieren.

Erteilen Sie eine Übersicht über [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows) kann Daten direkt von Ihrem physischen oder virtuellen Windows-Computern in Ihrem Rechenzentrum oder anderen Cloud-Umgebung in einem einzelnen Repository zur detaillierten Analyse und Korrelation sammeln.

Um die unterstützte Konfiguration zu verstehen, lesen Sie [unterstützte Windows-Betriebssysteme](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und [netzwerkfirewallkonfiguration](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

Wenn Sie nicht über ein Azure-Abonnement verfügen, erstellen eine [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) bevor Sie beginnen.

### <a name="login-in-to-azure-portal"></a>Zur Anmeldung beim Azure-Portal

Melden Sie sich beim Azure-Portal an [ https://portal.azure.com ](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

### <a name="create-a-workspace"></a>Erstellen eines Arbeitsbereichs

Weitere Informationen zu den unten aufgeführten Schritten finden Sie unter den [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/learn/quick-collect-windows-computer).

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen, **Log Analytics**. Wenn Sie mit der Eingabe beginnen, die Listenfilter entsprechend den Eingaben. Wählen Sie **Protokollanalysen**.<br><br> 

   ![Azure-Portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. Klicken Sie auf **erstellen**, und wählen Sie anschließend Optionen für die folgenden Elemente:

   * Geben Sie einen Namen für die neue **Log Analytics-Arbeitsbereich**, z. B. *DefaultLAWorkspace*. 
   * Wählen Sie eine **Abonnement** zu verknüpfen, dazu, der aus der Dropdown-Liste angezeigt werden soll, falls der Standardeintrag nicht geeignet ist.
   * Für **Ressourcengruppe**, wählen Sie eine vorhandene Ressourcengruppe aus, die einem oder mehreren virtuellen Azure-Computern enthält. <br><br>

      ![Erstellen von Log Analytics-Blatt "Ressourcen"](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. Nach dem Bereitstellen der erforderlichen Informationen auf der **Log Analytics-Arbeitsbereich** Bereich, klicken Sie auf **OK**.  

Obwohl die Informationen überprüft werden und der Arbeitsbereich wird erstellt, Sie können den Status unter Nachverfolgen **Benachrichtigungen** aus dem Menü. 

### <a name="obtain-workspace-id-and-key"></a>Abrufen von Arbeitsbereichs-ID und Schlüssel
Vor der Installation der Microsoft Monitoring Agent für Windows, Sie benötigen die Arbeitsbereichs-ID und Schlüssel für Ihren Log Analytics-Arbeitsbereich.  Diese Informationen sind erforderlich, durch den Setup-Assistenten ordnungsgemäß konfigurieren Sie den Agent, und stellen Sie sicher, dass er erfolgreich mit Log Analytics kommunizieren kann.  

1. Klicken Sie im Azure-Portal auf **alle Dienste** finden Sie in der oberen linken Ecke. Geben Sie in der Liste der Ressourcen, **Log Analytics**. Wenn Sie mit der Eingabe beginnen, die Listenfilter entsprechend den Eingaben. Wählen Sie **Protokollanalysen**.
2. Wählen Sie in der Liste mit den Log Analytics-Arbeitsbereiche, *DefaultLAWorkspace* zuvor erstellt haben.
3. Wählen Sie **Erweiterte Einstellungen**.<br><br> ![Erweiterte Einstellungen für die Protokollanalyse](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. Wählen Sie **verbundene Quellen**, und wählen Sie dann **Windows-Servern**.   
5. Der Wert rechts vom **Arbeitsbereichs-ID** und **Primärschlüssel**. Beide vorübergehend zu speichern – kopieren Sie beide Zertifikate in Ihrem bevorzugten Editor zurzeit.   

## <a name="installing-the-agent-on-windows"></a>Installation des Agents unter Windows
Die folgenden Schritte installieren und konfigurieren den Microsoft Monitoring Agent. **Achten Sie darauf, um diesen Agent auf jedem Server in Ihrem Cluster installieren und um anzugeben, dass den Agent beim Start von Windows ausgeführt werden sollen.**

1. Auf der **Windows-Servern** Seite, wählen Sie das entsprechende **Windows-Agent herunterladen** Version, abhängig von der Prozessorarchitektur des Windows-Betriebssystems herunterzuladen.
2. Führen Sie Setup aus, um den Agent auf Ihrem Computer zu installieren.
2. Klicken Sie auf der **Willkommenseite** auf **Weiter**.
3. Auf der **Lizenzbedingungen** Seite, lesen Sie die Lizenzbedingungen, und klicken Sie dann auf **ich stimme zu**.
4. Auf der **Zielordner** Seite werden soll, ändern oder behalten Sie den standardmäßigen Installationsordner, und klicken Sie dann auf **Weiter**.
5. Auf der **Agent-Setupoptionen** Seite, und wählen Sie den Agent mit Azure Log Analytics verbinden, und klicken Sie auf **Weiter**.   
6. Auf der **Azure Log Analytics** führen die folgenden:
   1. Fügen Sie der **Arbeitsbereichs-ID** und **Arbeitsbereichsschlüssel (Primärschlüssel)** , die Sie zuvor kopiert haben.    
    a. Wenn der Computer für die Kommunikation über einen Proxyserver mit Log Analytics-Dienst muss, klicken Sie auf **erweitert** und geben Sie die URL und Portnummer des Proxyservers.  Wenn Ihr Proxyserver eine Authentifizierung erfordert, geben Sie Benutzername und Kennwort mit dem Proxyserver authentifizieren, und klicken Sie auf **Weiter**.  
7. Klicken Sie auf **Weiter** , nachdem Sie die Bereitstellung der erforderlichen Konfigurationseinstellungen abgeschlossen haben.<br><br> ![Fügen Sie die Arbeitsbereichs-ID und Primärschlüssel](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. Auf der **Installationsbereit** Seite, überprüfen Sie Ihre Auswahl, und klicken Sie dann auf **installieren**.
9. Auf der **Konfiguration wurde erfolgreich abgeschlossen** auf **Fertig stellen**.

Nach Abschluss des Vorgangs die **Microsoft Monitoring Agent** wird im **Systemsteuerung**. Sie können Ihre Konfiguration überprüfen und sicherzustellen, dass der Agent mit Log Analytics verbunden ist. Wenn verbunden, auf die **Azure Log Analytics** Registerkarte der Agent Meldung angezeigt: **Der Microsoft Monitoring Agent wurde erfolgreich mit Microsoft Log Analytics-Dienst verbunden.** 

![MMA-Verbindungsstatus mit Log Analytics](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

Um die unterstützte Konfiguration zu verstehen, lesen Sie [unterstützte Windows-Betriebssysteme](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) und [netzwerkfirewallkonfiguration](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements).

## <a name="collecting-event-and-performance-data"></a>Sammeln von Ereignis-und Leistungsdaten

Log Analytics können Ereignisse erfassen, aus dem Windows-Ereignisprotokoll und Leistungsindikatoren, die Sie für längerfristige Analysen und Berichte angeben, und Maßnahmen ergreifen, wenn eine bestimmte Bedingung erkannt wird.  Um die Sammlung von Ereignissen aus dem Windows-Ereignisprotokoll sowie mehreren allgemeinen Leistungsindikatoren zu konfigurieren, gehen Sie wie folgt vor.  

1. Klicken Sie im Azure-Portal auf **Weitere Dienste** finden Sie auf der linken unteren Ecke. Geben Sie in der Liste der Ressourcen, **Log Analytics**. Wenn Sie mit der Eingabe beginnen, die Listenfilter entsprechend den Eingaben. Wählen Sie **Protokollanalysen**.
2. Wählen Sie **Erweiterte Einstellungen**.<br><br> ![Erweiterte Einstellungen für die Protokollanalyse](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. Wählen Sie **Daten**, und wählen Sie dann **Windows-Ereignisprotokolle**.  
4. Hier, der Integritätsdienst-Ereignis-Kanal hinzufügen, geben Sie in den folgenden Namen und dann auf das Pluszeichen **+** .  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. Überprüfen Sie in der Tabelle die Schweregrade **Fehler** und **Warnung**.   
6. Klicken Sie auf **speichern** am oberen Rand der Seite, um die Konfiguration zu speichern.
7. Wählen Sie **Windows-Leistungsindikatoren** zum Aktivieren der Erfassung von Leistungsindikatoren auf einem Windows-Computer. 
8. Wenn Sie Windows-Leistungsindikatoren für einen neuen Log Analytics-Arbeitsbereich zum ersten Mal konfigurieren, erhalten Sie die Möglichkeit, schnell mehrere allgemeine Indikatoren zu erstellen. Sie werden mit einem Kontrollkästchen neben jeder aufgelistet.<br> ![Standard-Windows-Leistungsindikatoren ausgewählt](media/configure-azure-monitor/windows-perfcounters-default.png)<br> Klicken Sie auf **ausgewählte Leistungsindikatoren hinzufügen**.  Sie werden hinzugefügt und mit einem Stichprobenintervall von zehn Sekunden voreingestellt.  
9. Klicken Sie auf **speichern** am oberen Rand der Seite, um die Konfiguration zu speichern.

## <a name="creating-alerts-based-on-log-data"></a>Erstellen von Warnungen basierend auf Protokolldaten

Wenn Sie es geschafft haben jetzt Ihren Cluster sollte werden Ihre Protokolle und Leistungsindikatoren an Log Analytics senden. Der nächste Schritt ist die Erstellung von Warnungsregeln, die in regelmäßigen Abständen automatisch protokollsuchen durchgeführt werden. Wenn die Ergebnisse der protokollsuche bestimmte Kriterien erfüllen, wird dann eine Warnung ausgelöst, die Ihnen eine e-Mail oder SMS-Benachrichtigung sendet. Betrachten Sie diese unten.

### <a name="create-a-query"></a>Erstellen Sie eine Abfrage

Starten Sie durch Öffnen des Portals der Protokollsuche.   

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen, **Monitor**. Wenn Sie mit der Eingabe beginnen, die Listenfilter entsprechend den Eingaben. Wählen Sie **Monitor**.
2. Wählen Sie im Navigationsmenü Monitor **Log Analytics** und wählen Sie dann einen Arbeitsbereich.

Die schnellste Möglichkeit zum Abrufen von Daten zum Arbeiten mit ist eine einfache Abfrage, die alle Datensätze aus der Tabelle zurückgibt. Geben Sie die folgenden Abfragen in das Suchfeld ein, und klicken Sie auf die Schaltfläche "Suchen".  

```
Event
```

Daten werden in der Standardlistenansicht zurückgegeben, und Sie können sehen, wie viele Datensätze insgesamt zurückgegeben wurden.

![Einfache Abfrage](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

Ist Sie auf der linken Seite des Bildschirms im Filterbereich hinzufügen, Filtern der Abfrage ohne direkt ändern können.  Mehrere Datensatzeigenschaften werden für diesen Datensatztyp angezeigt, und Sie können eine oder mehrere Eigenschaftswerte auf Ihre Suchergebnisse eingrenzen auswählen.

Aktivieren Sie das Kontrollkästchen neben **Fehler** unter **EVENTLEVELNAME** , oder geben Sie Folgendes ein, um die Ergebnisse auf Fehlerereignisse zu beschränken.

```
Event | where (EventLevelName == "Error")
```

![Filter](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

Nachdem Sie die entsprechende Abfragen für Ereignisse, die, denen Sie interessieren haben, speichern Sie sie für den nächsten Schritt.

### <a name="create-alerts"></a>Erstellen von Warnungen
Jetzt betrachten wir ein Beispiel für eine Warnung zu erstellen.

1. Klicken Sie im Azure-Portal auf **alle Dienste**. Geben Sie in der Liste der Ressourcen, **Log Analytics**. Wenn Sie mit der Eingabe beginnen, die Listenfilter entsprechend den Eingaben. Wählen Sie **Protokollanalysen**.
2. Wählen Sie im linken Bereich **Warnungen** , und klicken Sie dann auf **neue Warnungsregel** zwischen dem oberen Rand der Seite, um eine neue Warnung zu erstellen.<br><br> ![Erstellen Sie neue Warnungsregel](media/configure-azure-monitor/alert-rule-02.png)<br>
3. Für den ersten Schritt unter dem **Erstellen von Warnungen** Abschnitt setupbegrüßungsbildschirm Log Analytics-Arbeitsbereich als Ressource auswählen, da es sich um einen protokollbasierten Warnungssignal handelt.  Filtern Sie die Ergebnisse durch Auswählen der spezifischen **Abonnement** aus der Dropdown-Liste, wenn sich mehr als 1 ist, die zuvor erstellten Log Analytics-Arbeitsbereich enthält.  Filter der **Ressourcentyp** dazu **Log Analytics** aus der Dropdown-Liste.  Wählen Sie abschließend die **Ressource** **DefaultLAWorkspace** , und klicken Sie dann auf **Fertig**.<br><br> ![Warnung Schritt 1 Aufgabe erstellen](media/configure-azure-monitor/alert-rule-03.png)<br>
4. Im Abschnitt **Warnungskriterien**, klicken Sie auf **Kriterien hinzufügen** Ihre gespeicherte Abfrage auswählen, und geben Sie dann die Logik, die die Warnungsregel folgt.
5. Konfigurieren Sie die Warnung mit den folgenden Informationen ein:  
   a. Von der **basierend auf** Dropdown-Liste **aufgrund metrischer Messungen**.  Eine metrische Maßeinheit wird eine Warnung für jedes Objekt in der Abfrage mit einem Wert erstellt, die unsere angegebenen Schwellenwert überschreitet.  
   b. Für die **Bedingung**Option **größer als** , und geben Sie einen Thershold.  
   c. Dann definieren Sie, wann die Warnung auslösen. Wählen Sie z. B. beispielsweise **aufeinanderfolgende sicherheitsverletzungen** , und wählen Sie in der Dropdown-Listenfeld **größer als** den Wert 3.  
   d. Bearbeiten Sie unter Auswertung basierend auf den Abschnitt der **Zeitraum** Wert **30** Minuten und **Häufigkeit** auf 5. Die Regel wird alle fünf Minuten ausgeführt und Zurückgeben von Datensätzen, die innerhalb der letzten 30 Minuten nach der aktuellen Uhrzeit erstellt wurden.  Festlegen des Zeitraums in einem größeren Fenster Konten für das volle Potenzial von Datenlatenz und stellt sicher, dass der Abfrage zurückgegeben Daten zur Vermeidung einer falsch negativ wird, in dem die Warnung niemals ausgelöst.  
6. Klicken Sie auf **Fertig** um die Warnungsregel abzuschließen.<br><br> ![Konfigurieren von Warnungssignal](media/configure-azure-monitor/alert-signal-logic-02.png)<br> 
7. Geben Sie einen Namen für Ihre Warnung im jetzt in der zweiten Schritt Verschieben der **Name der Warnungsregel** Feld, z. B. **Warnung für alle Fehlerereignisse**.  Geben Sie einen **Beschreibung** mit Einzelheiten zur Warnung, und wählen Sie **kritisch (Schweregrad 0)** für die **Schweregrad** Wert über die angegebenen Optionen.
8. Um die Warnungsregel bei der Erstellung sofort zu aktivieren, akzeptieren Sie den Standardwert für **Regel beim Erstellen aktivieren**.
9. Im dritten und letzten Schritt geben Sie eine **Aktionsgruppe**, die sicherstellt, dass die gleichen Aktionen jeweils ausgeführt werden, eine Warnung wird ausgelöst, und für jede Regel, die Sie definieren, verwendet werden kann. Konfigurieren Sie eine neue Aktionsgruppe mit den folgenden Informationen ein:  
   a. Wählen Sie **neue Aktionsgruppe** und **Aktionsgruppe hinzufügen** angezeigt.  
   b. Für **Gruppennamen der Überwachungsaktion**, geben Sie einen Namen wie z. B. **IT-Betrieb -** und **Kurznamen** wie z. B. **Itops-n**.  
   c. Überprüfen Sie die Standardwerte für **Abonnement** und **Ressourcengruppe** richtig sind. Wenn dies nicht der Fall ist, wählen Sie das richtige Abonnement aus der Dropdown-Liste.   
   d. Klicken Sie im Abschnitt "Aktionen" Geben Sie einen Namen für die Aktion, z. B. **E-Mail senden** und wählen Sie unter **Aktionstyp** wählen **E-Mail/SMS/Push/Sprachanruf** aus der Dropdown-Liste. Die **E-Mail/SMS/Push/Sprachanruf** Bereich "Eigenschaften" wird geöffnet, auf der rechten Seite, um zusätzliche Informationen bereitzustellen.  
   e. Auf der **E-Mail/SMS/Push/Sprachanruf** Bereich auswählen und den jeweiligen Anforderungen einrichten. Aktivieren Sie z. B. **-e-Mail** , und geben Sie eine gültige e-Mail-Adresse im SMTP-Adresse, die Nachricht zu übermitteln.  
   f. Klicken Sie auf **OK**, um die Änderungen zu speichern.<br><br> 

    ![Neue Aktionsgruppe erstellen](media/configure-azure-monitor/action-group-properties-01.png)

10. Klicken Sie auf **OK** zum Abschließen der Aktionsgruppe. 
11. Klicken Sie auf **Warnungsregel erstellen** um die Warnungsregel abzuschließen. Die Ausführung beginnt sofort.<br><br> ![Führen Sie die neue Warnungsregel wird erstellt](media/configure-azure-monitor/alert-rule-01.png)<br> 

### <a name="test-alerts"></a>Prüfen von Warnungen

Zu Referenzzwecken ist dies an, wie eine Warnung Beispiel aussieht:

![Warnungs-e-Mail-Beispiel](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage "direkte Speicherplätze"](storage-spaces-direct-overview.md)
- Lesen Sie detaillierte Informationen, die [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-viewdata).
