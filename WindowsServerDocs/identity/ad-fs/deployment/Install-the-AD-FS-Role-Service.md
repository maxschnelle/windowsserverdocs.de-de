---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: Installieren des AD FS-Rollendiensts
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 435634e7b6edfc110c7bd208d727b974804eb236
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972177"
---
# <a name="install-the-ad-fs-role-service"></a>Installieren des AD FS-Rollendiensts

Mithilfe des folgenden Verfahrens können Sie den AD FS-Rollen Dienst auf einem Computer installieren, auf dem Windows Server 2012 R2 ausgeführt wird, um als ersten Verbund Server in einer Verbund Serverfarm oder als Verbund Server in einer vorhandenen Verbund Serverfarm zu dienen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>So installieren Sie die AD FS-Serverrolle mithilfe des Assistenten zum Hinzufügen von Rollen und Features

1.  Öffnen Sie den Server-Manager. Um Server-Manager zu öffnen, klicken Sie auf der **Start** Seite auf **Server-Manager** , oder **Server-Manager** auf der Taskleiste auf dem Desktop. Klicken Sie auf der Seite **Dashboard** auf der Kachel für **Willkommen** auf der Registerkarte **Schnellstart** auf **Rollen und Features hinzufügen**. Alternativ können Sie im Menü **Verwalten** auf **Rollen und Features hinzufügen** klicken.

2.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.

3.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollen \- basierte oder \- featurebasierte Installation**, und klicken Sie dann auf **weiter**.

4.  Klicken Sie auf der Seite  **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, überprüfen Sie, ob der Zielcomputer ausgewählt ist, und klicken Sie dann auf **Weiter**.

5.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Verbunddienste**, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf der Seite **Features auswählen** auf **Weiter**. Die erforderlichen Voraussetzungen sind vorab ausgewählt. Sie müssen keine anderen Features auswählen.

7.  Klicken Sie auf der Seite **Active Directory Verbunddienst \( \) AD FS** auf **weiter**.

8.  Nachdem Sie die Informationen auf der Seite **Installationsauswahl bestätigen** überprüft haben, klicken Sie auf **Installieren**.

9. Überprüfen Sie auf der Seite **Installationsfortschritt**, ob alles ordnungsgemäß installiert wurden, und klicken Sie dann auf **Schließen**.

### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>So installieren Sie die AD FS-Serverrolle mithilfe von Windows PowerShell

1.  Öffnen Sie auf dem Computer, den Sie als Verbund Server konfigurieren möchten, das Windows PowerShell-Befehlsfenster, und führen Sie dann den folgenden Befehl aus: `Install-windowsfeature adfs-federation –IncludeManagementTools` .

## <a name="see-also"></a>Weitere Informationen

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)

[Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)


