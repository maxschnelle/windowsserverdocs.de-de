---
title: Netzwerk Richtlinien Server installieren
description: Sie können dieses Thema verwenden, um den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe von Windows PowerShell oder dem Assistenten zum Hinzufügen von Rollen und Features in Windows Server 2016 zu installieren.
manager: brianlic
ms.topic: article
ms.assetid: 4842a4ab-70bb-4744-bea7-70f2ac892ad1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8335c4a5a7f42fa33182a78e3dcb6777f76f6483
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953936"
---
# <a name="install-network-policy-server"></a>Netzwerk Richtlinien Server installieren

Sie können dieses Thema verwenden, um den Netzwerk Richtlinien Server (Network Policy Server, NPS) mithilfe von Windows PowerShell oder dem Assistenten zum Hinzufügen von Rollen und Features zu installieren. NPS ist ein Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste.

> [!NOTE]
> Standardmäßig überwacht NPS RADIUS-Datenverkehr auf den Ports 1812, 1813, 1645 und 1646 für alle installierten Netzwerkadapter. Wenn die Windows-Firewall mit erweiterter Sicherheit bei der Installation von NPS aktiviert ist, werden während des Installationsvorgangs automatisch Firewallausnahmen für diese Ports erstellt, sowohl für \( IPv6 \) -als auch für IPv4-Datenverkehr der Internet Protokollversion 6. Wenn Ihre Netzwerk Zugriffs Server für das Senden von RADIUS-Datenverkehr über andere Ports als diese Standardeinstellungen konfiguriert sind, entfernen Sie die Ausnahmen, die bei der NPS-Installation in der Windows-Firewall mit erweiterter Sicherheit erstellt wurden, und erstellen Sie Ausnahmen für die Ports, die Sie für den RADIUS

**Administrator Anmelde Informationen**

Zur Ausführung dieses Verfahrens müssen Sie ein Mitglied der Gruppe **Domänen-Admins** sein.

## <a name="to-install-nps-by-using-windows-powershell"></a>So installieren Sie NPS mithilfe von Windows PowerShell

Wenn Sie dieses Verfahren mithilfe von Windows PowerShell ausführen möchten, führen Sie Windows PowerShell als Administrator aus, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.

`Install-WindowsFeature NPAS -IncludeManagementTools`

## <a name="to-install-nps-by-using-server-manager"></a>So installieren Sie NPS mit Server-Manager

1.  Klicken Sie auf NPS1 unter Server-Manager auf **Verwalten** und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.

2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.

    > [!NOTE]
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.

3.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.

4.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.

5.  Wählen Sie unter **Server Rollen auswählen**unter **Rollen**die Option **Netzwerk Richtlinien-und Zugriffs Dienste**aus. Es wird ein Dialogfeld geöffnet, in dem Sie gefragt werden, ob für Netzwerk Richtlinien-und Zugriffs Dienste erforderliche Features hinzugefügt werden sollen. Klicken Sie auf **Features hinzufügen**und dann auf **weiter** .

6.  Klicken Sie unter **Features auswählen** auf **Weiter**, überprüfen Sie unter **Netzwerkrichtlinien- und Zugriffsdienste** die angegebenen Informationen, und klicken Sie dann auf **Weiter**.

7.  Klicken Sie unter **Rollendienste auswählen** auf **Netzwerkrichtlinienserver**.  Klicken Sie unter **Sollen für Netzwerkrichtlinienserver erforderliche Features hinzugefügt werden?** auf **Features hinzufügen**. Klicken Sie auf **Weiter**.

8.  Klicken Sie unter **Installationsauswahl bestätigen** auf **Zielserver bei Bedarf automatisch neu starten**. Wenn Sie aufgefordert werden, die Auswahl zu bestätigen, klicken Sie auf **Ja** und dann auf **Installieren**. Auf der Seite %%amp;quot;Installationsstatus%%amp;quot; wird der Status während der Installation angezeigt. Wenn der Vorgang abgeschlossen ist, wird die Meldung "Installation erfolgreich auf *Computername*" angezeigt, wobei *Computername* der Name des Computers ist, auf dem Sie den Netzwerk Richtlinien Server installiert haben. Klicken Sie auf **Schließen**.

Weitere Informationen finden Sie unter [Verwalten von NPSS](nps-manage-servers.md).