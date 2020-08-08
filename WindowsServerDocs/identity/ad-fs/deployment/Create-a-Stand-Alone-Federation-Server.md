---
ms.assetid: ab97948a-c434-48f2-8313-c1a7a518e5f7
title: Erstellen eines eigenständigen Verbundservers
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 498b2f1c87181ee2675bf7a312c73ba90d0b0421
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962964"
---
# <a name="create-a-stand-alone-federation-server"></a>Erstellen eines eigenständigen Verbundservers

Nachdem Sie den Verbunddienst-Rollen Dienst installiert und die erforderlichen Zertifikate auf einem Computer konfiguriert haben, können Sie den Computer als Verbund Server konfigurieren. Mit dem folgenden Verfahren können Sie den Computer als eigen \- ständigen Verbund Server einrichten. Beim Erstellen eines eigenständigen Verbund \- Servers wird auch eine neue Verbunddienst erstellt. Sie erstellen einen Verbund Server mit dem Konfigurations-Assistenten für AD FS-Verbund Server.

> [!NOTE]
> Für den Verbund \- \- \( -SSO-Entwurf für einmaliges Anmelden (SSO) \) müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807127(v=ws.11)).

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.Microsoft.com \/ swlink \/ ? LinkId \= 83477 \) .

### <a name="to-create-a-stand-alone-federation-server"></a>So erstellen Sie einen eigen \- ständigen Verbund Server

1.  Es gibt zwei Möglichkeiten, den AD FS-Assistenten für die Konfiguration des Verbundservers zu starten. Führen Sie zum Starten des Assistenten eine der folgenden Aktionen aus:

    -   Nachdem der Verbunddienst-Rollen Dienst installiert ist, öffnen Sie das Snap-in AD FS Verwaltung, \- und klicken Sie auf der Seite **Übersicht** oder im Bereich **Aktionen** auf den Link AD FS Verbund Server- **Konfigurations-Assistent** .

    -   Öffnen Sie nach Abschluss des Setup-Assistenten Windows-Explorer, navigieren Sie zum Ordner **C: \\ Windows \\ ADFS** , und doppelklicken Sie dann auf \- **FsConfigWizard.exe**.

2.  Vergewissern Sie sich auf der **Willkommen**-Seite, dass **Neuen Verbunddienst erstellen** ausgewählt ist, und klicken Sie dann auf **Weiter**.

3.  Klicken Sie auf der Seite **eigen \- ständige oder Farm Bereitstellung auswählen** auf **eigen \- ständiger Verbund Server**, und klicken Sie dann auf **weiter**.

    > [!IMPORTANT]
    > Wenn Sie \- im Assistenten zum Konfigurieren von AD FS Verbund Server die Option eigenständiger Verbund Server auswählen, wird das diesem Verbunddienst zugeordnete Dienst Konto automatisch dem Netzwerkdienst Konto zugewiesen. Die Verwendung des Netzwerk Dienstanbieter als Dienst Konto wird nur in Situationen empfohlen, in denen Sie AD FS in einer Testumgebung auswerten. Wenn Sie die Option eigenständiger Verbund \- Server verwenden möchten, um einen Verbund Server in einer Produktionsumgebung bereitzustellen, ist es wichtig, dass Sie dieses Dienst Konto in ein geeignetere Dienst Konto ändern, das für die Bereitstellung von Anforderungen für diese neue Verbunddienst reserviert werden kann. Wenn Sie das Dienst Konto in ein anderes Konto als den Netzwerkdienst ändern, werden mögliche Angriffsvektoren verringert, die andernfalls den Verbund Server anfällig für böswillige Angriffe machen würden.

4.  Vergewissern Sie sich auf der Seite **Name des Verbunddiensts angeben**, dass das angezeigte **SSL-Zertifikat** richtig ist. Wenn dies nicht der gibt, wählen Sie das entsprechende Zertifikat aus der Liste **SSL-Zertifikat** aus.

    Dieses Zertifikat wird aus den Secure Sockets Layer \( SSL- \) Einstellungen für die Standard Website generiert. Wenn für die Standardwebsite nur ein SSL-Zertifikat konfiguriert ist, wird dieses Zertifikat angezeigt und automatisch zur Verwendung ausgewählt. Wenn mehrere SSL-Zertifikate für die Standardwebsite konfiguriert sind, werden alle diese Zertifikate hier aufgelistet, und Sie müssen eins daraus auswählen. Wemm für die Standardwebsite keine SSL-Einstellungen konfiguriert sind, wird die Liste aus den Zertifikaten generiert, die im persönlichen Zertifikatspeicher auf dem lokalen Computer vorhanden sind.

    > [!NOTE]
    > Der Assistent lässt nicht zu, dass Sie das Zertifikat außer Kraft setzen, wenn für IIS ein SSL-Zertifikat konfiguriert ist. Damit wird sichergestellt, dass eine frühere vorgesehene IIS-Konfiguration für SSL-Zertifikate beibehalten wird. Um diese Einschränkung zu umgehen, können Sie das Zertifikat entfernen oder manuell mit der IIS-Verwaltungskonsole neu konfigurieren.

5.  Wenn die AD FS Datenbank, die Sie ausgewählt haben, bereits vorhanden ist, wird die Seite **vorhandene AD FS Konfigurations Datenbank erkannt** angezeigt. In diesem Fall klicken Sie auf **Datenbank löschen**, und klicken Sie dann auf **Weiter**.

    > [!CAUTION]
    > Wählen Sie diese Option nur aus, wenn Sie sicher sind, dass die Daten in dieser AD FS-Datenbank unwichtig sind bzw. nicht in einer Produktions-Verbundserverfarm verwendet werden.

6.  Überprüfen Sie auf der Seite **Bereit zum Übernehmen der Einstellungen** die Details. Wenn die Einstellungen richtig sind, klicken Sie auf **Weiter**, um AD FS mit diesen Einstellungen zu konfigurieren.

7.  Überprüfen Sie die Ergebnisse auf der Seite **Konfigurationsergebnisse**. Wenn alle Konfigurationsschritte abgeschlossen sind, klicken Sie auf **Schließen** , um den Assistenten zu beenden.

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)

