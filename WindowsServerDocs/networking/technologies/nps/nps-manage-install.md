---
title: Installieren des Netzwerkrichtlinienservers
description: In diesem Thema können Sie (Network Policy Server, NPS) installieren, indem Sie mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features-Assistenten in Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 4842a4ab-70bb-4744-bea7-70f2ac892ad1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9d11f77ff8b9db8bc10970b325afae60ba937cfa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831191"
---
# <a name="install-network-policy-server"></a>Installieren des Netzwerkrichtlinienservers

In diesem Thema können um mithilfe von Windows PowerShell oder das Hinzufügen von Rollen und Features-Assistent (Network Policy Server, NPS) zu installieren. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

> [!NOTE]
> Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktiviert ist, werden Firewallausnahmen für diese Ports automatisch während des Installationsvorgangs für Internetprotokoll Version 6 erstellt \(IPv6\) und IPv4-Datenverkehr. Wenn Ihre Netzwerkzugriffsserver für das Senden von RADIUS-Verkehr über andere diese Standardwerte Ports konfiguriert sind, entfernen Sie die Ausnahmen, die in der Windows-Firewall mit erweiterter Sicherheit während der NPS-Installation erstellt, und erstellen Sie Ausnahmen für die Ports, denen Sie verwenden RADIUS-Verkehr.

**Administratoranmeldeinformationen**

Zur Ausführung dieses Verfahrens müssen Sie ein Mitglied der Gruppe **Domänen-Admins** sein.

## <a name="to-install-nps-by-using-windows-powershell"></a>Zum Installieren von NPS mithilfe von Windows PowerShell

Geben Sie den folgenden Befehl zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell, Windows PowerShell als Administrator ausführen, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature NPAS -IncludeManagementTools`

## <a name="to-install-nps-by-using-server-manager"></a>Zum Installieren von NPS mithilfe von Server-Manager

1.  Klicken Sie auf NPS1 unter Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.

4.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.

5.  In **Serverrollen auswählen**im **Rollen**Option **Netzwerkrichtlinien- und Zugriffsdienste**. Ein Dialogfeld gefragt, ob sie Funktionen hinzufügen sollten, die für Netzwerkrichtlinien- und Zugriffsdienste erforderlich sind. Klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **weiter**

6.  Klicken Sie unter **Features auswählen** auf **Weiter**, überprüfen Sie unter **Netzwerkrichtlinien- und Zugriffsdienste** die angegebenen Informationen, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie unter **Rollendienste auswählen** auf **Netzwerkrichtlinienserver**.  Klicken Sie unter **Sollen für Netzwerkrichtlinienserver erforderliche Features hinzugefügt werden?** auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

8.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Zielserver bei Bedarf automatisch neu starten**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja** und dann auf **Installieren**. Auf der Seite %%amp;quot;Installationsstatus%%amp;quot; wird der Status während der Installation angezeigt. Wenn der Prozess abgeschlossen ist, die Meldung "Installation erfolgreich auf *ComputerName*" angezeigt wird, wobei *ComputerName* ist der Name des Computers, auf dem Netzwerkrichtlinienserver installiert. Klicken Sie auf **Schließen**.

Weitere Informationen finden Sie unter [verwalten NPSs](nps-manage-servers.md).