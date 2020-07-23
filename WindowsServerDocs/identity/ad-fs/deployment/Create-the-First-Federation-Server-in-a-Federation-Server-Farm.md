---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: Erstellen des ersten Verbundservers in einer Verbundserverfarm
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2ed7302a0712c50837d985c6d55ec133ffdcd5fa
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965982"
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>Erstellen des ersten Verbundservers in einer Verbundserverfarm

Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mithilfe des folgenden Verfahrens können Sie den Computer so einrichten, dass er der erste Verbund Server in einer neuen Verbund Serverfarm wird, indem Sie den Konfigurations-Assistenten für den AD FS-Verbund Server verwenden.  
  
Bei der Erstellung des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt und dieser Computer als primärer Verbundserver definiert. Dies bedeutet, dass dieser Computer mit einer Lese- \/ /Schreibkopie der AD FS Konfigurations Datenbank konfiguriert wird. Alle anderen Verbund Server in dieser Farm müssen alle am primären Verbund Server vorgenommenen Änderungen auf Ihre schreibgeschützten Kopien der \- AD FS Konfigurations Datenbank replizieren, die Sie lokal speichern. Weitere Informationen zu diesem Replikationsprozess finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
> [!NOTE]  
> Für den Verbund \- \- \( -SSO-Entwurf für einmaliges Anmelden (SSO) \) müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807127(v=ws.11)).  
  
Zum Ausführen dieses Verfahrens müssen Sie mindestens Mitglied in der Gruppe „Domänenadministratoren“ sind oder über ein delegiertes Domänenkonto verfügen, dem Schreibzugriff auf den Programmdatenconteiner Active Directory gewährt wurde.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>So erstellen Sie den ersten Verbundserver in einer Verbundserverfarm  
  
1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Nachdem der Verbunddienst-Rollen Dienst installiert ist, öffnen Sie das Snap-in AD FS Verwaltung, \- und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link AD FS Verbund Server- **Konfigurations-Assistent** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten den Windows-Explorer, navigieren Sie zum Ordner **C: \\ Windows \\ ADFS** , und doppelklicken Sie dann auf \- **FsConfigWizard.exe**.  
  
2.  Vergewissern Sie sich auf der **Willkommen**-Seite, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **eigen \- ständige oder Farm Bereitstellung auswählen** auf **neue Verbund Server Farm**, und klicken Sie dann auf **weiter**.  
  
4.  Vergewissern Sie sich auf der Seite **Name des Verbunddiensts angeben**, dass das angezeigte **SSL-Zertifikat** richtig ist. Ist dieses Zertifikat nicht das richtige Zertifikat, wählen Sie das entsprechende Zertifikat in der Liste **SSL-Zertifikat** aus.  
  
    Dieses Zertifikat wird aus den Secure Sockets Layer \( SSL- \) Einstellungen für die Standard Website generiert. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.  
  
    > [!NOTE]  
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Sie können diese Einschränkung umgehen, indem Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.  
  
5.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. Wenn diese Seite angezeigt wird, klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank unwichtig sind bzw. nicht in einer Produktions-Verbundserverfarm verwendet werden.  
  
6.  Klicken Sie auf der Seite **Dienstkonto angeben** auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** nach dem Domänenkonto, das in dieser neuer Verbundserverfarm als Dienstkonto verwendet werden soll, und klicken Sie dann auf **OK**. Geben Sie das Kennwort für dieses Konto ein, bestätigen Sie es, und klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienst Kontos für eine Verbund Serverfarm finden Sie unter [Manuelles Konfigurieren eines Dienst Kontos für eine Verbund Serverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) . Jeder Verbund Server in der Verbund Serverfarm muss das gleiche Dienst Konto angeben, damit die Farm betriebsbereit ist. Wenn beispielsweise das erstellte Dienst Konto " \\ ADFS2SVC" lautet, muss für jeden Computer, den Sie für die Verbund Server Rolle konfigurieren und der Teil derselben Farm sein wird, in diesem Schritt im Assistenten für die Konfiguration des Verbund Servers die Angabe von "" angegeben werden, damit \\ die Farm betriebsbereit ist.  
  
7.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um AD FS mit diesen Einstellungen zu konfigurieren.  
  
8.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
    > [!IMPORTANT]  
    > Für eine sichere Bereitstellung sind die Artefaktauflösung und Antworterkennung deaktiviert, wenn Sie den Assistenten für die Konfiguration eines AD FS-Verbundservers verwenden, um eine Verbundserverfarm zu konfigurieren. Dieser Assistent konfiguriert automatisch die interne Windows-Datenbank zum Speichern von Dienstkonfigurationsdaten. Sie können diese Änderung jedoch versehentlich rückgängig machen, indem Sie den artefaktauflösungs-Endpunkt entweder über den Knoten **Endpunkte** im Snap-in "AD FS-Verwaltung" \- oder über das \- Cmdlet "adosendpoint" in Windows PowerShell aktivieren. Achten Sie sorgfältig darauf, die Standardeinstellung nicht erneut zu konfiguieren, damit dieser Endpunkt deaktiviert bleibt, wenn Sie eine Verbundserverfarm und die interne Windows-Datenbank gemeinsam verwenden.  
  
## <a name="additional-references"></a>Zusätzliche Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
