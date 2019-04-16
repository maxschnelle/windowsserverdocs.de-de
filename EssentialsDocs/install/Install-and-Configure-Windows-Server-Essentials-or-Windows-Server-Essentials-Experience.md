---
title: Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8a2310b178663c6ca32a4e07d11656f1aaf2a11b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Installieren und Konfigurieren von Windows Server Essentials oder Windows Server Essentials Experience

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Windows Server Essentials ist ein idealer erster Server für kleine Unternehmen mit bis zu 25 Benutzer und 50 Geräte. Für Organisationen mit bis zu 100 Benutzern und 200 Geräten können Sie jetzt Windows Server 2012 R2 mit installierter Windows Server Essentials Experience-Rolle. In diesem Thema zielt auf beide Szenarien.  
  
Windows Server Essentials Experience ist eine Rolle in Windows Server 2016 und ermöglicht Ihnen, alle Features (z. B. Remotewebzugriff und PC-Sicherung) nutzen, die Ihnen zur Verfügung stehen in Windows Server Essentials ohne die Sperren und Beschränkungen, die in Windows Server Essentials erzwungen werden. Diese Serverrolle steht auch in Windows Server Essentials und ist standardmäßig aktiviert.
  
Beachten Sie die folgenden Einschränkungen, vor der Installation von Windows Server Essentials oder die Essentials Experience-Rolle.  
  
|Windows Server Essentials Experience in Windows Server Essentials|Windows Server Essentials Experience in WindowsServer 2016
|----|----|
|-Muss der Domänencontroller im Stamm der Gesamtstruktur und Domäne sein und muss alle FSMO-Rollen.<br /><br /> -Kann in einer Umgebung mit einer bereits vorhandenen Active Directory-Domäne installiert werden (es gibt jedoch eine Toleranzperiode von 21 Tagen Kulanzzeitraum).|-Ist kein Domänencontroller sein, wenn es in einer Umgebung mit einer bereits vorhandenen Active Directory-Domäne installiert ist.<br /><br /> – Wenn es sich um eine Active Directory-Domäne nicht vorhanden ist, Installieren der Rolle Active Directory-Domäne erstellt, und der Server wird der Domänencontroller im Stamm der Gesamtstruktur und Domäne, halten alle FSMO-Rollen werden.  
|Kann nur in einer einzelnen Domäne bereitgestellt werden.|Kann nur in einer einzelnen Domäne bereitgestellt werden.  
|Ein schreibgeschützten Domänencontroller kann nicht in der Domäne vorhanden sein.|Ein schreibgeschützten Domänencontroller kann nicht in der Domäne vorhanden sein.

> [!NOTE]
>  Informationen zum Herunterladen von Evaluierungsversionen des Betriebssystems finden Sie auf der TechNet-Evaluierungscenter:  
>   
>  [Herunterladen von WindowsServer 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials herunterladen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>Installationsoptionen  
 Dieses Dokument enthält eine schrittweise Anleitung zum Installieren und Konfigurieren von Windows Server Essentials. Je nach Netzwerkumgebung haben Sie die folgenden Installationsoptionen zur Verfügung:  
  
-    Windows Server Essentials (mit der Windows Server Essentials Experience-Rolle standardmäßig aktiviert)  
  
-    Windows Server 2016 mit installierter Windows Server Essentials Experience-Rolle  
 
|-Umgebung|Beschreibung|Verwandte Abschnitt|  
|----------------------------|-----------------|---------------------|  
|Neue Active Directory-Umgebung|Sie können Windows Server Essentials zum Erstellen einer neuen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|Vorhandene Active Directory-Umgebung|Sie können Windows Server Essentials in einer vorhandenen Active Directory-Umgebung installieren.|[Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|Virtuelle Umgebung|Sie können Windows Server Essentials als virtuellen Computer bereitstellen.|[Ihre Umgebung zu virtualisieren](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|Automatisierte Bereitstellung|Sie können die Bereitstellung von Windows Server Essentials mithilfe von Windows PowerShell automatisieren.|[Installieren und Konfigurieren von Windows Server Essentials mithilfe von Windows PowerShell](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>Bevor Sie beginnen  
 Überprüfen Sie vor dem Beginn der Installations der folgenden Dokumentation:  
  
-   [Windows Server Essentials – Produktübersicht](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Systemanforderungen für Windows Server Essentials](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a>Bereitstellen von Windows Server Essentials zum Einrichten einer neuen Active Directory-Umgebung  
 Windows Server Essentials bietet eine Möglichkeit, ein Active Directory-Umgebung und zugehörige Serverfeatures schnell einzurichten.  
  
###  <a name="BKMK_WSEDeploy"></a>Bereitstellen von Windows Server Essentials  
 Wenn Sie Windows Server Essentials verwenden, ist Windows Server Essentials-Umgebung bereits aktiviert. Allerdings müssen Sie einige Schritte zum Konfigurieren des Servers ausführen.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>So konfigurieren Sie Windows Server Essentials auf einem physischen server  
  
1.  Nachdem die Windows **Willkommen** Seite, die **Konfigurieren von Windows Server Essentials-Assistenten** auf Ihrem Desktop angezeigt wird.  
  
2.  Führen Sie die Anweisungen, um den Assistenten wie folgt abzuschließen:  
  
    1.  Auf der **Konfigurieren von Windows Server Essentials** auf **Weiter**.  
  
    2.  In **Uhrzeiteinstellungen**, stellen Sie sicher, dass Ihr Datum, Uhrzeit und Zeitzone richtig sind, und klicken Sie dann auf **Weiter**.  
  
    3.  In **Unternehmensinformationen**, geben Sie den Namen Ihres Unternehmens z. B. **Contoso, Ltd.**, und klicken Sie dann auf **Weiter**. Optional können Sie den internen Domänennamen und den Servernamen ändern.  
  
    4.  In **Erstellen eines Netzwerkadministrators**, geben Sie einen neuen Administratorkontonamen und ein Kennwort.  
  
        > [!NOTE]
        >  Verwenden Sie nicht die standardmäßige **Administrator** Kontoname und Kennwort.  
  
    5.  Klicken Sie auf **konfigurieren**.  
  
3.  Der Server wird mehrmals neu starten, bei der Konfiguration, und Ihre Anmeldungen erfolgen automatisch, bis die Konfiguration abgeschlossen ist. Dieser Vorgang dauert ca. 20 Minuten.  
  
4.  Klicken Sie auf dem Desktop auf das Dashboard-Symbol, um das serverdashboard zu starten. Auf der **Home** schließen die **Einstieg** für Aufgaben der **Setup** Registerkarte.  
  
 Nachdem Sie die Server-Konfiguration abgeschlossen haben, wird der Server, auf der Windows Server Essentials ausgeführt wird als Domänencontroller eingerichtet werden.  
  
###  <a name="BKMK_DeployWSERole"></a>Bereitstellen von Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard und Datacenter  
 Sie können Server-Manager verwenden, aktivieren und Konfigurieren von Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter mithilfe des folgenden Verfahrens.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Bereitstellen von Windows Server Essentials Experience-Rolle in Windows Server 2012 R2  
  
1.  Melden Sie sich an den Server als lokaler Administrator an.  
  
2.  Öffnen **Server-Manager**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**.  
  
3.  In **Serverrollen auswählen**, wählen die **Windows Server Essentials Experience** Rolle. Klicken Sie im Dialogfeld auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
4.  In **Features**, klicken Sie auf **Weiter**.  
  
5.  Überprüfen der **Windows Server Essentials Experience** Beschreibung, und klicken Sie dann auf **Weiter**.  
  
6.  In den folgenden Seiten klicken Sie auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **installieren**.  
  
7.  Nachdem die Installation abgeschlossen ist, sollte Windows Server Essentials Experience als Serverrolle im Server-Manager aufgeführt.  
  
8.  Im meldungsinfobereich im Server-Manager, klicken Sie auf das Kennzeichen, und klicken Sie dann auf **Konfigurieren von Windows Server Essentials**.  
  
9. (Optional) Ändern Sie den Namen des Servers.  
  
    > [!IMPORTANT]
    >  Sie können nicht den Namen des Servers nicht ändern, nachdem Sie Windows Server Essentials konfiguriert haben.  
  

10. Folgen Sie dem Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

10. Folgen Sie dem Assistenten zum Konfigurieren von Windows Server Essentials, wie zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

  
##  <a name="BKMK_ExistingAD"></a>Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung  
 Sie können Windows Server Essentials auch bereitstellen, wenn Ihre Organisation bereits über eine vorhandene Active Directory-Umgebung verfügt. Darüber hinaus können Sie auswählen, wenn Sie Windows Server Essentials als Domänencontroller bereitstellen möchten.  
  
> [!IMPORTANT]
>  Diese Option ist nur verfügbar, wenn Sie die Windows Server Essentials Experience-Rolle in Windows Server 2012 R2 Standard oder Windows Server 2012 R2 Datacenter bereitstellen.  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>Bereitstellen von Windows Server Essentials in einer vorhandenen Active Directory-Umgebung  
  
1.  (Optional) Ändern Sie den Namen des Servers.  
  
    > [!IMPORTANT]
    >  Sie können nicht den Namen des Servers nicht ändern, nachdem Sie Windows Server Essentials konfiguriert haben.  
  
2.  Verknüpfen Sie Ihren Server, die mit Windows Server Essentials zu einer vorhandenen Domäne wie folgt:  
  
    1.  Wenn dieser Server ein Domänencontroller sein soll, richten Sie den Server als Replikat-Domänencontroller.  
  
    2.  Wenn Sie nicht, dass der Server ein Domänencontroller sein möchten, Verbinden des Servers mit Ihrer Domäne mit den systemeigenen Windows-Tools.  
  
3.  Starten Sie den Server neu, und melden Sie sich an den Server als Domänenadministrator an.  
  
4.  Öffnen Sie Server-Manager, und klicken Sie dann auf **Hinzufügen von Rollen und Features**.  
  
5.  Auf den Seiten, die darauf folgen, auf **Weiter**.  
  
6.  In **Serverrollen auswählen**Option **Windows Server Essentials Experience**. Klicken Sie im Dialogfeld auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  In **Features**, klicken Sie auf **Weiter**.  
  
8.  Überprüfen der **Windows Server Essentials Experience** Beschreibung, und klicken Sie dann auf **Weiter**.  
  
9. In den folgenden Seiten klicken Sie auf **Weiter**, und klicken Sie dann auf der Bestätigungsseite auf **installieren**.  
  
10. Nachdem die Installation abgeschlossen ist, wird Windows Server Essentials Experience als Serverrolle im Server-Manager aufgeführt.  
  
11. Klicken Sie im meldungsinfobereich im **Server-Manager**, klicken Sie auf das Kennzeichen, und klicken Sie dann auf **Konfigurieren von Windows Server Essentials**.  
  
12. Führen Sie den Assistenten zum Konfigurieren von Windows Server Essentials. Je nach Ihrer Active Directory-Konfiguration werden Sie informiert, ob Sie Windows Server Essentials auf einem Domänencontroller oder als Mitglied einer Domäne konfigurieren. Klicken Sie auf **konfigurieren** an der Konfiguration zu beginnen. Die Konfiguration dauert ungefähr 10 Minuten.  
  
##  <a name="BKMK_VirtualWSE"></a>Ihre Umgebung zu virtualisieren  
  Windows Server Essentials, Windows Server 2012 R2 Standard und Windows Server 2012 R2 Datacenter können als virtuelle Computer ausgeführt werden. Sie können virtuelle Computer mithilfe der Hyper-V-Verwaltungstools auf einem Server mit Hyper-V ausführen. Aus lizenzierungsperspektive ermöglicht Windows Server Essentials die Hyper-V-Rolle einzurichten und Ihre Umgebung zu virtualisieren. Die Lizenz ermöglicht Ihnen die Einrichtung eines anderen Gastbetriebssystems, auf denen Windows Server Essentials ausgeführt wird. Je nach Ihren "¢ s-Konfiguration, Windows Server Essentials können Sie nahtlose Einrichtung einer virtualisierten Umgebung.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Bereitstellen von Windows Server Essentials als virtuellen Computer  
  
1.  Nach der Windows-Willkommensseite (je nach "Konfiguration Ihres Systems Anbieter ¢ s) die **vor dem Beginn** Seite bietet eine Option zum Windows Server Essentials als virtuelle Instanz oder auf physische Hardware einrichten. Die Verfügbarkeit dieser Optionen ist von Ihrem Systemanbieter vordefiniert, und beide Optionen möglicherweise nicht immer zur Verfügung. So installieren Sie Windows Server Essentials als virtuellen Computer, in **Installieren von Windows Server Essentials**Option **als virtuelle Instanz installieren**, und klicken Sie dann auf **konfigurieren**.  
  
2.  Der Assistent wird eine virtuelle Maschine bereitgestellt werden sollen, etwa fünf Minuten dauert.  
  

3.  Konfigurieren Sie anschließend Windows Server Essentials, wie dies zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

3.  Konfigurieren Sie anschließend Windows Server Essentials, wie dies zuvor im Abschnitt der [Bereitstellen von Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) Abschnitt.  

  
##  <a name="BKMK_PowerShell"></a>Installieren und Konfigurieren von Windows Server Essentials mithilfe von Windows PowerShell  
 Sie können die Installation von Windows Server Essentials mithilfe von Windows PowerShell-Cmdlets automatisieren.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>So installieren Sie Windows Server Essentials mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell-Konsole ein Eingabeaufforderungsfenster mit erhöhten Rechten.  
  
2.  Installieren Sie Windows Server Essentials Experience-Rolle mithilfe des folgenden Befehls:  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  Führen Sie `Get-Help Start-WssConfigurationService`.  
  
    1.  Führen Sie den folgenden Befehl aus, um die Konfiguration für das Einrichten von Windows Server Essentials als Domänencontroller zu starten:  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  Führen Sie den folgenden Befehl an der Konfiguration zum Einrichten von Windows Server Essentials als ein vorhandenes Domänenmitglied zu beginnen. Sie müssen ein Mitglied der Gruppe "Organisations-Admins" und die Gruppe "Domänen-Admins" in Active Directory zum Ausführen dieser Aufgabe sein:  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  Überwachen Sie den Fortschritt der Installation mithilfe der folgenden Befehle ein:  
  
    -   Um den Installationsstatus auf der Statusanzeige angezeigt haben, führen Sie `Get-WssConfigurationStatus  œShowProgress`.  
  
    -   Um den unmittelbaren Fortschritt ohne die Statusanzeige abzurufen, führen Sie `Get-WssConfigurationStatus`.  
  
## <a name="see-also"></a>Siehe auch  
  
-   [Was ist neu in Windows Server Essentials](../get-started/what-s-new.md)  
  
-   [Installieren von Windows Server Essentials](Install-Windows-Server-Essentials.md)  
  
-   [Erste Schritte mit Windows Server Essentials](../get-started/get-started.md)
