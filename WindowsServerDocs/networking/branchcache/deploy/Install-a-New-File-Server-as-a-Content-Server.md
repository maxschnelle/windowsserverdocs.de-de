---
title: Installieren eines neuen Dateiservers als Inhaltsserver
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9808f21d971ec2a3b6610c7c0c279af00947d813
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954136"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>Installieren eines neuen Dateiservers als Inhaltsserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die Server Rolle "Dateidienste" und den Rollen Dienst " **BranchCache für Netzwerkdateien** " auf einem Computer mit Windows Server 2016 installieren.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell auszuführen, führen Sie Windows PowerShell als Administrator aus, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.
>
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`
>
> `Restart-Computer`
>
> Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Rollen Dienst "Datendeduplizierung" zu installieren.
>
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`

### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>So installieren Sie die Serverrolle „Dateidienste“ und den Rollendienst „BranchCache für Netzwerkdateien“

1.  Klicken Sie im Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie unter **Vorbemerkungen** auf **Weiter**.

2.  Vergewissern Sie sich, dass unter **Installationstyp auswählen**die Option **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **weiter**.

3.  Stellen **Sie in Zielserver auswählen**sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **weiter**.

4.  Beachten Sie, dass unter **Server Rollen auswählen**unter **Rollen**die Rolle **Datei-und Speicherdienste** bereits installiert ist. Klicken Sie auf den Pfeil links neben dem Rollennamen, um die Auswahl der Rollen Dienste zu erweitern, und klicken Sie dann auf den Pfeil links neben **Datei-und iSCSI-Dienste**.

5.  Aktivieren Sie die Kontrollkästchen für den **Datei Server** und den **BranchCache für Netzwerkdateien**.

    > [!TIP]
    > Es wird empfohlen, dass Sie auch das Kontrollkästchen für die **Datendeduplizierung**aktivieren.

    Klicken Sie auf **Weiter**.

6.  Klicken Sie unter **Features auswählen**auf **weiter**.

7.  Überprüfen Sie unter **Installations Auswahl bestätigen**Ihre Auswahl, und klicken Sie dann auf **Installieren**. Der Bereich **Installationsfortschritt** wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **Schließen**.
