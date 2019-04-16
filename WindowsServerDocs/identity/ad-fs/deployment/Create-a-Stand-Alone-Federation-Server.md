---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: "Erstellen eines eigenständigen Verbundservers"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fd075c5b7d1bfce89cc27c4917a016e7e5037ce5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-stand-alone-federation-server"></a>Erstellen eines eigenständigen Verbundservers

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Nachdem Sie den Verbunddienst-Rollendienst installieren und konfigurieren die erforderlichen Zertifikate auf einem Computer, können Sie den Computer als Verbundserver konfigurieren. Das folgende Verfahren können den Computer einrichten, um eine eigenständige Verbundserver. Erstellen Sie einen eigenständige Verbundserver wird auch ein neuer Verbunddienst erstellt. Sie einen Verbundserver mit AD FS Federation Server-Konfigurations-Assistenten erstellen.  
  
> [!NOTE]  
> Für den Federated-Web-Single\-Sign\-On \(SSO\)-Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation. Weitere Informationen finden Sie unter [Where to Place a Federation Server](https://technet.microsoft.com/library/dd807127.aspx).  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-create-a-stand-alone-federation-server"></a>Erstellen Sie einen eigenständige Verbundserver  
  
1.  Es gibt zwei Möglichkeiten, die AD FS Federation Server-Konfigurations-Assistenten zu starten. Um den Assistenten zu starten, führen Sie eine der folgenden:  
  
    -   Nach der Installation des Verbunddienst-Rollendiensts abgeschlossen ist, öffnen Sie die AD FS-Verwaltungs-Snap-In, und klicken Sie auf die **AD FS-Verbundserverkonfigurations-Assistenten** link der **Übersicht** Seite oder in der **Aktionen** Bereich.  
  
    -   Jederzeit nach Abschluss des Setup-Assistenten öffnen Windows Explorer, navigieren Sie zu der **C:\\Windows\\ADFS** Ordner, und klicken Sie dann Variablenname klicken **FsConfigWizard.exe**.  
  
2.  Auf der **Willkommen** überprüfen Sie, ob Seite **Erstellen eines neuen Verbunddiensts** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **wählen Sie eigenständige Bereitstellung oder Farmbereitstellung** auf **eigenständige Verbundserver**, und klicken Sie dann auf **Weiter**.  
  
    > [!IMPORTANT]  
    > Wenn Sie die Option für eigenständige Federation Server in AD FS Federation Server-Konfigurations-Assistenten auswählen, wird das diesem Verbunddienst zugeordnete Dienstkonto automatisch das Netzwerkdienstkonto zugewiesen werden. Netzwerkdienst als Dienstkonto verwenden wird nur in Situationen empfohlen, in dem Sie AD FS in einer Testumgebung bewerten. Wenn Sie die eigenständige Option für die Verbundserverproxy-Server zum Bereitstellen eines Verbundservers in einer Produktionsumgebung verwenden möchten, ist es wichtig, dass Sie dieses Dienstkonto ein angemessener Dienstkonto ändern, die für die Bereitstellung von Anforderungen für diese neuen Verbunddienst festgelegt werden kann. Ändern des Dienstkontos in ein anderes Konto als Netzwerkdienst werden mögliche Angriffsvektoren verringern, die andernfalls den Verbundserver anfällig für böswillige Angriffe machen würden.  
  
4.  Auf der **angeben eines Verbunddienstnamens** Seite, überprüfen Sie, ob die **SSL-Zertifikat** richtig angezeigt wird. Falls nicht, wählen Sie das entsprechende Zertifikat aus der **SSL-Zertifikat** Liste.  
  
    Dieses Zertifikat wird von den Secure Sockets Layer \(SSL\) Einstellungen für die Standardwebsite generiert. Wenn die Standardwebsite nur ein SSL-Zertifikat konfiguriert wurde, ist dieses Zertifikat angezeigt und automatisch ausgewählt, für die Verwendung. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wenn keine SSL-Einstellungen für die Standardwebsite konfiguriert vorhanden sind, wird die Liste der Zertifikate generiert, die in den persönlichen Zertifikatspeicher auf dem lokalen Computer verfügbar sind.  
  
    > [!NOTE]  
    > Der Assistent können nicht Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Dadurch wird sichergestellt, dass alle vorgesehen, dass frühere IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder neu konfigurieren manuell mit der IIS-Verwaltungskonsole.  
  
5.  Wenn die AD FS-Konfigurationsdatenbank, die Sie ausgewählt haben bereits vorhanden ist, die **vorhandene AD FS-Konfigurationsdatenbank gefunden** Seite wird angezeigt. Klicken Sie in diesem Fall **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur, wenn Sie sicher sind, dass die Daten in dieser AD FS-Konfigurationsdatenbank nicht wichtig ist oder diese nicht in einer Produktions-Verbundserverfarm verwendet wird.  
  
6.  Auf der **bereit zum Anwenden der Einstellungen** Seite, überprüfen Sie die Detail. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **Weiter** zum Konfigurieren von AD FS mit diesen Einstellungen zu starten.  
  
7.  Auf der **Konfigurationsergebnisse** Seite, überprüfen Sie die Ergebnisse. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **schließen** um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  

