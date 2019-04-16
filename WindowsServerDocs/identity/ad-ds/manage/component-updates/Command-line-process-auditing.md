---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: Befehlszeilenprozessen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 61e7a5ca2b9c00c9976e6032bb10adb1974020b0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="command-line-process-auditing"></a>Befehlszeilenprozessen

>Gilt für: Windows Server 2016, Windows Server2012 R2

**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
## <a name="overview"></a>(Übersicht)  
  
-   Bereits vorhandene Audit Prozesserstellungsereignis ID 4688 enthält Überwachungsinformationen für Prozesse Befehlszeile.  
  
-   Es wird darüber hinaus SHA1/2-Hash der ausführbaren Datei in das Applocker-Ereignisprotokoll protokolliert.  
  
    -   Application and Services Logs\Microsoft\Windows\AppLocker  
  
-   Sie können über ein Gruppenrichtlinienobjekt, aber es ist standardmäßig deaktiviert  
  
    -   "Befehlszeile in Verarbeitung Erstellung von Ereignissen einschließen"  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 16 Ereignis 4688**  
  
Überprüfen Sie das aktualisierte Ereignis-ID 4688 in REF _Ref366427278 \h Abbildung16.  Aktualisieren Sie zuvor keine Informationen für **Prozessbefehlszeile** protokolliert wird.  Aufgrund dieser zusätzliche Protokollierung können wir nun sehen, dass nicht nur der wscript.exe Prozess gestartet wurde, aber es auch wurde verwendet, um ein VB-Skript auszuführen.  
  
## <a name="configuration"></a>Konfiguration  
Um die Auswirkungen, die dieses Update angezeigt wird, müssen Sie zwei Richtlinieneinstellungen aktivieren.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>Sie benötigen Prozesserstellung überwachen, Ereignis-ID 4688 aktiviert.  
Bearbeiten Sie die folgenden Gruppenrichtlinien zum Aktivieren der Richtlinie Prozesserstellung überwachen:  
  
**Richtlinienspeicherort:** Computerkonfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > erweiterte Sicherheitsüberwachungsrichtlinien-Konfiguration > detaillierte Überwachung  
  
**Richtlinienname:** Prozesserstellung überwachen  
  
**Unterstützt in:** Windows7 und höher  
  
**Beschreibung/Hilfe:**  
  
Diese sicherheitsrichtlinieneinstellung legt fest, ob das Betriebssystem generiert Überwachungsereignisse, wenn ein Prozess (gestartet) erstellt wird und den Namen der Anwendung oder des Benutzers, der Sie erstellt.  
  
Diese Überwachungsereignisse können Sie besser verstehen, wie ein Computer verwendet wird und Benutzeraktivitäten nachverfolgen.  
  
Ereignisvolumen: Niedrig bis Mittel, je nach systemnutzung  
  
**Standard:** nicht konfiguriert  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>Um die Ergänzungen der mit Ereignis-ID 4688 angezeigt wird, müssen Sie die neue Einstellung aktivieren: Befehlszeile in Verarbeitung Erstellung von Ereignissen einschließen  
**Tabelle SEQ Tabelle \\\ * Arabisch 19 Befehl Zeile Prozess-Einstellung**  
  
|Die Konfiguration|Detail|  
|------------------------|-----------|  
|**Pfad**|Erstellung von administrativen Templates\System\Audit|  
|**Einstellung**|**Befehlszeile in Verarbeitung Erstellung von Ereignissen einschließen**|  
|**Standardeinstellung**|Nicht konfiguriert (nicht aktiviert)|  
|**Unterstützt in:**|?|  
|**Beschreibung**|Diese Einstellung bestimmt, welche Informationen protokolliert werden, in Sicherheitsüberwachungsereignisse, wenn ein neuer Prozess erstellt wurde.<br /><br />Diese Einstellung gilt nur, wenn die Richtlinie Prozesserstellung aktiviert ist. Wenn Sie diese Einstellung aktivieren, die Befehlszeileninformationen für jeden Prozess im Rahmen der Prozesserstellung Ereignis 4688 im Nur-Text in das Sicherheitsereignisprotokoll protokolliert werden, wurde "ein neuer Prozess erstellt" auf den Arbeitsstationen und Servern, auf denen diese Einstellung angewendet wird.<br /><br />Wenn Sie deaktivieren oder diese Einstellung nicht konfigurieren, werden die Informationen des Prozesses Befehlszeile in Prozesserstellung Ereignisse nicht berücksichtigt.<br /><br />Standard: Nicht konfiguriert<br /><br />Hinweis: Wenn diese Einstellung aktiviert ist, erstellt jeder Benutzer mit Zugriff zum Lesen der Sicherheitsereignisse die Befehlszeilenargumente für eine erfolgreiche lesen können Prozess. Befehlszeilenargumente können vertrauliche oder private Informationen wie Kennwörter oder Benutzerdaten enthalten.|  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
Wenn Sie Einstellungen für erweiterte Überwachungsrichtlinienkonfiguration verwenden, müssen Sie sicherstellen, dass diese Einstellungen nicht von grundlegenden Überwachungsrichtlinieneinstellungen überschrieben werden.  Ereignis 4719 wird protokolliert, wenn die Einstellungen überschrieben werden.  
  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
Das folgende Verfahren zeigt, wie Sie Konflikte verhindern, indem Sie die Anwendung von alle grundlegenden Überwachungsrichtlinieneinstellungen blockieren.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>Um sicherzustellen, dass die Einstellungen für die erweiterte Überwachungsrichtlinienkonfiguration nicht überschrieben werden  
![Befehlszeilen-Überwachung](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole  
  
2.  Mit der rechten Maustaste Default Domain Policy, und klicken Sie dann auf Bearbeiten.  
  
3.  Doppelklicken Sie auf die Computerkonfiguration, doppelklicken Sie auf Richtlinien, und doppelklicken Sie dann auf Windows-Einstellungen.  
  
4.  Doppelklicken Sie auf Sicherheitseinstellungen, doppelklicken Sie auf lokale Richtlinien, und klicken Sie dann auf Sicherheitsoptionen.  
  
5.  Doppelklicken Sie auf Überwachung: Audit unterkategorieeinstellungen (Windows Vista oder höher) außer Kraft setzen Überwachungsrichtlinieneinstellungen Kategorie, und klicken Sie auf diese Richtlinieneinstellung definieren.  
  
6.  Klicken Sie auf aktiviert, und klicken Sie dann auf OK.  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Prozesserstellung überwachen](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[Erweiterte Sicherheitsüberwachungsrichtlinien Step-by-Step Guide](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>Versuchen Sie Folgendes: Entdecken Sie befehlszeilenprozessen  
  
1.  Aktivieren Sie **Prozesserstellung** Ereignisse und stellen Sie sicher, die erweiterte Überwachungsrichtlinie Konfiguration wird nicht überschrieben.  
  
2.  Erstellen Sie ein Skript, das einige interessante Ereignisse generiert und führen Sie das Skript.  Beachten Sie die Ereignisse.  Das Skript verwendet, um das Ereignis in der Lektion generieren sah folgendermaßen aus:  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  Aktivieren Sie die befehlszeilenprozessen  
  
4.  Ausführen von einem Skript vor und beobachten, ob Ereignisse  
  


