---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: Anhang C – geschützte Konten und Gruppen in Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 70e29ad42b57cf315c7179d6eea8220ad2bfab48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834701"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: Geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: Geschützte Konten und Gruppen in Active Directory

Innerhalb von Active Directory ein Standardsatz von sehr privilegierten Konten und Gruppen gelten als geschützte Konten und Gruppen. Bei den meisten Objekten in Active Directory können delegierte Administratoren (Benutzer, die delegierte Berechtigungen zum Verwalten von Active Directory-Objekte) Berechtigungen für die Objekte, einschließlich dem Ändern von Berechtigungen, die sich selbst so ändern Sie die Mitgliedschaften ermöglichen ändern. die Gruppen, z. B.  

Geschützte Konten und Gruppen, sind Berechtigungen für die für die Objekte allerdings festgelegt und erzwungen, die über einen automatischen Prozess, der sicherstellt, dass die Berechtigungen für die Objekte bleiben konsistent, auch wenn die Objekte sind das Verzeichnis verschoben. Auch wenn jemand ein geschütztes Objekt Berechtigungen manuell geändert wird, gewährleistet dieser Prozess an, dass es sich bei Berechtigungen schnell auf ihre Standardwerte zurückgegeben werden.  

### <a name="protected-groups"></a>Geschützter Gruppen

Die folgende Tabelle enthält die geschützten Gruppen in Active Directory Domänencontroller-Betriebssystems aufgeführt.  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>Geschützte Konten und Gruppen in Active Directory nach Betriebssystem

| Windows Server 2003 RTM | Windows Server 2003 SP1+ | Windows Server 2012, <br> Windows Server 2008 R2, <br> WindowsServer 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|
|Administrator|Administrator|Administrator|Administrator|
|Administratoren|Administratoren|Administratoren|Administratoren|
|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|
|Zertifikatherausgeber|||
|Domänen-Admins|Domänen-Admins|Domänen-Admins|Domänen-Admins|
|Domänencontroller|Domänencontroller|Domänencontroller|Domänencontroller|
|Organisations-Admins|Organisations-Admins|Organisations-Admins|Organisations-Admins|
||||Organisations-Admins-Schlüssel|
||||Key-Administratoren|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|
|||Read-only-Domänencontroller|Read-only-Domänencontroller|
|Replikations-Operator|Replikations-Operator|Replikations-Operator|Replikations-Operator|
|Schema-Admins|Schema-Admins|Schema-Admins|Schema-Admins|
|Server-Operatoren|Server-Operatoren|Server-Operatoren|Server-Operatoren|

#### <a name="adminsdholder"></a>AdminSDHolder

Das AdminSDHolder-Objekt dient "Template"-Berechtigungen für geschützte Konten und Gruppen in der Domäne bereitstellen. AdminSDHolder wird automatisch als ein Objekt im Systemcontainer jeder Domäne der Active Directory erstellt. Der Pfad ist: **CN=AdminSDHolder,CN=System,DC=<domain_component>,DC=<domain_component>?.**  

Im Gegensatz zu den meisten Objekten in Active Directory-Domäne, die Gruppe "Administratoren" gehören, gehört der Gruppe "Domänenadministratoren" AdminSDHolder. Standardmäßig können EAs AdminSDHolder-Objekt für jede Domäne, ändern wie Domänen-Admins und Administratoren-Gruppen der Domäne. Darüber hinaus auch der Standardbesitzer des AdminSDHolder Domänen-Admins der Domäne ist, können Mitglieder Administratoren oder Unternehmensadministratoren Besitzer des Objekts ausführen.  

#### <a name="sdprop"></a>SDProp

SDProp ist ein Prozess, der alle 60 Minuten (standardmäßig) auf dem Domänencontroller ausgeführt wird, die der Domäne die PDC-Emulator (PDCE) enthält. SDProp vergleicht die Berechtigungen für die Domäne AdminSDHolder-Objekt mit den Berechtigungen für die geschützte Konten und Gruppen in der Domäne. Wenn die Berechtigungen für jedes geschützte Konten und Gruppen die Berechtigungen für das AdminSDHolder-Objekt nicht übereinstimmen, werden die Berechtigungen für die geschützte Konten und Gruppen zurückgesetzt, um der Domäne AdminSDHolder-Objekt übereinstimmen.  

Darüber hinaus ist die Vererbung von Berechtigungen deaktiviert zu geschützten Gruppen und Konten, was bedeutet, dass selbst wenn die Konten und Gruppen an unterschiedliche Stellen im Verzeichnis verschoben werden, auf sie nicht von ihren neuen übergeordneten Objekten Berechtigungen erben. Vererbung ist für das AdminSDHolder-Objekt deaktiviert, damit Änderungen an Berechtigungen, um den übergeordneten Objekten nicht die Berechtigungen des AdminSDHolder ändern.  

##### <a name="changing-sdprop-interval"></a>Ändern der SDProp-Intervall

In der Regel sollten Sie nicht das Intervall, in dem SDProp ausgeführt wird, mit Ausnahme von Testzwecken ändern müssen. Wenn Sie das Intervall der SDProp, auf dem PDCE für die Domäne ändern müssen verwenden Sie "regedit" zum Hinzufügen oder ändern den AdminSDProtectFrequency DWORD-Wert in HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters.  

Der Wertebereich ist in Sekunden zwischen 60 7200 (eine Minute auf zwei Stunden). Um die Änderungen umzukehren, löschen Sie AdminSDProtectFrequency-Schlüssel, der SDProp die 60-Minuten-Intervall wiederherstellen bewirken. Sie sollten in der Regel nicht dieses Intervall in Produktionsdomänen reduzieren, wie sie LSASS Verarbeitungsaufwand auf dem Domänencontroller erhöhen kann. Die Auswirkungen diese Erhöhung ist abhängig von der Anzahl von geschützten Objekten in der Domäne.  

##### <a name="running-sdprop-manually"></a>Manuelles Ausführen von SDProp

Ein besserer Ansatz für das Testen von AdminSDHolder-Änderungen ist SDProp manuell ausführen, die bewirkt, dass die Aufgabe sofort ausgeführt, jedoch wirkt sich nicht auf die geplante Ausführung. Manuelles Ausführen von SDProp ist etwas anders als für Domänencontroller unter Windows Server 2008 und frühere Versionen als auf Domänencontrollern unter Windows Server 2012 oder Windows Server 2008 R2 ist.  

Verfahren für die manuelle Ausführung SDProp unter älteren Betriebssystemen finden Sie unter [Microsoft Support-Artikel 251343](https://support.microsoft.com/kb/251343), und folgen eine schrittweise Anleitung für ältere und neuere Betriebssysteme. In beiden Fällen müssen Sie eine Verbindung herstellen, auf das RootDSE-Objekt in Active Directory und führen Sie einen Änderungsvorgang mit einem null-DN für das RootDSE-Objekt, den Namen des Vorgangs angeben, wie das Attribut zu ändern. Weitere Informationen zu den änderbaren Vorgänge für das RootDSE-Objekt, finden Sie unter [RootDSE ändern Vorgänge](https://msdn.microsoft.com/library/cc223297.aspx) auf der MSDN-Website.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Ausgeführte SDProp manuell in WindowsServer 2008 oder früher

Sie können erzwingen, dass SDProp mithilfe von Ldp.exe oder durch Ausführen eines LDAP-Änderung Skripts ausgeführt werden. Führen Sie mithilfe von Ldp.exe SDProp führen Sie die folgenden Schritte aus, nachdem Sie auf das Objekt "AdminSDHolder" in einer Domäne Änderungen vorgenommen haben:  

1. Starten Sie **Ldp.exe**.  
2. Klicken Sie auf **Verbindung** auf das Dialogfeld für die "Ldp", und klicken Sie auf **Connect**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. In der **Connect** Dialogfeld Feld, geben Sie den Namen des Domänencontrollers für die Domäne, die die Rolle des PDC-Emulator (PDCE) enthält, und klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. Stellen Sie sicher, dass Sie erfolgreich, wie durch eine Verbindung hergestellt haben **Dn: (RootDSE)**  klicken Sie im folgenden Screenshot auf **Verbindung** , und klicken Sie auf **binden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. In der **binden** Dialogfeld geben die Anmeldeinformationen eines Benutzerkontos mit der Berechtigung zum Ändern des RootDSE-Objekts. (Wenn Sie sich als dieser Benutzer angemeldet sind, können Sie auswählen **als binden** aktuell angemeldeten Benutzer.) Klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. Nachdem Sie der Bindungsvorgang abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie auf **ändern**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. In der **ändern** lassen Sie im Dialogfeld die **DN** Feld leer. In der **Attributeingabe bearbeiten** Feld **FixUpInheritance**, und klicken Sie in der **Werte** Feld **Ja**. Klicken Sie auf **EINGABETASTE** zum Auffüllen der **Eingabeliste** wie im folgenden Screenshot gezeigt.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. Aufgefüllte ändern im Dialogfeld klicken Sie auf Ausführen, und stellen Sie sicher, dass die an das AdminSDHolder-Objekt vorgenommenen Änderungen für dieses Objekt aufgetreten sind.  

> [!NOTE]  
> Informationen zum Ändern von AdminSDHolder zum angegebene nicht privilegierte Konten so ändern Sie die Mitgliedschaft in geschützten Gruppen können, finden Sie unter [Anhang I: Erstellen von Verwaltungskonten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  

Wenn Sie SDProp manuell über LDIFDE oder ein Skript ausführen möchten, können Sie einen Eintrag ändern, wie hier gezeigt erstellen:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Manuelles Ausführen von SDProp in WindowsServer 2012 oder Windows Server 2008 R2

Sie können auch SDProp auszuführende mithilfe von Ldp.exe oder durch Ausführen eines LDAP-Änderung Skripts erzwingen. Führen Sie mithilfe von Ldp.exe SDProp führen Sie die folgenden Schritte aus, nachdem Sie auf das Objekt "AdminSDHolder" in einer Domäne Änderungen vorgenommen haben:  

1. Starten Sie **Ldp.exe**.  

2. In der **"Ldp"** Dialogfeld klicken Sie auf **Verbindung**, und klicken Sie auf **Connect**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. In der **Connect** Dialogfeld Feld, geben Sie den Namen des Domänencontrollers für die Domäne, die die Rolle des PDC-Emulator (PDCE) enthält, und klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. Stellen Sie sicher, dass Sie erfolgreich, wie durch eine Verbindung hergestellt haben **Dn: (RootDSE)**  klicken Sie im folgenden Screenshot auf **Verbindung** , und klicken Sie auf **binden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. In der **binden** Dialogfeld geben die Anmeldeinformationen eines Benutzerkontos mit der Berechtigung zum Ändern des RootDSE-Objekts. (Wenn Sie sich als dieser Benutzer angemeldet sind, können Sie auswählen **Bindung als aktuell angemeldeter Benutzer**.) Klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. Nachdem Sie der Bindungsvorgang abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie auf **ändern**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. In der **ändern** lassen Sie im Dialogfeld die **DN** Feld leer. In der **Attributeingabe bearbeiten** Feld **RunProtectAdminGroupsTask**, und klicken Sie in der **Werte** Feld **1**. Klicken Sie auf **EINGABETASTE** zum Auffüllen der Eintragsliste, wie hier gezeigt.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. In die aufgefüllte **ändern** Dialogfeld klicken Sie auf **ausführen**, und stellen Sie sicher, dass Sie die Änderungen an das AdminSDHolder-Objekt für dieses Objekt aufgetreten sind.  

Wenn Sie SDProp manuell über LDIFDE oder ein Skript ausführen möchten, können Sie einen Eintrag ändern, wie hier gezeigt erstellen:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
