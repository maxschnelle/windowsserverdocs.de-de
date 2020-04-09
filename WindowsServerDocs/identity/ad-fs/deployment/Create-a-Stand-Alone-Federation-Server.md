---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: Erstellen eines eigenständigen Verbundservers
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 603786d8553cce20f0b559ba8a91dfc29f760488
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855483"
---
# <a name="create-a-stand-alone-federation-server"></a>Erstellen eines eigenständigen Verbundservers

Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mithilfe des folgenden Verfahrens können Sie den Computer so einrichten, dass er zu einem eigenständigen\-eigenständigen Verbund Server wird. Beim Erstellen eines eigenständigen Verbund Servers mit eigen\-wird auch eine neue Verbunddienst erstellt. Sie erstellen einen Verbund Server mit dem Konfigurations-Assistenten für AD FS-Verbund Server.  
  
> [!NOTE]  
> Für den Verbund-SSO-\-Sign\-on \(SSO\) Design müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](https://technet.microsoft.com/library/dd807127.aspx).  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-create-a-stand-alone-federation-server"></a>So erstellen Sie einen eigenständigen\-Verbund Server  
  
1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:  
  
    -   Öffnen Sie nach Abschluss der Installation des Verbunddienst Rollen Dienstanbieter das\-Snap-in AD FS Verwaltung, und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link Konfigurations-Assistent für AD FS-Verbund **Server** .  
  
    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C:\\Windows\\ADFS** , und Doppel\-klicken Sie dann auf **fsconfigwizard. exe**.  
  
2.  Vergewissern Sie sich auf der **Willkommen**-Seite, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **\-eigenständige oder Farm Bereitstellung auswählen** auf **eigenständiger\-Verbund Server**, und klicken Sie dann auf **weiter**.  
  
    > [!IMPORTANT]  
    > Wenn Sie im Assistenten für die AD FS-Verbund Serverkonfiguration die Option\-eigenständiger Verbund Server auswählen, wird das diesem Verbunddienst zugeordnete Dienst Konto automatisch dem Netzwerkdienst Konto zugewiesen. Die Verwendung des Netzwerk Dienstanbieter als Dienst Konto wird nur in Situationen empfohlen, in denen Sie AD FS in einer Testumgebung auswerten. Wenn Sie die Option eigenständiger Verbund Server verwenden möchten, um einen Verbund Server in einer Produktionsumgebung bereitzustellen, ist es wichtig, dass Sie dieses Dienst Konto in ein geeignetere Dienst Konto ändern, das für die bereit\-Stellung von Anforderungen für diese neue Verbunddienst reserviert werden kann. Wenn Sie das Dienst Konto in ein anderes Konto als den Netzwerkdienst ändern, werden mögliche Angriffsvektoren verringert, die andernfalls den Verbund Server anfällig für böswillige Angriffe machen würden.  
  
4.  Vergewissern Sie sich auf der Seite **Name des Verbunddiensts angeben**, dass das angezeigte **SSL-Zertifikat** richtig ist. Wenn dies nicht der gibt, wählen Sie das entsprechende Zertifikat aus der Liste **SSL-Zertifikat** aus.  
  
    Dieses Zertifikat wird aus den Secure Sockets Layer \(SSL-\)-Einstellungen für die Standard Website generiert. Ist für die Standardwebsite nur ein SSL-Zertifikat konfiguriert, wird dieses Zertifikat angezeigt und automatisch zur Nutzung ausgewählt. Sind mehrere Zertifikate für die Standardwebsite konfiguriert, werden hier alle Zertifikate aufgelistet, und Sie müssen eines dieser Zertifikate auswählen. Sind keine SSL-Einstellungen für die Standardwebsite konfiguriert, wird die Liste mit den Zertifikaten generiert, die im persönlichen Zertifikatespeicher des lokalen Computers verfügbar sind.  
  
    > [!NOTE]  
    > Der Assistent lässt das Überschreiben des Zertifikats nicht zu, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine ggf. zuvor festgelegte IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.  
  
5.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. In diesem Fall klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.  
  
    > [!CAUTION]  
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank unwichtig sind bzw. nicht in einer Produktions-Verbundserverfarm verwendet werden.  
  
6.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um AD FS mit diesen Einstellungen zu konfigurieren.  
  
7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)  
  

