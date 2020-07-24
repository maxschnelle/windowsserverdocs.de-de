---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: Überwachen von Befehlszeilenprozessen
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5ca29f1eef61bd11b2ceede4f335c029412e7331
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966402"
---
# <a name="command-line-process-auditing"></a>Überwachen von Befehlszeilenprozessen

>Gilt für: Windows Server 2016, Windows Server 2012 R2

**Autor**: Justin Turner, Senior Support Eskalations Techniker mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
  
-   Die bereits vorhandene Überwachungs Ereignis-ID 4688 für die Prozesserstellung enthält jetzt Überwachungsinformationen für Befehlszeilen Prozesse.  
  
-   Außerdem wird der SHA1/2-Hash der ausführbaren Datei im AppLocker-Ereignisprotokoll protokolliert.  
  
    -   Anwendungs-und dienstprotokolle\microsoft\windows\applocker  
  
-   Sie aktivieren per GPO, sind aber standardmäßig deaktiviert.  
  
    -   "Befehlszeile in Prozess Erstellungs Ereignisse einschließen"  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**Abbildung * Abbildung \\ \* Arabisch 16 Ereignis 4688**  
  
Überprüfen Sie die aktualisierte Ereignis-ID 4688 in Ref _Ref366427278 \h Abbildung 16.  Vor diesem Update wird keine der Informationen für die **Prozess Befehlszeile** protokolliert.  Aufgrund dieser zusätzlichen Protokollierung können wir nun sehen, dass nicht nur der wscript.exe Prozess gestartet wurde, sondern auch ein VB-Skript ausgeführt wurde.  
  
## <a name="configuration"></a>Konfiguration  
Um die Auswirkungen dieses Updates anzuzeigen, müssen Sie zwei Richtlinien Einstellungen aktivieren.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>Die Überwachung der Überwachungsprozess Erstellung muss aktiviert sein, damit die Ereignis-ID 4688 angezeigt wird.  
Bearbeiten Sie die folgende Gruppenrichtlinie, um die Richtlinie für die Überwachungsprozess Erstellung zu aktivieren:  
  
**Richtlinien Speicherort:** Computer Konfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > erweiterte Überwachungskonfiguration > ausführliche Nachverfolgung  
  
**Richtlinien Name:** Prozesserstellung überwachen  
  
**Unterstützt für:** Windows 7 und höher  
  
**Beschreibung/Hilfe:**  
  
Diese Sicherheitsrichtlinien Einstellung bestimmt, ob das Betriebssystem Überwachungs Ereignisse generiert, wenn ein Prozess erstellt wird (startet), und der Name des Programms oder Benutzers, von dem das Betriebssystem erstellt wurde.  
  
Mithilfe dieser Überwachungs Ereignisse können Sie nachvollziehen, wie ein Computer verwendet wird, und die Benutzeraktivität nachverfolgen.  
  
Ereignisvolumen: Niedrig bis mittel, je nach Systemnutzung  
  
**Standardwert:** Nicht konfiguriert  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>Um die Ergänzungen der Ereignis-ID 4688 anzuzeigen, müssen Sie die neue Richtlinien Einstellung "Befehlszeile in Prozess Erstellungs Ereignisse einschließen" aktivieren.  
**Tabelle in der Tabelle \\ \* Arabisch 19 Befehlszeilen-Prozess Richtlinien Einstellung**  
  
|Richtlinienkonfiguration|Details|  
|------------------------|-----------|  
|**Pfad**|Administrative vorlagen\system\überwachungs Prozesserstellung|  
|**Einstellung**|**Befehlszeile in Prozess Erstellungs Ereignisse einschließen**|  
|**Standardeinstellung**|Nicht konfiguriert (nicht aktiviert)|  
|**Unterstützt auf:**|?|  
|**Beschreibung**|Mit dieser Richtlinien Einstellung wird festgelegt, welche Informationen in Sicherheits Überwachungs Ereignissen protokolliert werden, wenn ein neuer Prozess erstellt wurde.<p>Diese Einstellung gilt nur, wenn die Richtlinie für die Überwachungsprozess Erstellung aktiviert ist. Wenn Sie diese Richtlinien Einstellung aktivieren, werden die Befehlszeilen Informationen für jeden Prozess im Rahmen des Überwachungsprozess Erstellungs Ereignisses 4688, "ein neuer Prozess wurde erstellt", auf den Arbeitsstationen und Servern, auf denen diese Richtlinien Einstellung angewendet wird, als nur-Text im Sicherheits Ereignisprotokoll protokolliert.<p>Wenn Sie diese Richtlinien Einstellung deaktivieren oder nicht konfigurieren, werden die Befehlszeilen Informationen des Prozesses nicht in Überwachungsprozess-Erstellungs Ereignisse eingeschlossen.<p>Standard: Nicht konfiguriert<p>Hinweis: Wenn diese Richtlinien Einstellung aktiviert ist, kann jeder Benutzer mit Zugriff zum Lesen der Sicherheitsereignisse die Befehlszeilenargumente für jeden erfolgreich erstellten Prozess lesen. Befehlszeilenargumente können vertrauliche oder private Informationen (z. b. Kenn Wörter oder Benutzerdaten) enthalten.|  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
Wenn Sie die Einstellungen für die erweiterte Überwachungsrichtlinienkonfiguration verwenden, müssen Sie sicherstellen, dass diese Einstellungen nicht von den grundlegenden Überwachungsrichtlinieneinstellungen überschrieben werden.  Das Ereignis 4719 wird protokolliert, wenn die Einstellungen überschrieben werden.  
  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
Das folgende Verfahren veranschaulicht, wie Sie Konflikte verhindern, indem Sie die Anwendung grundlegender Überwachungsrichtlinieneinstellungen blockieren.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>So stellen Sie sicher, dass die Einstellungen unter „Erweiterte Überwachungsrichtlinienkonfiguration“ nicht überschrieben werden:  
![Überprüfung der Befehlszeile](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  Öffnen Sie die Gruppenrichtlinie-Verwaltungskonsole.  
  
2.  Klicken Sie mit der rechten Maustaste auf Standarddomänenrichtlinie, und klicken Sie dann auf Bearbeiten.  
  
3.  Doppelklicken Sie auf Computerkonfiguration, doppelklicken Sie auf Richtlinien, und doppelklicken Sie dann auf Windows-Einstellungen.  
  
4.  Doppelklicken Sie auf Sicherheitseinstellungen, doppelklicken Sie auf lokale Richtlinien, und klicken Sie dann auf Sicherheitsoptionen.  
  
5.  Doppelklicken Sie auf Überwachung: Unterkategorieeinstellungen der Überwachungsrichtlinie erzwingen (Windows Vista oder höher), um Kategorieeinstellungen der Überwachungsrichtlinie außer Kraft zu setzen, und klicken Sie dann auf Diese Richtlinieneinstellung definieren.  
  
6.  Klicken Sie auf Aktiviertund dann auf OK.  
  
## <a name="additional-resources"></a>Weitere Ressourcen  
[Prozesserstellung überwachen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941613(v=ws.10))  
  
[Schritt-für-Schritt-Anleitung für die erweiterte Sicherheits Überwachungsrichtlinie](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd408940(v=ws.10))  
  
[AppLocker: häufig gestellte Fragen](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee619725(v=ws.10))  
  
## <a name="try-this-explore-command-line-process-auditing"></a>Versuchen Sie Folgendes: Überprüfen der Befehlszeilen Prozessüberwachung  
  
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
  
