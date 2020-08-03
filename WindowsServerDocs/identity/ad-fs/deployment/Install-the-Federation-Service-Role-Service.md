---
ms.assetid: e33673ff-ea1c-4476-a549-3bf5899a47dd
title: Installieren des Verbundserver-Rollendiensts
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7ed7caad187181b4ad52cf4032d6343a3353c9f7
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519979"
---
# <a name="install-the-federation-service-role-service"></a>Installieren des Verbundserver-Rollendiensts

Nachdem Sie einen Computer mit den erforderlichen Anwendungen und Zertifikaten ordnungsgemäß konfiguriert haben, können Sie den Verbunddienst-Rollen Dienst Active Directory-Verbunddienste (AD FS) (AD FS) installieren. Wenn Sie die Verbunddienst auf einem Computer installieren, wird dieser Computer zu einem Verbund Server.

> [!NOTE]
> Für den Federated-Web-SSO-Entwurf (Single Sign-on, einmaliges Anmelden) müssen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation besitzen. Weitere Informationen finden Sie unter [Platzierung eines Verbundservers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807127(v=ws.11)).

Mithilfe des folgenden Verfahrens können Sie den Verbunddienst-Rollen Dienst von AD FS auf einem Computer installieren, der als erster Verbund Server oder auf einem Computer, der als Verbund Server für eine vorhandene Verbund Serverfarm verwendet wird, verwendet werden soll.

## <a name="prerequisites"></a>Voraussetzungen
Vergewissern Sie sich, dass ein SSL-Zertifikat mit dem privaten Schlüssel bereits installiert oder in den lokalen Zertifikat Speicher (persönlicher Speicher) importiert wurde, bevor Sie mit diesem Verfahren beginnen. Wenn Sie ein Tokensignaturzertifikat verwenden, das von einer Zertifizierungsstelle (Certification Authority, ca) ausgestellt wird, überprüfen Sie, ob ein Tokensignaturzertifikat mit dem privaten Schlüssel bereits installiert oder in den lokalen Zertifikat Speicher (persönlicher Speicher) importiert wurde, bevor Sie mit diesem Verfahren beginnen. Als Alternative können Sie ein selbst signiertes Tokensignaturzertifikat mithilfe des Assistenten zum Hinzufügen von Rollen erstellen, wie in diesem Verfahren beschrieben. Weitere Informationen zu Tokensignaturzertifikaten finden Sie unter [Zertifikat Anforderungen für Verbund Server](../design/certificate-requirements-for-federation-servers.md).

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich. Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

#### <a name="to-install-the-federation-service-role-service"></a>So installieren Sie den Verbunddienst-Rollendienst

1. Geben Sie auf dem **Start** Bildschirm**Server-Manager**ein, und drücken Sie dann die EINGABETASTE.

2. Klicken Sie auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**, um den Assistent zum Hinzufügen von Rollen und Features zu starten.

3. Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.

4. Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf **Weiter**.

5. Klicken Sie auf der Seite **Zielserver auswählen** auf **Server aus dem Serverpool auswählen**, vergewissern Sie sich, dass der Zielcomputer ausgewählt ist, und klicken dann auf **Weiter**.

6. Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Verbunddienste**, und klicken Sie dann auf Weiter.

    > [!NOTE]
    > Wenn Sie aufgefordert werden, zusätzliche .NET Framework- oder Windows-Prozessaktivierungsdienst-Features zu installieren, klicken Sie auf **Features hinzufügen**, um sie zu installieren.

7. Vergewissern Sie sich auf der Seite **Features auswählen**, dass die Features festgelegt sind, und klicken Sie dann auf **Weiter**.

8. Klicken Sie auf der Seite **Active Directory-Verbunddienst (AD FS)** auf **Weiter**.

9. Aktivieren Sie auf der Seite **Rollendienste auswählen** das Kontrollkästchen **Verbunddienst**, und klicken Sie dann auf **Weiter**.

10. Klicken Sie auf der Seite **Webserverrolle (IIS)** auf **Weiter**.

11. Klicken Sie auf der Seite **Rollendienste auswählen** auf **Weiter**.

12. Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** geprüft haben, aktivieren Sie das Kontrollkästchen **Zielserver bei Bedarf automatisch neu starten**, und klicken Sie dann auf **Installieren**.

13. Überprüfen Sie auf der Seite **Installationsfortschritt**, ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.