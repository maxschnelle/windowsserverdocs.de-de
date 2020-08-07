---
title: Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver
description: Dieses Thema ist Teil des BranchCache-Bereitstellungs Handbuchs für Windows Server 2016, das zeigt, wie BranchCache im Modus für verteilte und gehostete Caches bereitgestellt wird, um die WAN-Bandbreitenauslastung in Zweigniederlassungen zu optimieren.
manager: brianlic
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ddb6a9d8ad14146d6f4aca27171649fde3b227eb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971917"
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe dieses Verfahrens können Sie den Rollen Dienst " **BranchCache für Netzwerkdateien** " der Server Rolle "Dateidienste" auf einem Computer mit Windows Server 2016 installieren.

> [!IMPORTANT]
> Führen Sie dieses Verfahren nicht weiter aus, wenn die Serverrolle Dateidienste noch nicht installiert wurde. Weitere Informationen finden Sie unter [Installieren eines neuen Dateiservers als Inhalts Server](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md).

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.

> [!NOTE]
> Um dieses Verfahren mithilfe von Windows PowerShell auszuführen, führen Sie Windows PowerShell als Administrator aus, geben Sie die folgenden Befehle an der Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.
>
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`
>
> Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Rollen Dienst "Datendeduplizierung" zu installieren.
>
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`

### <a name="to-install-the-branchcache-for-network-files-role-service"></a>So installieren Sie den Rollen Dienst "BranchCache für Netzwerkdateien"

1.  Klicken Sie im Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet. Klicken Sie auf **Weiter**.

2.  Vergewissern Sie sich, dass unter **Installationstyp auswählen**die Option **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **weiter**.

3.  Stellen **Sie in Zielserver auswählen**sicher, dass der richtige Server ausgewählt ist, und klicken Sie dann auf **weiter**.

4.  Beachten Sie, dass unter **Server Rollen auswählen**unter **Rollen**die Rolle **Datei-und Speicherdienste** bereits installiert ist. Klicken Sie auf den Pfeil links neben dem Rollennamen, um die Auswahl der Rollen Dienste zu erweitern, und klicken Sie dann auf den Pfeil links neben **Datei-und iSCSI-Dienste**.

5.  Aktivieren Sie das Kontrollkästchen **BranchCache für Netzwerkdateien**.

    > [!TIP]
    > Wenn Sie dies nicht bereits getan haben, sollten Sie auch das Kontrollkästchen für die **Datendeduplizierung**aktivieren.

    Klicken Sie auf **Weiter**.

6.  Klicken Sie unter **Features auswählen**auf **weiter**.

7.  Überprüfen Sie unter **Installations Auswahl bestätigen**Ihre Auswahl, und klicken Sie dann auf **Installieren**. Der Bereich **Installationsfortschritt** wird während der Installation angezeigt. Wenn die Installation abgeschlossen ist, klicken Sie auf **Schließen**.



