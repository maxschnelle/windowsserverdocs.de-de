---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: Erstellen eines eigenständigen Verbundservers
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4b70b0b048f66f9a8ba19cd7990dde57e0655ae4
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192232"
---
# <a name="create-a-stand-alone-federation-server"></a>Erstellen eines eigenständigen Verbundservers

Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Sie können das folgende Verfahren verwenden, auf den Computer einrichten, um einen eigenständigen werden\-allein Verbundserver. Erstellen Sie einen eigenständigen\-allein Verbundserver auch ein neuer Verbunddienst erstellt. Sie erstellen einen Verbundserver mit der AD FS Konfigurations-Assistenten.  
  
> [!NOTE]  
> Für die einzelnen für Federated Web\-anmelden\-auf \(SSO\) -Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation . Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
### <a name="to-create-a-stand-alone-federation-server"></a>Erstellen Sie einen eigenständigen\-allein Verbundserver  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Konfigurations-Assistenten zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Nachdem die Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap\-in, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** auf einen link auf die **Übersicht über die** Seite oder in der **Aktionen** Bereich.  
  
    -   Jederzeit nach der Setup-Assistent abgeschlossen wurde, öffnen ein Windows-Explorer ist, navigieren Sie zu der **C:\\Windows\\ADFS** Ordner, und klicken Sie dann Double\-klicken Sie auf **FsConfigWizard.exe**.  
  
2.  Stellen Sie auf der Seite **Willkommen** sicher, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **wählen stehen\-Alone Bereitstellung oder Farmbereitstellung** auf **stehen\-allein Verbundserver**, und klicken Sie dann auf **Weiter**.  
  
    > [!IMPORTANT]  
    > Bei Auswahl der eigenständigen\-allein Federation Server-Option in der AD FS Konfigurations-Assistenten, das diesem Verbunddienst zugeordnete Dienstkonto automatisch zugewiesen, das Netzwerkdienstkonto. Mithilfe des NETZWERKDIENSTES als das Dienstkonto wird nur in Situationen empfohlen, in dem Sie AD FS in einer testumgebung auswerten. Wenn Sie beabsichtigen, mit dem eigenständigen\-allein Federation Server eine Option zum Bereitstellen eines Verbundservers in einer produktionsumgebung, es ist wichtig, dass Sie dieses Dienstkonto ein geeigneter Dienstkonto ändern, die Bereitstellung verwendet werden können Anforderungen für diesen neuen Verbunddienst. Ändern das Dienstkonto in ein anderes Konto als Netzwerkdienst werden mögliche Angriffsvektoren verringern, die andernfalls dem Verbundserver anfällig für Angriffe machen würden.  
  
4.  Überprüfen Sie auf der Seite **Angeben eines Verbunddienstnamens**, ob das angezeigte **SSL-Zertifikat** korrekt ist. Falls nicht, wählen Sie das entsprechende Zertifikat aus der **SSL-Zertifikat** Liste.  
  
    Dieses Zertifikat wird aus der Secure Sockets Layer generiert \(SSL\) Einstellungen für die Standardwebsite. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.  
  
    > [!NOTE]  
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder manuell konfigurieren Sie es erneut mit der IIS-Verwaltungskonsole.  
  
5.  Wenn die AD FS-Datenbank, die Sie bereits ausgewählt vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Klicken Sie in diesem Fall auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank nicht von Bedeutung ist oder sie nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
6.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn Sie die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** um Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

