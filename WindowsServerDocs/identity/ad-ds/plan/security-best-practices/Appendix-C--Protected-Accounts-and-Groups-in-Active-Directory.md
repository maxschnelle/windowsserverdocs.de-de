---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: 'Anhang C: geschützte Konten und Gruppen in Active Directory'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3036176127cbb5401c582d81ddb2704d790a209a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821683"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: Geschützte Konten und Gruppen in Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>Anhang C: Geschützte Konten und Gruppen in Active Directory

Innerhalb Active Directory werden ein Standardsatz von Konten und Gruppen mit hohen Berechtigungen als geschützte Konten und Gruppen angesehen. Bei den meisten Objekten in Active Directory können Delegierte Administratoren (Benutzer, die Berechtigungen zum Verwalten von Active Directory Objekten delegiert haben) die Berechtigungen für die Objekte ändern, einschließlich der Änderung von Berechtigungen, um die Gruppenmitgliedschaften zu ändern, z. b.  

Bei geschützten Konten und Gruppen werden die Berechtigungen der Objekte jedoch über einen automatischen Prozess festgelegt und erzwungen, der sicherstellt, dass die Berechtigungen für die Objekte konsistent bleiben, auch wenn die Objekte das Verzeichnis verschieben. Auch wenn jemand die Berechtigungen eines geschützten Objekts manuell ändert, stellt dieser Vorgang sicher, dass die Berechtigungen schnell auf ihre Standardwerte zurückgegeben werden.  

### <a name="protected-groups"></a>Geschützte Gruppen

In der folgenden Tabelle sind die geschützten Gruppen in Active Directory aufgeführt, die nach Domänen Controller-Betriebssystem aufgeführt sind.  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>Geschützte Konten und Gruppen in Active Directory nach Betriebs System

| Windows Server 2003 RTM | Windows Server 2003 SP1 und höher | Windows Server 2012, <br> Windows Server 2008 R2, <br> WindowsServer 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|
|Administrator|Administrator|Administrator|Administrator|
|Administratoren|Administratoren|Administratoren|Administratoren|
|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|
|Zertifikatherausgeber|||
|Domänen-Admins|Domänen-Admins|Domänen-Admins|Domänen-Admins|
|Domänencontroller|Domänencontroller|Domänencontroller|Domänencontroller|
|Organisations-Admins|Organisations-Admins|Organisations-Admins|Organisations-Admins|
||||Enterprise Key-Administratoren|
||||Haupt Administratoren|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|
|||Read-only-Domänencontroller|Read-only-Domänencontroller|
|Replikations-Operator|Replikations-Operator|Replikations-Operator|Replikations-Operator|
|Schema-Admins|Schema-Admins|Schema-Admins|Schema-Admins|
|Server-Operatoren|Server-Operatoren|Server-Operatoren|Server-Operatoren|

#### <a name="adminsdholder"></a>AdminSDHolder

Das AdminSDHolder-Objekt dient zum Bereitstellen von "Template"-Berechtigungen für die geschützten Konten und Gruppen in der Domäne. "AdminSDHolder" wird automatisch als Objekt im System Container jeder Active Directory Domäne erstellt. Der Pfad lautet: **CN = AdminSDHolder, CN = System, DC = < domain_component >, DC = < domain_component >?.**  

Im Gegensatz zu den meisten Objekten in der Active Directory Domäne, die sich im Besitz der Gruppe "Administratoren" befinden, gehört "AdminSDHolder" der Gruppe "Domänen-Admins". Standardmäßig kann EAS Änderungen an den AdminSDHolder-Objekten beliebiger Domänen vornehmen, wie die Domänen-Admins und Administratoren der Domäne. Obwohl der Standard Besitzer von AdminSDHolder die Gruppe der Domänen-Admins der Domäne ist, können Mitglieder von Administratoren oder Organisations Administratoren den Besitz des Objekts übernehmen.  

#### <a name="sdprop"></a>SDPROP

SDPROP ist ein Prozess, der auf dem Domänen Controller, der den PDC-Emulator (PDCE) der Domäne enthält, alle 60 Minuten (standardmäßig) ausgeführt wird. SDPROP vergleicht die Berechtigungen für das AdminSDHolder-Objekt der Domäne mit den Berechtigungen für die geschützten Konten und Gruppen in der Domäne. Wenn die Berechtigungen für eines der geschützten Konten und Gruppen nicht mit den Berechtigungen für das AdminSDHolder-Objekt übereinstimmen, werden die Berechtigungen für die geschützten Konten und Gruppen so zurückgesetzt, dass Sie mit denen des AdminSDHolder-Objekts der Domäne übereinstimmen.  

Außerdem wird die Vererbung von Berechtigungen für geschützte Gruppen und Konten deaktiviert. Dies bedeutet, dass selbst dann, wenn die Konten und Gruppen an verschiedene Speicherorte im Verzeichnis verschoben werden, keine Berechtigungen von ihren neuen übergeordneten Objekten geerbt werden. Die Vererbung ist für das AdminSDHolder-Objekt deaktiviert, sodass Berechtigungs Änderungen an den übergeordneten Objekten die Berechtigungen von AdminSDHolder nicht ändern.  

##### <a name="changing-sdprop-interval"></a>Ändern des SDPROP-Intervalls

Normalerweise sollten Sie das Intervall, in dem SDPROP ausgeführt wird, nicht ändern müssen, mit Ausnahme der Testzwecke. Wenn Sie das SDPROP-Intervall ändern müssen, verwenden Sie auf der PDCE für die Domäne regedit, um den Wert von adminsdprotectfrequency DWORD in hklm\system\currentcontrolset\services\ntds\parametershinzu zufügen oder zu ändern.  

Der Wertebereich ist in Sekunden zwischen 60 und 7200 (eine Minute bis zwei Stunden). Um die Änderungen umzukehren, löschen Sie den adminsdprotectfrequency Key, der bewirkt, dass SDPROP auf das Intervall von 60 Minuten zurückgesetzt wird. Im Allgemeinen sollten Sie dieses Intervall nicht in Produktions Domänen reduzieren, da es den LSASS-Verarbeitungsaufwand auf dem Domänen Controller erhöhen kann. Welche Auswirkung diese Zunahme hat, hängt von der Anzahl der geschützten Objekte in der Domäne ab.  

##### <a name="running-sdprop-manually"></a>Manuelles Ausführen von SDPROP

Eine bessere Vorgehensweise beim Testen von AdminSDHolder-Änderungen besteht darin, SDPROP manuell auszuführen. Dies bewirkt, dass die Aufgabe sofort ausgeführt wird, die geplante Ausführung jedoch nicht beeinträchtigt wird. Die manuelle Ausführung von SDPROP erfolgt auf Domänen Controllern unter Windows Server 2008 und älter als auf Domänen Controllern unter Windows Server 2012 oder Windows Server 2008 R2.  

Prozeduren zum manuellen Ausführen von SDPROP unter älteren Betriebssystemen finden Sie in [Microsoft-Support Artikel 251343](https://support.microsoft.com/kb/251343), und im folgenden finden Sie Schritt-für-Schritt-Anleitungen für ältere und neuere Betriebssysteme. In beiden Fällen müssen Sie eine Verbindung mit dem rootDSE-Objekt in Active Directory herstellen und einen Modify-Vorgang mit einem NULL-DN für das rootDSE-Objekt ausführen, wobei der Name des Vorgangs als zu ändernde Attribut angegeben wird. Weitere Informationen zu änderbaren Vorgängen für das rootDSE-Objekt finden Sie unter [rootDSE](https://msdn.microsoft.com/library/cc223297.aspx) -Änderungs Vorgänge auf der MSDN-Website.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Manuelles Ausführen von SDPROP in Windows Server 2008 oder früher

Sie können die Ausführung von SDPROP erzwingen, indem Sie "Ldp. exe" oder ein LDAP-Änderungs Skript ausführen. Führen Sie die folgenden Schritte aus, nachdem Sie das AdminSDHolder-Objekt in einer Domäne geändert haben, um SDPROP mithilfe von "Ldp. exe" auszuführen:  

1. Starten Sie " **Ldp. exe**".  
2. Klicken Sie im Dialogfeld Ldp auf **Verbindung** , und klicken Sie auf **verbinden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. Geben Sie im Dialogfeld **verbinden** den Namen des Domänen Controllers für die Domäne ein, in der die PDC-Emulatorrolle (PDCE) enthalten ist, und klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. Vergewissern Sie sich, dass die Verbindung erfolgreich hergestellt wurde, wie von **DN: (RootDSE)** im folgenden Screenshot angegeben, klicken Sie auf **Verbindung** , und klicken Sie dann auf **binden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. Geben Sie im Dialogfeld **binden** die Anmelde Informationen eines Benutzerkontos ein, das über die Berechtigung zum Ändern des RootDSE-Objekts verfügt. (Wenn Sie als dieser Benutzer angemeldet sind, können Sie **Bind als** aktuell angemeldeter Benutzer auswählen.) Klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. Nachdem Sie den Bindungs Vorgang abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie dann auf **ändern**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. Lassen Sie im Dialogfeld **ändern** das Feld **DN** leer. Geben Sie im Feld **Eingabe Attribut bearbeiten** den Wert **fixupvererbung**ein, und geben Sie im Feld **Werte den Wert** **Ja**ein. **Drücken** Sie die EINGABETASTE, um die **Eingabeliste aufzufüllen** , wie im folgenden Screenshot gezeigt.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. Klicken Sie im Dialogfeld aufgefüllt ändern auf Ausführen, und überprüfen Sie, ob die Änderungen, die Sie am Objekt AdminSDHolder vorgenommen haben, in diesem Objekt angezeigt wurden.  

> [!NOTE]  
> Informationen zum Ändern von AdminSDHolder, sodass bestimmte nicht privilegierte Konten die Mitgliedschaft geschützter Gruppen ändern können, finden Sie [unter Anhang I: Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  

Wenn Sie SDPROP lieber manuell über LDIFDE oder ein Skript ausführen möchten, können Sie einen Änderungs Eintrag erstellen, wie hier gezeigt:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Manuelles Ausführen von SDPROP in Windows Server 2012 oder Windows Server 2008 R2

Sie können auch erzwingen, dass SDPROP mithilfe von "Ldp. exe" oder durch Ausführen eines LDAP-Änderungs Skripts ausgeführt wird. Führen Sie die folgenden Schritte aus, nachdem Sie das AdminSDHolder-Objekt in einer Domäne geändert haben, um SDPROP mithilfe von "Ldp. exe" auszuführen:  

1. Starten Sie " **Ldp. exe**".  

2. Klicken Sie im Dialogfeld **LDP** auf **Verbindung**, und klicken Sie dann auf **verbinden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. Geben Sie im Dialogfeld **verbinden** den Namen des Domänen Controllers für die Domäne ein, in der die PDC-Emulatorrolle (PDCE) enthalten ist, und klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. Vergewissern Sie sich, dass die Verbindung erfolgreich hergestellt wurde, wie von **DN: (RootDSE)** im folgenden Screenshot angegeben, klicken Sie auf **Verbindung** , und klicken Sie dann auf **binden**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. Geben Sie im Dialogfeld **binden** die Anmelde Informationen eines Benutzerkontos ein, das über die Berechtigung zum Ändern des RootDSE-Objekts verfügt. (Wenn Sie als dieser Benutzer angemeldet sind, können Sie **Bind als aktuell angemeldeter Benutzer**auswählen.) Klicken Sie auf **OK**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. Nachdem Sie den Bindungs Vorgang abgeschlossen haben, klicken Sie auf **Durchsuchen**, und klicken Sie dann auf **ändern**.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. Lassen Sie im Dialogfeld **ändern** das Feld **DN** leer. Geben Sie im Feld **Eingabe Attribut bearbeiten** den Wert **runprotectadmingroupstask**ein, und geben Sie im Feld **Werte den Wert** **1 ein**. **Drücken** Sie die EINGABETASTE, um die Eingabeliste aufzufüllen, wie hier gezeigt.  

   ![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. Klicken Sie im Dialogfeld aufgefüllt **ändern** auf **Ausführen**, und überprüfen Sie, ob die Änderungen, die Sie am Objekt AdminSDHolder vorgenommen haben, in diesem Objekt angezeigt wurden.  

Wenn Sie SDPROP lieber manuell über LDIFDE oder ein Skript ausführen möchten, können Sie einen Änderungs Eintrag erstellen, wie hier gezeigt:  

![geschützte Konten und Gruppen](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
