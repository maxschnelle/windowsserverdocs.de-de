---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: Erstellen des ersten Verbundservers in einer Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 09b577ddcf722c6eac17ea145f29f9583d1cdb00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408422"
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>Erstellen des ersten Verbundservers in einer Verbundserverfarm

Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mithilfe des folgenden Verfahrens können Sie den Computer so einrichten, dass er der erste Verbund Server in einer neuen Verbund Serverfarm wird, indem Sie den Konfigurations-Assistenten für den AD FS-Verbund Server verwenden.  
  
Bei der Erstellung des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt und dieser Computer als primärer Verbundserver definiert. Dies bedeutet, dass dieser Computer mit einer Lese-/0-Schreibkopie der AD FS Konfigurations Datenbank konfiguriert wird. Alle anderen Verbund Server in dieser Farm müssen alle Änderungen, die auf dem primären Verbund Server vorgenommen werden, auf Ihre schreibgeschützten @ no__t-0-Kopien der AD FS Konfigurations Datenbank replizieren, die lokal gespeichert werden. Weitere Informationen zu diesem Replikationsprozess finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
> [!NOTE]  
> Für den Entwurf "Federated Web Single @ no__t-0sign @ no__t-1On \(sso @ no__t-3" müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Zum Ausführen dieses Verfahrens müssen Sie mindestens Mitglied in der Gruppe „Domänenadministratoren“ sind oder über ein delegiertes Domänenkonto verfügen, dem Schreibzugriff auf den Programmdatenconteiner Active Directory gewährt wurde.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>So erstellen Sie den ersten Verbundserver in einer Verbundserverfarm  
  
1.  Es gibt zwei Möglichkeiten, den Assistenten für die Konfiguration des AD FS-Verbund Servers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Öffnen Sie nach Abschluss der Installation des Verbunddienst-Rollen Dienstanbieter das AD FS Verwaltungs-Snap @ no__t-0in, und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link **AD FS Verbund Server-Konfigurations-Assistent** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten den Windows-Explorer, navigieren Sie zum Ordner **C: \\Windows @ no__t-2adfs** , und doppelklicken Sie dann auf den Wert von @ no__t-3click **fsconfigwizard. exe**.  
  
2.  Stellen Sie auf der Seite **Willkommen** sicher, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite Wählen Sie die Option " **eigenständige @ no__t-oder Farm Bereitstellung** " aus auf **neue Verbund Server Farm**, und klicken Sie dann auf **weiter**.  
  
4.  Überprüfen Sie auf der Seite **Angeben eines Verbunddienstnamens**, ob das angezeigte **SSL-Zertifikat** korrekt ist. Falls nicht das korrekte Zertifikat angezeigt wird, wählen Sie das geeignete Zertifikat aus der Liste **SSL-Zertifikat** aus.  
  
    Dieses Zertifikat wird aus den Secure Sockets Layer \(ssl @ no__t-1-Einstellungen für die Standard Website generiert. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.  
  
    > [!NOTE]  
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Sie können diese Einschränkung umgehen, indem Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.  
  
5.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. Wenn diese Seite angezeigt wird, klicken Sie auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS Datenbank nicht wichtig sind oder nicht in einer Produktions-Verbund Serverfarm verwendet werden.  
  
6.  Klicken Sie auf der Seite **Angeben eines Dienstkontos** auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** nach dem Domänenkonto, das in dieser neuen Verbundserverfarm als Dienstkonto verwendet wird, und klicken Sie dann auf **OK**. Geben Sie das Kennwort für dieses Konto ein, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Weitere Informationen zum Angeben eines Dienst Kontos für eine Verbund Serverfarm finden Sie unter [Manuelles Konfigurieren eines Dienst Kontos für eine Verbund Serverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) . Jeder Verbund Server in der Verbund Serverfarm muss das gleiche Dienst Konto angeben, damit die Farm betriebsbereit ist. Wenn beispielsweise das erstellte Dienst Konto "%% amp; quot; no__t-0adfs2svc" lautet, muss bei diesem Schritt auf dem Verbund Server für jeden Computer, den Sie für die Verbund Server Rolle konfigurieren und der Teil derselben Farm sein soll, "c" @ no__t-1adfs2svc angegeben werden. Der Konfigurations-Assistent für die Farm ist funktionstüchtig.  
  
7.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **weiter** , um mit dem Konfigurieren von AD FS mit diesen Einstellungen zu beginnen.  
  
8.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
    > [!IMPORTANT]  
    > Für eine sichere Bereitstellung sind die Artefaktauflösung und Antworterkennung deaktiviert, wenn Sie den Assistenten für die Konfiguration eines AD FS-Verbundservers verwenden, um eine Verbundserverfarm zu konfigurieren. Dieser Assistent konfiguriert automatisch die interne Windows-Datenbank zum Speichern von Dienstkonfigurationsdaten. Sie können diese Änderung jedoch versehentlich rückgängig machen, indem Sie den artefaktauflösungs-Endpunkt entweder über den Knoten **Endpunkte** im AD FS Verwaltungs-Snap @ no__t-1In oder über das Cmdlet Enable @ no__t-2adf Point in Windows PowerShell aktivieren. Achten Sie sorgfältig darauf, die Standardeinstellung nicht erneut zu konfiguieren, damit dieser Endpunkt deaktiviert bleibt, wenn Sie eine Verbundserverfarm und die interne Windows-Datenbank gemeinsam verwenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

