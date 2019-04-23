---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: Überwachen von Befehlszeilenprozessen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 66ae6992775319cf614b0cb4c21f864150746687
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859551"
---
# <a name="command-line-process-auditing"></a>Überwachen von Befehlszeilenprozessen

>Gilt für: Windows Server 2016, Windows Server 2012 R2

**Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
  
-   Das bereits vorhandene Audit Prozesserstellungsereignis ID 4688 enthält jetzt die Überwachungsinformationen für Prozesse, die über die Befehlszeile.  
  
-   Es wird auch SHA1/2-Hash der ausführbaren Datei in das Applocker-Ereignisprotokoll protokolliert.  
  
    -   Anwendungs- und dienstprotokolle\microsoft\windows\applocker  
  
-   Sie ermöglichen, über ein Gruppenrichtlinienobjekt, aber es ist standardmäßig deaktiviert.  
  
    -   "Include über die Befehlszeile in prozesserstellungsereignisse"  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**Figure SEQ Abbildung \\ \* Arabische 16 Ereignis 4688**  
  
Überprüfen Sie das aktualisierte Ereignis-ID 4688 in REF _Ref366427278 \h Abbildung 16 aus.  Aktualisieren Sie zuvor keine Informationen für **Prozessbefehlszeile** ruft protokolliert.  Aufgrund dieser zusätzliche Protokollierung sehen wir jetzt, dass nicht nur der wscript.exe-Prozess gestartet wurde, aber, dass es auch war verwendet, um ein VB-Skript auszuführen.  
  
## <a name="configuration"></a>Konfiguration  
Um die Auswirkungen dieses Updates sehen zu können, müssen Sie zwei Richtlinieneinstellungen aktivieren.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>Sie benötigen die Prozesserstellung überwachen Überwachung aktiviert, um die Ereignis-ID 4688 finden Sie unter.  
Bearbeiten Sie die folgenden Gruppenrichtlinien zum Aktivieren der Richtlinie Prozesserstellung überwachen:  
  
**Richtlinienspeicherort:** Computerkonfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > erweiterte Überwachungskonfiguration > detaillierte nachverfolgung  
  
**Richtlinienname:** Prozesserstellung überwachen  
  
**Unterstützt auf:** Windows 7 und höher  
  
**Beschreibung/Hilfe:**  
  
Diese sicherheitseinstellung für die Richtlinie bestimmt, ob das Betriebssystem generiert Überwachungsereignissen, wenn ein Prozess (er beginnt) erstellt wird und den Namen des Programms oder der Benutzer, die sie erstellt haben.  
  
Diese Ereignisse überwachen können dabei helfen herauszufinden, wie ein Computer verwendet wird und die Benutzeraktivität nachverfolgen.  
  
Ereignisvolumen: Niedrig bis Mittel, je nach Verwendung des Systems  
  
**Standardwert:** Nicht konfiguriert  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>Um den Ereignis-ID 4688-Erweiterungen anzuzeigen, müssen Sie die neue richtlinieneinstellung aktivieren: Über die Befehlszeile in prozesserstellungsereignisse einschließen  
**Tabelle SEQ Tabelle \\ \* Arabische 19 Befehl Zeile Prozess richtlinieneinstellung**  
  
|Richtlinienkonfiguration|Details|  
|------------------------|-----------|  
|**Pfad**|Administrative Templates\System\Audit Prozesserstellung|  
|**Einstellung**|**Über die Befehlszeile in prozesserstellungsereignisse einschließen**|  
|**Standardeinstellung**|Nicht konfiguriert (nicht aktiviert)|  
|**Unterstützt auf:**|?|  
|**Beschreibung**|Mit dieser richtlinieneinstellung wird bestimmt, welche Informationen protokolliert werden, in Sicherheitsüberwachungsereignisse, wenn ein neuer Prozess erstellt wurde.<br /><br />Diese Einstellung gilt nur, wenn die Prozesserstellung überwachen-Richtlinie aktiviert ist. Wenn Sie dieser richtlinieneinstellung kann die Informationen über die Befehlszeile festgelegt aktivieren, für jeden Prozess im nur-Text in das Sicherheitsereignisprotokoll als Teil der Prozesserstellung überwachen Ereignis 4688 protokolliert werden, "ein neuer Prozess wurde," auf den Arbeitsstationen und Servern, auf dem diese Richtlinie die Einstellung angewendet wird.<br /><br />Wenn Sie diese richtlinieneinstellung nicht konfigurieren oder deaktivieren, werden die Informationen des Prozesses über die Befehlszeile in Prozesserstellung überwachen-Ereignisse nicht berücksichtigt.<br /><br />Standardwert: Nicht konfiguriert<br /><br />Hinweis: Wenn diese richtlinieneinstellung aktiviert ist, erstellt jeder Benutzer mit Zugriff zum Lesen, dass die Sicherheitsereignisse, lesen Sie die Befehlszeilenargumente für jeden erfolgreich sein werden Prozess. Befehlszeilenargumente können sensible oder private Informationen wie Kennwörter oder Benutzerdaten enthalten.|  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
Wenn Sie die Einstellungen für die erweiterte Überwachungsrichtlinienkonfiguration verwenden, müssen Sie sicherstellen, dass diese Einstellungen nicht von den grundlegenden Überwachungsrichtlinieneinstellungen überschrieben werden.  Ereignis 4719 wird protokolliert, wenn die Einstellungen überschrieben werden.  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
Das folgende Verfahren veranschaulicht, wie Sie Konflikte verhindern, indem Sie die Anwendung grundlegender Überwachungsrichtlinieneinstellungen blockieren.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>So stellen Sie sicher, dass die Einstellungen unter „Erweiterte Überwachungsrichtlinienkonfiguration“ nicht überschrieben werden:  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole  
  
2.  Mit der rechten Maustaste Standardrichtlinie der Domäne, und klicken Sie dann auf Bearbeiten.  
  
3.  Doppelklicken Sie auf die Computerkonfiguration, doppelklicken Sie auf Richtlinien, und doppelklicken Sie dann auf Windows-Einstellungen.  
  
4.  Doppelklicken Sie auf die Sicherheitseinstellungen, doppelklicken Sie auf die lokale Richtlinien und klicken Sie dann auf Sicherheitsoptionen.  
  
5.  Doppelklicken Sie auf die Überwachung: Unterkategorie sicherheitsüberwachungs-Richtlinieneinstellungen zu erzwingen (Windows Vista oder höher) außer Kraft setzen kategorieeinstellungen der Überwachungsrichtlinie, und klicken Sie auf diese richtlinieneinstellung definieren.  
  
6.  Klicken Sie auf aktiviert, und klicken Sie dann auf OK.  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Prozesserstellung überwachen](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[Advanced Security Audit-Richtlinie schrittweise Anleitung](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>Versuchen Sie Folgendes aus: Untersuchen von befehlszeilenprozessen  
  
1.  Aktivieren Sie **Prozesserstellung Überwachen** Ereignisse und stellen Sie sicher, die erweiterte Überwachungsrichtlinie-Konfiguration wird nicht überschrieben.  
  
2.  Erstellen Sie ein Skript, das einige interessante Ereignisse generiert und führen Sie das Skript ein.  Beachten Sie die Ereignisse an.  Das Skript verwendet, um das Ereignis in der Lektion generieren sah folgendermaßen aus:  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  Aktivieren der befehlszeilenprozessen  
  
4.  Führen Sie das gleiche Skript wie vor und beobachten, ob Ereignisse  
  


