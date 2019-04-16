---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: "Anhang C - geschützte Konten und Gruppen in Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c1d29b61844428115f8b2d1f5d935f225a249659
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: geschützte Konten und Gruppen in Active Directory  
In Active Directory ein Standardsatz von sehr privilegierten Konten und Gruppen gelten als geschützte Konten und Gruppen. Mit den meisten Objekte in Active Directory können delegierte Administratoren (Benutzer, die Berechtigungen zum Verwalten von Active Directory-Objekte wurden) Berechtigungen für Objekte, z. B. Ändern von Berechtigungen für die Mitgliedschaften der Gruppen, z. B. ändern lassen ändern.  

Geschützte Konten und Gruppen, sind der Objekte Berechtigungen allerdings festgelegt und erzwungen, die über einen automatischen Prozess, der sicherstellt, dass die Berechtigungen für die Objekte bleiben konsistent, auch wenn die Objekte sind das Verzeichnis verschoben. Auch wenn ein Benutzer ein geschütztes Objekt Berechtigungen manuell geändert wird, wird dieser Prozess Berechtigungen schnell auf ihre Standardwerte zurückgegeben werden.  

### <a name="protected-groups"></a>Geschützter Gruppen  
Die folgende Tabelle enthält die geschützten Gruppen in Active Directory Domänencontroller-Betriebssystems aufgeführt.  

**Geschützte Konten und Gruppen in Active Directory vom Betriebssystem**  

|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows 2000 SP4 – Windows Server 2003 RTM**|**Windows Server 2003 SP1 oder höher**|**Windows Server 2012, Windows Server 2008 R2, WindowsServer 2008**|  
|Administratoren|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|  
||Administrator|Administrator|Administrator|  
||Administratoren|Administratoren|Administratoren|  
||Sicherungs-Operatoren|Sicherungs-Operatoren|Sicherungs-Operatoren|  
||Zertifikatherausgeber|||  
|Domänen-Admins|Domänen-Admins|Domänen-Admins|Domänen-Admins|  
||Domänencontroller|Domänencontroller|Domänencontroller|  
|Organisations-Admins|Organisations-Admins|Organisations-Admins|Organisations-Admins|  
||KRBTGT|KRBTGT|KRBTGT|  
||Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|  
||||Read-only Domain Controller|  
||Replicator|Replicator|Replicator|  
|Schema-Admins|Schema-Admins|Schema-Admins|Schema-Admins|  
||Server-Operatoren|Server-Operatoren|Server-Operatoren|  

#### <a name="adminsdholder"></a>AdminSDHolder  
Das AdminSDHolder-Objekt dient zum Bereitstellen von "Vorlage" Berechtigungen für die geschützte Konten und Gruppen in der Domäne. AdminSDHolder wird automatisch als ein Objekt im Systemcontainer jeder Active Directory-Domäne erstellt. Der Pfad ist: **CN = AdminSDHolder, CN = System, DC = < Domain_component >, DC = < Domain_component >?.**  

Anders als die meisten Objekte in Active Directory-Domäne, die sich im Besitz der Gruppe "Administratoren" sind, ist die Gruppe "Domänen-Admins" AdminSDHolder zuständig. Standardmäßig können EAs Änderungen an einer beliebigen Domäne AdminSDHolder-Objekt, vornehmen, wie Gruppen für die Domäne Domänen-Admins und Administratoren können. Darüber hinaus auch der Standardbesitzer AdminSDHolder Domänen-Admins der Domäne ist, können Mitglieder der Administratoren "oder" Organisations-Admins des Objekts Besitzrechte.  

#### <a name="sdprop"></a>SDProp  
SDProp ist ein Prozess, der alle 60 Minuten (standardmäßig) auf dem Domänencontroller ausgeführt wird, die der Domäne PDC-Emulator (PDCE) enthält. SDProp vergleicht die Berechtigungen für die Domäne AdminSDHolder-Objekt mit den Berechtigungen für die geschützte Konten und Gruppen in der Domäne. Wenn die Berechtigungen für geschützte Konten und Gruppen die Berechtigungen für das AdminSDHolder-Objekt nicht übereinstimmen, werden die Berechtigungen für die geschützte Konten und Gruppen zurückgesetzt, um die Domäne AdminSDHolder-Objekt übereinstimmen.  

Darüber hinaus ist die Vererbung von Berechtigungen deaktiviert auf geschützten Gruppen und Konten, dies bedeutet, dass selbst wenn die Konten und Gruppen in verschiedenen Speicherorten in das Verzeichnis verschoben werden, sie Berechtigungen von ihren neuen übergeordneten Objekten nicht erben. Vererbung ist für das AdminSDHolder-Objekt deaktiviert, sodass Änderungen an den übergeordneten Objekten nicht die Berechtigungen des AdminSDHolder ändern.  

##### <a name="changing-sdprop-interval"></a>SDProp Intervall ändern  
In der Regel müssen Sie nicht das Intervall auf dem SDProp ausgeführt wird, mit Ausnahme von Testzwecken zu ändern. Wenn Sie das Intervall SDProp auf dem PDCE für die Domäne ändern müssen verwenden Sie "regedit" hinzufügen oder ändern den AdminSDProtectFrequency DWORD-Wert in HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters.  

Der Wertebereich liegt in 7200 (eine Minute bis zwei Stunden) von 60 Sekunden. Um die Änderungen zu stornieren, löschen Sie AdminSDProtectFrequency-Schlüssel, wodurch SDProp zurück, die 60-Minuten-Intervall wiederherzustellen. Sie sollten im Allgemeinen nicht dieses Intervall in Production Domänen reduzieren, wie LSASS Verarbeitungsaufwand auf dem Domänencontroller erhöhen können. Die Auswirkung dieser Zunahme ist abhängig von der Anzahl der geschützten Objekte in der Domäne.  

##### <a name="running-sdprop-manually"></a>Manuelles Ausführen von SDProp  
Die führt dazu, dass die Aufgabe sofort ausgeführt, jedoch wirkt sich nicht auf die geplante Ausführung es ist besser testen AdminSDHolder Änderungen SDProp manuell ausführen. Manuelles Ausführen von SDProp ist ausgeführte etwas anders auf Domänencontrollern unter Windows Server 2008 und älteren Versionen als ist auf Domänencontrollern unter Windows Server 2012 oder Windows Server 2008 R2.  

Verfahren für die Ausführung von SDProp manuell unter älteren Betriebssystemen finden Sie unter [Microsoft Support-Artikel 251343](https://support.microsoft.com/kb/251343), und folgen eine schrittweise Anleitung zum älteren und neueren Betriebssystemen. In beiden Fällen müssen Sie zum RootDSE-Objekt in Active Directory verbinden und führen Sie einen Änderungsvorgang mit einer null-DN für das RootDSE-Objekt, geben Sie den Namen des Vorgangs als das Attribut zu ändern. Weitere Informationen zu den änderbaren Vorgänge für das RootDSE-Objekt, finden Sie unter [RootDSE ändern Operations](https://msdn.microsoft.com/library/cc223297.aspx) auf der MSDN-Website.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Ausgeführten SDProp manuell in WindowsServer 2008 oder früher  
Sie können erzwingen, dass SDProp mithilfe von Ldp.exe oder durch Ausführen eines LDAP-Änderung Skripts ausführen. Führen Sie mithilfe von Ldp.exe SDProp führen Sie die folgenden Schritte aus, nachdem Sie das AdminSDHolder-Objekt in einer Domäne geändert haben:  

1.  Starten Sie **Ldp.exe**.  

2.  Klicken Sie auf **Verbindung** auf dem Dialogfeld "Ldp", und klicken Sie dann auf **verbinden**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3.  In der **verbinden** Dialogfeld ein, geben Sie den Namen des Domänencontrollers für die Domäne, die die Rolle des PDC-Emulator (PDCE) enthält, und klicken Sie auf **OK**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4.  Stellen Sie sicher, dass Sie durch erfolgreich angeschlossen haben **Dn: (RootDSE)** im folgenden Screenshot, klicken Sie auf **Verbindung** , und klicken Sie auf **binden**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5.  In der **binden** Dialogfeld Geben Sie die Anmeldeinformationen eines Benutzerkontos mit der Berechtigung zum Ändern des RootDSE-Objekts. (Wenn Sie als dieser Benutzer angemeldet sind, können Sie auswählen **Bindung als** derzeit angemeldeten Benutzer.) Klicken Sie auf **OK**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6.  Nachdem Sie die Bind-Operation abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie auf **ändern**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7.  In der **ändern** lassen Sie im Dialogfeld die **DN** Feld leer. In der **Attributeingabe bearbeiten** geben **FixUpInheritance**, und in der **Werte** geben **Ja**. Klicken Sie auf **EINGABETASTE** zum Auffüllen der **Eingabeliste** wie im folgenden Screenshot dargestellt.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8.  Gefüllte ändern im Dialogfeld klicken Sie auf Ausführen, und stellen Sie sicher, dass die Änderungen an das AdminSDHolder-Objekt für dieses Objekt angezeigt wurden.  

> [!NOTE]  
> Informationen zum Ändern von AdminSDHolder um festgelegte nicht privilegierten Konten zum Ändern der Mitgliedschaft geschützter Gruppen zu ermöglichen, finden Sie unter [Anhang I: Erstellen von Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  

Wenn Sie SDProp über LDIFDE oder ein Skript manuell ausführen möchten, können Sie einen Eintrag ändern, wie hier gezeigt erstellen:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Manuelles Ausführen von SDProp in WindowsServer 2012 oder Windows Server 2008 R2  
Sie können auch erzwingen, SDProp mithilfe von Ldp.exe oder durch Ausführen eines LDAP-Änderung Skripts ausführen. Führen Sie mithilfe von Ldp.exe SDProp führen Sie die folgenden Schritte aus, nachdem Sie das AdminSDHolder-Objekt in einer Domäne geändert haben:  

1.  Starten Sie **Ldp.exe**.  

2.  In der **"Ldp"** Dialogfeld, klicken Sie auf **Verbindung**, und klicken Sie auf **verbinden**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3.  In der **verbinden** Dialogfeld ein, geben Sie den Namen des Domänencontrollers für die Domäne, die die Rolle des PDC-Emulator (PDCE) enthält, und klicken Sie auf **OK**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4.  Stellen Sie sicher, dass Sie durch erfolgreich angeschlossen haben **Dn: (RootDSE)** im folgenden Screenshot, klicken Sie auf **Verbindung** , und klicken Sie auf **binden**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5.  In der **binden** Dialogfeld Geben Sie die Anmeldeinformationen eines Benutzerkontos mit der Berechtigung zum Ändern des RootDSE-Objekts. (Wenn Sie als dieser Benutzer angemeldet sind, können Sie auswählen **Bindung als aktuell angemeldete Benutzer**.) Klicken Sie auf **OK**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6.  Nachdem Sie die Bind-Operation abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie auf **ändern**.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7.  In der **ändern** lassen Sie im Dialogfeld die **DN** Feld leer. In der **Attributeingabe bearbeiten** geben **RunProtectAdminGroupsTask**, und in der **Werte** geben **1**. Klicken Sie auf **EINGABETASTE** zum Auffüllen der Liste der Einträge wie hier gezeigt.  

    ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8.  In der gefüllten **ändern** Dialogfeld, klicken Sie auf **ausführen**, und stellen Sie sicher, dass Sie die Änderungen an das AdminSDHolder-Objekt für dieses Objekt angezeigt wurden.  

Wenn Sie SDProp über LDIFDE oder ein Skript manuell ausführen möchten, können Sie einen Eintrag ändern, wie hier gezeigt erstellen:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
