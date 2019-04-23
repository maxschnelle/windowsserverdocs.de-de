---
title: Verwalten von Benutzern in Ihrer RDS-Sammlung
description: Informationen Sie zum Verwalten von Benutzern in Remote Desktop Services.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2727e1ab-69b8-46f3-9f6d-2540324fe596
author: christianmontoya
ms.author: chrimo
ms.date: 03/27/2018
manager: scottman
ms.openlocfilehash: 4b45061697926a3003712a88610cb17ef3c00c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859641"
---
# <a name="manage-users-in-your-rds-collection"></a>Verwalten von Benutzern in Ihrer RDS-Sammlung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Als Administrator können Sie direkt verwalten, welche Benutzer Zugriff auf bestimmte Sammlungen haben. Auf diese Weise erstellen Sie eine Sammlung mit standard-Anwendungen für Information Worker können dann eine separate Sammlung mit grafikintensive Anwendungen für Engineers erstellen. Es gibt zwei primäre Schritte zum Verwalten des Benutzerzugriffs in einer Bereitstellung für Remote Desktop Services (RDS):

1.  [Erstellen von Benutzern und Gruppen in Active Directory](#create-your-users-and-groups-in-active-directory)
2.  [Zuweisen von Benutzern und Gruppen für Sammlungen](#assign-users-and-groups-to-collections)


## <a name="create-your-users-and-groups-in-active-directory"></a>Erstellen Sie Ihre Benutzer und Gruppen in Active Directory

In einer RDS-Bereitstellung ist die Active Directory Domain Services (AD DS) die Quelle der alle Benutzer, Gruppen und andere Objekte in der Domäne. Können Sie Active Directory direkt mit PowerShell verwalten, oder Sie können integrierte Benutzeroberflächentools, die einfachere und flexiblere hinzufügen. Die folgenden Schritte führt Sie zum Installieren dieser Tools – Wenn Sie nicht bereits installiert haben, und verwenden Sie diese Tools zum Verwalten von Benutzern und Gruppen.

### <a name="install-ad-ds-tools"></a>Installieren von AD DS-tools

Die folgenden Schritte beschreiben, wie Sie die AD DS-Tools auf einem Server, die bereits mit AD DS installieren. Nach Abschluss der Installation können Sie dann Erstellen von Benutzern oder Gruppen erstellen.

1. Verbinden Sie mit dem Server mit Active Directory Domain Services. Für Azure-Bereitstellungen:
   1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, und klicken Sie dann auf die Ressourcengruppe für die Bereitstellung
   2. Wählen Sie die AD-Computer.
   3. Klicken Sie auf **verbinden > Öffnen** den Remotedesktopclient zu öffnen. Wenn **Connect** abgeblendet ist, den virtuellen Computer verfügen nicht über eine öffentliche IP-Adresse. Damit geben Sie ihm eine führen Sie die folgenden Schritte aus, klicken Sie dann wiederholen Sie diesen Schritt.
      1. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.
      2. Klicken Sie auf **Einstellungen > IP-Adresse**.
      3. Für **öffentliche IP-Adresse**Option **aktiviert**, und klicken Sie dann auf **IP-Adresse**.
      4. Wenn Sie eine vorhandene öffentliche IP-Adresse, die Sie verwenden möchten verfügen, wählen Sie sie aus der Liste aus. Klicken Sie anderenfalls auf **neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und **speichern**.
   4. Klicken Sie auf dem Client auf **Connect**, und klicken Sie dann auf **verwenden ein anderes Konto**. Geben Sie den Benutzernamen und das Kennwort für ein Domänenkonto für Administrator ein.
   5. Klicken Sie auf **Ja** Wenn zu dem Zertifikat aufgefordert.
2. Installieren Sie die AD DS-Tools:
   1. Klicken Sie in Server-Manager auf **verwalten > Rollen und Features hinzufügen**.
   2. Klicken Sie auf **rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf den aktuellen AD-Server. Führen Sie die Schritte, bis Sie auf die **Features** Registerkarte.
   3. Erweitern Sie **Remoteserver-Verwaltungstools > Rollenverwaltungstools > AD DS und AD LDS-Tools**, und wählen Sie dann **AD DS-Tools**.
   4. Wählen Sie **automatisch neu starten die Zielserver bei Bedarf**, und klicken Sie dann auf **installieren**.

### <a name="create-a-group"></a>Erstellen einer Gruppe

Sie können AD DS-Gruppen verwenden, Gewähren von Zugriff auf eine Gruppe von Benutzern, die die gleichen Remoteressourcen verwenden müssen.

1. Klicken Sie im Server-Manager auf dem Server mit AD DS **Extras > Active Directory-Benutzer und-Computer**.
2. Erweitern Sie die Domäne im linken Bereich, um die Unterordner anzuzeigen.
3. Mit der rechten Maustaste in des Ordners, in dem Sie die Gruppe erstellen, und klicken Sie dann auf möchten **neu > Gruppe**.
4. Geben Sie einen Namen für die entsprechende Gruppe aus, und wählen Sie dann **Global** und **Sicherheit**.

### <a name="create-a-user-and-add-to-a-group"></a>Erstellen eines Benutzers und einer Gruppe hinzufügen
1. Klicken Sie im Server-Manager auf dem Server mit AD DS **Extras > Active Directory-Benutzer und-Computer**.
2. Erweitern Sie die Domäne im linken Bereich, um die Unterordner anzuzeigen.
3. Mit der rechten Maustaste **Benutzer**, und klicken Sie dann auf **neu > Benutzer**.
4. Geben Sie, Minimum, einen Vornamen und einen Benutzernamen für die Anmeldung ein.
5. Geben Sie an, und ein Kennwort für den Benutzer. Legen Sie entsprechende Optionen, z. B. **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**.
6. Fügen Sie den neuen Benutzer zu einer Gruppe hinzu:
   1. In der **Benutzer** Ordner mit der rechten Maustaste des neuen Benutzers.
   2. Klicken Sie auf **hinzufügen zu einer Gruppe**.
   3. Geben Sie den Namen der Gruppe, zu der Sie den Benutzer hinzufügen möchten.

## <a name="assign-users-and-groups-to-collections"></a>Zuweisen von Benutzern und Gruppen für Sammlungen
Nun, dass Sie die Benutzer und Gruppen in Active Directory erstellt haben, können Sie einige Granularität in Bezug auf, die Zugriff auf den Remotedesktop-Sammlungen in Ihrer Bereitstellung hat hinzufügen.

1. Verbinden Sie mit dem Server mit der Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker)-Rolle, die zuvor beschriebenen Schritte.
2. Fügen Sie die anderen Remotedesktop-Server, auf dem Remotedesktop-Verbindungsbroker-Pool von verwalteten Servern:
   1. Klicken Sie in Server-Manager auf **verwalten > Hinzufügen von Servern**.
   2. Klicken Sie auf **Jetzt suchen**.
   3. Klicken Sie auf jedem Server in Ihrer Bereitstellung, die eine Remotedesktopdienste-Rolle ausgeführt wird, und klicken Sie dann auf **OK**.
3. Bearbeiten Sie eine Sammlung, um den Zugriff auf bestimmte Benutzer oder Gruppen zuweisen:
   1. Klicken Sie in Server-Manager auf **Remote Desktop Services > Übersicht über die**, und klicken Sie dann auf eine bestimmte Sammlung.
   2. Klicken Sie unter **Eigenschaften**, klicken Sie auf **Aufgaben > bearbeiten Eigenschaften**.
   3. Klicken Sie auf **Benutzergruppen**.
   4. Klicken Sie auf **hinzufügen** , und geben Sie den Benutzer oder Gruppe, die Sie auf die Auflistung zugreifen möchten. Sie können Benutzer und Gruppen aus diesem Fenster auch entfernen, indem Sie auswählen, die Benutzer oder eine Gruppe, die Sie entfernen möchten, und klicken Sie dann auf **entfernen**. 
   
   >[!NOTE] 
   > Das Fenster der Benutzer Gruppen darf nicht leer sein. Um den von Benutzern einzuschränken, wer Zugriff auf die Auflistung haben, müssen Sie bestimmte Benutzer oder Gruppen zuerst hinzufügen, vor dem größere Gruppen entfernen.