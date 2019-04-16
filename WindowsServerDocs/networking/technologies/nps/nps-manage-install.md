---
title: Installieren von Netzwerkrichtlinienserver
description: In diesem Thema können Sie den Netzwerkrichtlinienserver (Network Policy Server, NPS) installieren Sie mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features-Assistenten in Windows Server2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4842a4ab-70bb-4744-bea7-70f2ac892ad1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b76654fa01b68b5a8c9ea1efc80dfbc47e6a62f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-network-policy-server"></a>Installieren von Netzwerkrichtlinienserver

In diesem Thema können Sie Netzwerkrichtlinienserver (Network Policy Server, NPS) mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features-Assistenten installieren. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

> [!NOTE]
> Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktiviert ist, werden die Firewallausnahmen für diese Ports während der Installation für Internetprotokoll Version 6 \(IPv6\) und IPv4-Datenverkehr automatisch erstellt. Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere Ports als die standardmäßigen konfiguriert sind, entfernen Sie die Ausnahmen in der Windows-Firewall mit erweiterter Sicherheit während der Installation von NPS erstellt, und erstellen Sie Ausnahmen für die Ports, die Sie für RADIUS-Datenverkehr verwenden.

**Administrative Anmeldeinformationen**

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Domänen-Admins** Gruppe.

## <a name="to-install-nps-by-using-windows-powershell"></a>So installieren Sie NPS mithilfe von Windows PowerShell

Geben Sie den folgenden Befehl zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature NPAS -IncludeManagementTools`

## <a name="to-install-nps-by-using-server-manager"></a>So installieren Sie NPS mithilfe des Server-Managers

1.  Klicken Sie auf NPS1 unter Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.

2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.

    > [!NOTE]
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.

3.  In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.

4.  In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.

5.  In **Serverrollen auswählen**im **Rollen**Option **Netzwerkrichtlinien- und Zugriffsdienste**. Ein Dialogfeld gefragt werden, ob sie Features hinzufügen sollten, die für Netzwerkrichtlinien- und Zugriffsdienste erforderlich sind. Klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **weiter**

6.  In **Features auswählen**, klicken Sie auf **Weiter**, und im **Netzwerkrichtlinien- und Zugriffsdienste**, überprüfen Sie die Informationen, die bereitgestellt wird, und klicken Sie dann auf **Weiter**.

7.  In **Rollendienste auswählen**, klicken Sie auf **Netzwerkrichtlinienserver**.  In **Hinzufügen von Features, die für Netzwerkrichtlinienserver erforderlich sind**, klicken Sie auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

8.  In **Installationsauswahl bestätigen**, klicken Sie auf **Zielserver bei Bedarf automatisch neu**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja**, und klicken Sie dann auf **installieren**. Der Installationsstatus wird Status während der Installation. Wenn der Vorgang abgeschlossen ist, die Meldung "die Installation war erfolgreich auf *ComputerName*" angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem Netzwerkrichtlinienserver installiert. Klicken Sie auf **schließen **.

Weitere Informationen finden Sie unter [NPS-Server verwalten](nps-manage-servers.md).