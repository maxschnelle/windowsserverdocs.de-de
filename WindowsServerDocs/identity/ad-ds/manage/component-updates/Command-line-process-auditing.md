---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: Überwachen von Befehlszeilenprozessen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5d5ab971327ab7ec16bf2748571882458cc38f72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368987"
---
# <a name="command-line-process-auditing"></a>Überwachen von Befehlszeilenprozessen

>Gilt für: Windows Server 2016, Windows Server 2012 R2

**Autor**: Justin Turner, Senior Support Eskalations Ingenieur bei der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
  
-   Die bereits vorhandene Überwachungs Ereignis-ID 4688 für die Prozesserstellung enthält jetzt Überwachungsinformationen für Befehlszeilen Prozesse.  
  
-   Außerdem wird der SHA1/2-Hash der ausführbaren Datei im AppLocker-Ereignisprotokoll protokolliert.  
  
    -   Anwendungs-und dienstprotokolle\microsoft\windows\applocker  
  
-   Sie aktivieren per GPO, sind aber standardmäßig deaktiviert.  
  
    -   "Befehlszeile in Prozess Erstellungs Ereignisse einschließen"  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**Abbildung * Abbildung \\ @ no__t-2 Arabisch, 16-Ereignis 4688**  
  
Überprüfen Sie die aktualisierte Ereignis-ID 4688 in Ref _Ref366427278 \h Abbildung 16.  Vor diesem Update wird keine der Informationen für die **Prozess Befehlszeile** protokolliert.  Aufgrund dieser zusätzlichen Protokollierung können wir nun sehen, dass nicht nur der Prozess "Wscript. exe" gestartet wurde, sondern auch ein VB-Skript ausgeführt wurde.  
  
## <a name="configuration"></a>Konfiguration  
Um die Auswirkungen dieses Updates anzuzeigen, müssen Sie zwei Richtlinien Einstellungen aktivieren.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>Die Überwachung der Überwachungsprozess Erstellung muss aktiviert sein, damit die Ereignis-ID 4688 angezeigt wird.  
Bearbeiten Sie die folgende Gruppenrichtlinie, um die Richtlinie für die Überwachungsprozess Erstellung zu aktivieren:  
  
**Richtlinien Speicherort:** Computer Konfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > Erweiterte Überwachungskonfiguration > Ausführliche Nachverfolgung  
  
**Richtlinien Name:** Prozesserstellung überwachen  
  
**Unterstützt für:** Windows 7 und höher  
  
**Beschreibung/Hilfe:**  
  
Diese Sicherheitsrichtlinien Einstellung bestimmt, ob das Betriebssystem Überwachungs Ereignisse generiert, wenn ein Prozess erstellt wird (startet), und der Name des Programms oder Benutzers, von dem das Betriebssystem erstellt wurde.  
  
Mithilfe dieser Überwachungs Ereignisse können Sie nachvollziehen, wie ein Computer verwendet wird, und die Benutzeraktivität nachverfolgen.  
  
Ereignisvolumen: Niedrig bis Mittel, abhängig von der Systemnutzung  
  
**Vorgegebene** Nicht konfiguriert  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>Um die Ergänzungen der Ereignis-ID 4688 anzuzeigen, müssen Sie die neue Richtlinien Einstellung aktivieren: Befehlszeile in Prozess Erstellungs Ereignisse einschließen  
**Tabelle: Tabelle \\ @ no__t-2 Arabisch 19 Befehlszeilen-Prozess Richtlinien Einstellung**  
  
|Richtlinienkonfiguration|Details|  
|------------------------|-----------|  
|**Path**|Administrative vorlagen\system\überwachungs Prozesserstellung|  
|**Man**|**Befehlszeile in Prozess Erstellungs Ereignisse einschließen**|  
|**Standardeinstellung**|Nicht konfiguriert (nicht aktiviert)|  
|**Unterstützt für:**|?|  
|**Beschreibung**|Mit dieser Richtlinien Einstellung wird festgelegt, welche Informationen in Sicherheits Überwachungs Ereignissen protokolliert werden, wenn ein neuer Prozess erstellt wurde.<br /><br />Diese Einstellung gilt nur, wenn die Richtlinie für die Überwachungsprozess Erstellung aktiviert ist. Wenn Sie diese Richtlinien Einstellung aktivieren, werden die Befehlszeilen Informationen für jeden Prozess im Rahmen des Überwachungsprozess Erstellungs Ereignisses 4688, "ein neuer Prozess wurde erstellt" auf den Arbeitsstationen und Servern, auf denen diese Richtlinie erstellt wurde, als nur-Text im Sicherheits Ereignisprotokoll protokolliert. die Einstellung wird angewendet.<br /><br />Wenn Sie diese Richtlinien Einstellung deaktivieren oder nicht konfigurieren, werden die Befehlszeilen Informationen des Prozesses nicht in Überwachungsprozess-Erstellungs Ereignisse eingeschlossen.<br /><br />Standardwert: Nicht konfiguriert<br /><br />Hinweis: Wenn diese Richtlinien Einstellung aktiviert ist, kann jeder Benutzer mit Zugriff zum Lesen der Sicherheitsereignisse die Befehlszeilenargumente für jeden erfolgreich erstellten Prozess lesen. Befehlszeilenargumente können vertrauliche oder private Informationen (z. b. Kenn Wörter oder Benutzerdaten) enthalten.|  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
Wenn Sie die Einstellungen für die erweiterte Überwachungsrichtlinienkonfiguration verwenden, müssen Sie sicherstellen, dass diese Einstellungen nicht von den grundlegenden Überwachungsrichtlinieneinstellungen überschrieben werden.  Das Ereignis 4719 wird protokolliert, wenn die Einstellungen überschrieben werden.  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
Das folgende Verfahren veranschaulicht, wie Sie Konflikte verhindern, indem Sie die Anwendung grundlegender Überwachungsrichtlinieneinstellungen blockieren.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>So stellen Sie sicher, dass die Einstellungen unter „Erweiterte Überwachungsrichtlinienkonfiguration“ nicht überschrieben werden:  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  Öffnen Sie die Gruppenrichtlinie-Verwaltungskonsole.  
  
2.  Klicken Sie mit der rechten Maustaste auf Standard Domänen Richtlinie, und klicken Sie auf Bearbeiten.  
  
3.  Doppelklicken Sie auf Computer Konfiguration, doppelklicken Sie auf Richtlinien, und doppelklicken Sie dann auf Windows-Einstellungen.  
  
4.  Doppelklicken Sie auf Sicherheitseinstellungen, doppelklicken Sie auf lokale Richtlinien, und klicken Sie dann auf Sicherheitsoptionen.  
  
5.  Doppelklicken Sie auf überwachen: Erzwingen Sie die Einstellungen für die Unterkategorie der Überwachungsrichtlinie (Windows Vista oder höher), um Einstellungen der Überwachungs Richtlinien Kategorie zu überschreiben, und klicken Sie dann auf diese Richtlinien Einstellung  
  
6.  Klicken Sie auf aktiviert, und klicken Sie dann auf OK.  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Prozesserstellung überwachen](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[Schritt-für-Schritt-Anleitung für die erweiterte Sicherheits Überwachungsrichtlinie](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[applocker: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>Versuchen Sie Folgendes: Überprüfen der Befehlszeilen Verarbeitung  
  
1.  **Erstellungs** Ereignisse für Überwachungsprozesse aktivieren und sicherstellen, dass die erweiterte Überwachungs Richtlinien Konfiguration nicht überschrieben wird  
  
2.  Erstellen Sie ein Skript, mit dem einige relevante Ereignisse generiert werden, und führen Sie das Skript aus.  Beobachten Sie die Ereignisse.  Das Skript, das zum Generieren des Ereignisses in der Lektion verwendet wurde, sieht wie folgt aus:  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  Aktivieren der Überprüfung des Befehlszeilen Prozesses  
  
4.  Führen Sie das gleiche Skript wie zuvor aus, und beobachten Sie die Ereignisse.  
  


