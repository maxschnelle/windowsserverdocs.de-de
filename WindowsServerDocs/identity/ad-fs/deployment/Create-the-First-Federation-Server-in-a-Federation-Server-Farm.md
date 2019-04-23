---
ms.assetid: 5e334c4e-75a7-453c-83e8-5ab4243cc685
title: Erstellen des ersten Verbundservers in einer Verbundserverfarm
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: af0aa61f0d16d4ca567b140c95d74445d09f1cf3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879301"
---
# <a name="create-the-first-federation-server-in-a-federation-server-farm"></a>Erstellen des ersten Verbundservers in einer Verbundserverfarm

 >Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Sie können das folgende Verfahren verwenden, um den Computer einrichten, um den ersten Verbundserver in einer neuen Verbundserverfarm mithilfe der AD FS Konfigurations-Assistenten werden.  
  
Bei der Erstellung des ersten Verbundservers in einer Farm wird auch ein neuer Verbunddienst erstellt und dieser Computer als primärer Verbundserver definiert. Dies bedeutet, dass dieser Computer mit einem Lesevorgang konfiguriert wird\/Kopie der AD FS-Konfigurationsdatenbank zu schreiben. Alle anderen Verbundserver in dieser Farm müssen alle Änderungen, die auf dem primären Verbundserver für ihre Lese-erfolgen replizieren\-nur Kopien der AD FS-Konfigurationsdatenbank, die sie lokal speichern. Weitere Informationen zu diesem Replikationsprozess finden Sie unter [Die Rolle der AD FS-Konfigurationsdatenbank](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
> [!NOTE]  
> Für die einzelnen für Federated Web\-anmelden\-auf \(SSO\) -Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation . Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Zum Ausführen dieses Verfahrens müssen Sie mindestens Mitglied in der Gruppe „Domänenadministratoren“ sind oder über ein delegiertes Domänenkonto verfügen, dem Schreibzugriff auf den Programmdatenconteiner Active Directory gewährt wurde.  
  
### <a name="to-create-the-first-federation-server-in-a-federation-server-farm"></a>So erstellen Sie den ersten Verbundserver in einer Verbundserverfarm  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Konfigurations-Assistenten zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Nachdem die Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap\-in, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** auf einen link auf die **Übersicht über die** Seite oder in der **Aktionen** Bereich.  
  
    -   Navigieren Sie zu einem beliebigen Zeitpunkt nach der Setup-Assistent abgeschlossen wurde, öffnen ein Windows-Explorer, ist die **C:\\Windows\\ADFS** Ordner, und klicken Sie dann doppelt\-klicken Sie auf **FsConfigWizard.exe**.  
  
2.  Stellen Sie auf der Seite **Willkommen** sicher, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **wählen stehen\-Alone Bereitstellung oder Farmbereitstellung** auf **neuen Verbundserverfarm**, und klicken Sie dann auf **Weiter**.  
  
4.  Überprüfen Sie auf der Seite **Angeben eines Verbunddienstnamens**, ob das angezeigte **SSL-Zertifikat** korrekt ist. Falls nicht das korrekte Zertifikat angezeigt wird, wählen Sie das geeignete Zertifikat aus der Liste **SSL-Zertifikat** aus.  
  
    Dieses Zertifikat wird aus der Secure Sockets Layer generiert \(SSL\) Einstellungen für die Standardwebsite. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.  
  
    > [!NOTE]  
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Sie können diese Einschränkung umgehen, indem Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.  
  
5.  Wenn die AD FS-Datenbank, die Sie bereits ausgewählt vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Wenn diese Seite angezeigt wird, klicken Sie auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank nicht von Bedeutung ist oder sie nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
6.  Klicken Sie auf der Seite **Angeben eines Dienstkontos** auf **Durchsuchen**. Suchen Sie im Dialogfeld **Durchsuchen** nach dem Domänenkonto, das in dieser neuen Verbundserverfarm als Dienstkonto verwendet wird, und klicken Sie dann auf **OK**. Geben Sie das Kennwort für dieses Konto ein, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Finden Sie unter [manuell konfigurieren eines Dienstkontos für eine Verbundserverfarm](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md) für Weitere Informationen zum Angeben eines Dienstkontos für eine Verbundserverfarm. Jeden Verbundserver in der Verbundserverfarm muss für die Farm betriebsbereit ist dasselbe Dienstkonto angeben. Wenn das Dienstkonto, das erstellt wurde, Contoso wurde z. B.\\ADFS2SVC, muss jeder Computer, die Sie für die Verbundserver-Rolle konfigurieren und in der gleichen Farm einbezogen wird Contoso angeben\\ADFS2SVC in diesem Schritt die Konfigurations-Assistenten für die Farm betriebsbereit ist.  
  
7.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn Sie die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** um Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
8.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
    > [!IMPORTANT]  
    > Für eine sichere Bereitstellung sind die Artefaktauflösung und Antworterkennung deaktiviert, wenn Sie den Assistenten für die Konfiguration eines AD FS-Verbundservers verwenden, um eine Verbundserverfarm zu konfigurieren. Dieser Assistent konfiguriert automatisch die interne Windows-Datenbank zum Speichern von Dienstkonfigurationsdaten. Sie können jedoch versehentlich rückgängig machen, diese Änderung durch Aktivieren des Artefaktauflösung-Endpunkts mithilfe der **Endpunkte** Knoten in der AD FS-Verwaltungs-Snap\-in oder aktivieren\-ADFSEndpoint-Cmdlets in Windows PowerShell. Achten Sie sorgfältig darauf, die Standardeinstellung nicht erneut zu konfiguieren, damit dieser Endpunkt deaktiviert bleibt, wenn Sie eine Verbundserverfarm und die interne Windows-Datenbank gemeinsam verwenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Das Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

