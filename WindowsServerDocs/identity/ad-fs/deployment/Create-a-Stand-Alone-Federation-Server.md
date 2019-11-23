---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: Erstellen eines eigenständigen Verbundservers
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3a948fadeb1cfa2ebe259a9bb659e93a85e06910
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359659"
---
# <a name="create-a-stand-alone-federation-server"></a>Erstellen eines eigenständigen Verbundservers

Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mithilfe des folgenden Verfahrens können Sie den Computer so einrichten, dass er zu einem eigenständigen\-eigenständigen Verbund Server wird. Beim Erstellen eines eigenständigen Verbund Servers mit eigen\-wird auch eine neue Verbunddienst erstellt. Sie erstellen einen Verbund Server mit dem Konfigurations-Assistenten für AD FS-Verbund Server.  
  
> [!NOTE]  
> Für den Verbund-SSO-\-Sign\-on \(SSO\) Design müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-create-a-stand-alone-federation-server"></a>So erstellen Sie einen eigenständigen\-Verbund Server  
  
1.  Es gibt zwei Möglichkeiten, den Assistenten für die Konfiguration des AD FS-Verbund Servers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Öffnen Sie nach Abschluss der Installation des Verbunddienst Rollen Dienstanbieter das\-Snap-in AD FS Verwaltung, und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link Konfigurations-Assistent für AD FS-Verbund **Server** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C:\\Windows\\ADFS** , und Doppel\-klicken Sie dann auf **fsconfigwizard. exe**.  
  
2.  Stellen Sie auf der Seite **Willkommen** sicher, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **\-eigenständige oder Farm Bereitstellung auswählen** auf **eigenständiger\-Verbund Server**, und klicken Sie dann auf **weiter**.  
  
    > [!IMPORTANT]  
    > Wenn Sie im Assistenten für die AD FS-Verbund Serverkonfiguration die Option\-eigenständiger Verbund Server auswählen, wird das diesem Verbunddienst zugeordnete Dienst Konto automatisch dem Netzwerkdienst Konto zugewiesen. Die Verwendung des Netzwerk Dienstanbieter als Dienst Konto wird nur in Situationen empfohlen, in denen Sie AD FS in einer Testumgebung auswerten. Wenn Sie die Option eigenständiger Verbund Server verwenden möchten, um einen Verbund Server in einer Produktionsumgebung bereitzustellen, ist es wichtig, dass Sie dieses Dienst Konto in ein geeignetere Dienst Konto ändern, das für die bereit\-Stellung von Anforderungen für diese neue Verbunddienst reserviert werden kann. Wenn Sie das Dienst Konto in ein anderes Konto als den Netzwerkdienst ändern, werden mögliche Angriffsvektoren verringert, die andernfalls den Verbund Server anfällig für böswillige Angriffe machen würden.  
  
4.  Überprüfen Sie auf der Seite **Angeben eines Verbunddienstnamens**, ob das angezeigte **SSL-Zertifikat** korrekt ist. Wenn dies nicht der gibt, wählen Sie das entsprechende Zertifikat aus der Liste **SSL-Zertifikat** aus.  
  
    Dieses Zertifikat wird aus den Secure Sockets Layer \(SSL-\)-Einstellungen für die Standard Website generiert. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.  
  
    > [!NOTE]  
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.  
  
5.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. Klicken Sie in diesem Fall auf **Datenbank löschen** und dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS Datenbank nicht wichtig sind oder nicht in einer Produktions-Verbund Serverfarm verwendet werden.  
  
6.  Überprüfen Sie die Details auf der Seite **Bereit zum Anwenden der Einstellungen**. Wenn die Einstellungen korrekt zu sein scheinen, klicken Sie auf **weiter** , um mit dem Konfigurieren von AD FS mit diesen Einstellungen zu beginnen.  
  
7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  

