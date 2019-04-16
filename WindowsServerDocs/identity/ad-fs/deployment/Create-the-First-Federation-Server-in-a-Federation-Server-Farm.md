---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: Erstellen des ersten Verbundservers in einer Verbundserverfarm
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: af0aa61f0d16d4ca567b140c95d74445d09f1cf3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>Erstellen des ersten Verbundservers in einer Verbundserverfarm

 >Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Das folgende Verfahren können zum Einrichten des ersten Verbundservers in einer neuen Verbundserverfarm mit AD FS Federation Server-Konfigurations-Assistenten werden.  
  
Der Vorgang der Erstellung des ersten Verbundservers in einer Farm auch ein neuer Verbunddienst erstellt und macht diese Computer des primären Verbundservers. Dies bedeutet, dass dieser Computer mit einer Lese-/Schreibkopie der AD FS-Konfigurationsdatenbank konfiguriert wird. Alle anderen Verbundserver in dieser Farm müssen die Änderungen replizieren, die auf dem primären Verbundserver zu ihren schreibgeschützte Kopien der AD FS-Konfigurationsdatenbank vorgenommen werden, die sie lokal zu speichern. Weitere Informationen zu diesem Replikationsprozess finden Sie unter [die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
> [!NOTE]  
> Für den Federated-Web-Single\-Sign\-On \(SSO\)-Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation. Weitere Informationen finden Sie unter [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx).  
  
Mitglied der Gruppe Domänen-Admins oder ein delegiertes Domänenkonto verfügen, der Schreibzugriff auf die Daten des Programmdatencontainer in Active Directory gewährt wurde, ist mindestens erforderlich, um dieses Verfahren ausführen.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>Erstellen des ersten Verbundservers in einer Verbundserverfarm  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Federation Server-Konfigurations-Assistenten zu starten. Um den Assistenten zu starten, führen Sie eine der folgenden:  
  
    -   Nach der Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap-In, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** link der **Übersicht** Seite oder in der **Aktionen** Bereich.  
  
    -   Navigieren Sie zu einem beliebigen Zeitpunkt nach dem Setup-Assistenten Windows Explorer öffnen, wird die **C:\\Windows\\ADFS** Ordner, und klicken Sie dann Variablenname klicken **FsConfigWizard.exe**.  
  
2.  Auf der **Willkommen** überprüfen Sie, ob Seite **Erstellen eines neuen Verbunddiensts** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **wählen Sie eigenständige Bereitstellung oder Farmbereitstellung** auf **neue Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **angeben eines Verbunddienstnamens** Seite, überprüfen Sie, ob die **SSL-Zertifikat** richtig angezeigt wird. Wenn dies nicht das richtige Zertifikat ist, wählen Sie das entsprechende Zertifikat aus der **SSL-Zertifikat** Liste.  
  
    Dieses Zertifikat wird von den Secure Sockets Layer \(SSL\) Einstellungen für die Standardwebsite generiert. Wenn die Standardwebsite nur ein SSL-Zertifikat konfiguriert wurde, ist dieses Zertifikat angezeigt und automatisch ausgewählt, für die Verwendung. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wenn keine SSL-Einstellungen für die Standardwebsite konfiguriert vorhanden sind, wird die Liste der Zertifikate generiert, die in den persönlichen Zertifikatspeicher auf dem lokalen Computer verfügbar sind.  
  
    > [!NOTE]  
    > Der Assistent können nicht Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Dadurch wird sichergestellt, dass alle vorgesehen, dass frühere IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder neu manuell mit der IIS-Verwaltungskonsole konfigurieren.  
  
5.  Wenn die AD FS-Konfigurationsdatenbank, die Sie ausgewählt haben bereits vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Wenn diese Seite angezeigt wird, klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Konfigurationsdatenbank nicht wichtig ist oder diese nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
6.  Auf der **angeben eines Dienstkontos** auf **Durchsuchen**. In der **Durchsuchen** Dialogfeld Suchen das Domänenkonto, das als Dienstkonto in dieser neuen Verbundserverfarm verwendet werden, und klicken Sie dann auf **OK**. Geben Sie das Kennwort für dieses Konto, bestätigen Sie es, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Weitere Informationen finden Sie unter [manuell konfigurieren eines Dienstkontos für eine Verbundserverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) für Weitere Informationen zum Angeben eines Dienstkontos für eine Verbundserverfarm. Jeder Verbundserver in der Verbundserverfarm muss für die Farm betriebsbereit ist das gleiche Dienstkonto angeben. Wenn beispielsweise das Dienstkonto, das erstellt wurde contoso\\ADFS2SVC war, muss jedem Computer, den Sie für die Verbundserver-Rolle konfigurieren und in derselben Farm einbezogen wird contoso\\ADFS2SVC an dieser Stelle in der Konfigurations-Assistenten für die Farm betriebsbereit ist angeben.  
  
7.  Auf der **bereit zum Anwenden der Einstellungen** Seite, überprüfen Sie die Detail. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** zum Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
8.  Auf der **Konfigurationsergebnisse** Seite, überprüfen Sie die Ergebnisse. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
    > [!IMPORTANT]  
    > Sichere Bereitstellung z.B. Artefakt und Erkennung werden deaktiviert, wenn Sie AD FS Federation Server-Konfigurations-Assistenten verwenden, um eine Verbundserverfarm zu konfigurieren. Dieser Assistent konfiguriert automatisch die interne Windows-Datenbank zum Speichern von Dienstkonfigurationsdaten. Sie können jedoch fälschlicherweise rückgängig machen diese Änderung durch aktivieren den Artefaktauflösungsendpunkt entweder mithilfe der **Endpunkte** Knoten in AD FS-Verwaltungs-Snap-In oder das Cmdlet "Enable-ADFSEndpoint" in Windows PowerShell. Achten Sie darauf, dass Sie die Standardeinstellung nicht neu zu konfigurieren, damit dieser Endpunkt deaktiviert bleibt, wenn Sie eine Verbundserverfarm und die interne Windows-Datenbank gemeinsam verwenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

