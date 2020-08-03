---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: Installieren des Verbundserverproxy-Rollendiensts
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2378a0fe8f2fb9c91f41a69e7253d82532280ddd
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519989"
---
# <a name="install-the-federation-service-proxy-role-service"></a>Installieren des Verbundserverproxy-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und Zertifikaten konfiguriert haben, können Sie den Verbunddienstproxy-Rollen Dienst Active Directory-Verbunddienste (AD FS) AD FS installieren \( \) . Mit dem folgenden Verfahren können Sie den Verbunddienstproxy-Rollen Dienst installieren. Wenn Sie den Verbunddienstproxy-Rollen Dienst auf einem Computer installieren, wird dieser Computer zu einem Verbund Server Proxy.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>So installieren Sie den Verbunddienstproxy-Rollen Dienst mithilfe der Server-Manager

1.  Geben Sie auf dem **Start** Bildschirm**Server-Manager**ein, und drücken Sie dann die EINGABETASTE.

2.  Klicken Sie auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**, um den Assistent zum Hinzufügen von Rollen und Features zu starten.

3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.

4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollen \- basierte oder \- featurebasierte Installation**, und klicken Sie auf **weiter**.

5.  Klicken Sie auf der Seite **Zielserver auswählen** auf **Server aus dem Serverpool auswählen**, vergewissern Sie sich, dass der Zielcomputer ausgewählt ist, und klicken dann auf **Weiter**.

6.  Klicken Sie auf der Seite **Server Rollen auswählen** auf **Remote Zugriff**, und klicken Sie dann auf Weiter.

    > [!NOTE]
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework- oder Windows-Prozessaktivierungsdienst-Features zu installieren, klicken Sie auf **Features hinzufügen**, um sie zu installieren.

7. Aktivieren Sie auf der Seite **Rollendienste auswählen** das Kontrollkästchen **Verbunddienstproxy**, und klicken Sie dann auf **Weiter**.

8. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** geprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten**, und klicken Sie dann auf **Installieren**.

13. Überprüfen Sie auf der Seite **Installationsfortschritt**, ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>So installieren Sie den Verbunddienstproxy-Rollen Dienst mithilfe von PowerShell

1. Öffnen Sie Windows PowerShell (als Administrator ausführen).

2. Geben Sie den folgenden Befehl ein, und drücken **Sie Eingabe**:

    ```
    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools
    ```

## <a name="additional-references"></a>Zusätzliche Verweise

- [Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)

- [Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)
