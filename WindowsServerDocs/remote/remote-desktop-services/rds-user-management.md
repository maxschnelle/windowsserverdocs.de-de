---
title: Verwalten von Benutzern in Ihrer RDS-Sammlung
description: Erfahren Sie, wie Sie Benutzer in Remotedesktopdiensten verwalten.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 2727e1ab-69b8-46f3-9f6d-2540324fe596
author: christianmontoya
ms.author: chrimo
ms.date: 03/27/2018
manager: scottman
ms.openlocfilehash: 430c38f98dd9aec3034e023d737952e3015622eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858683"
---
# <a name="manage-users-in-your-rds-collection"></a>Verwalten von Benutzern in Ihrer RDS-Sammlung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Als Administrator können Sie direkt verwalten, welche Benutzer Zugriff auf bestimmte Sammlungen haben. Auf diese Weise können Sie eine Sammlung mit Standardanwendungen für Information Worker erstellen und dann eine separate Sammlung mit grafikintensiven Modellierungsanwendungen für Ingenieure. Es gibt zwei Hauptschritte beim Verwalten des Benutzerzugriffs in einer Remotedesktopdienste-Bereitstellung (RDS):

1.    [Erstellen von Benutzern und Gruppen in Active Directory](#create-your-users-and-groups-in-active-directory)
2.    [Zuweisen von Benutzern und Gruppen zu Sammlungen](#assign-users-and-groups-to-collections)


## <a name="create-your-users-and-groups-in-active-directory"></a>Erstellen von Benutzern und Gruppen in Active Directory

In einer RDS-Bereitstellung bildet Active Directory Domain Services (AD DS) die Quelle aller Benutzer, Gruppen und sonstigen Objekte in der Domäne. Sie können Active Directory direkt mit PowerShell verwalten oder integrierte UI-Tools verwenden, die mehr Komfort und Flexibilität bieten. Die folgenden Schritte führen Sie durch die Installation dieser Tools – wenn sie bei Ihnen noch nicht installiert sind – und anschließend durch die Verwendung dieser Tools zum Verwalten von Benutzern und Gruppen.

### <a name="install-ad-ds-tools"></a>Installieren von AD DS-Tools

In den folgenden Schritten wird detailliert beschrieben, wie Sie die AD DS-Tools auf einem Server installieren, der bereits AD DS ausführt. Nach der Installation können Sie dann Benutzer oder Gruppen erstellen.

1. Stellen Sie eine Verbindung mit dem Server her, der Active Directory Domain Services ausführt. Für Azure-Bereitstellungen:
   1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, und klicken Sie dann auf die Ressourcengruppe für die Bereitstellung
   2. Wählen Sie den virtuellen AD-Computer aus.
   3. Klicken Sie auf **Verbinden > Öffnen**, um den Remotedesktopclient zu öffnen. Wenn **Verbinden** abgeblendet ist, verfügt der virtuelle Computer möglicherweise nicht über eine öffentliche IP-Adresse. Führen Sie die folgenden Schritte aus, um ihn mit einer zu konfigurieren, und versuchen Sie dann noch einmal, diesen Schritt auszuführen.
      1. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.
      2. Klicken Sie auf **Einstellungen > IP-Adresse**.
      3. Wählen Sie für **Öffentliche IP-Adresse** die Option **Aktiviert** aus, und klicken Sie dann auf **IP-Adresse**.
      4. Wenn Sie über eine vorhandene öffentliche IP-Adresse verfügen, die Sie verwenden möchten, wählen Sie sie in der Liste aus. Klicken Sie andernfalls auf **Neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und auf **Speichern**.
   4. Klicken Sie im Client auf **Verbinden**,und klicken Sie dann auf **Anderes Konto verwenden**. Geben Sie den Benutzernamen und das Kennwort für ein Domänenadministratorkonto ein.
   5. Klicken Sie auf **Ja**, wenn Sie wegen des Zertifikats gefragt werden.
2. Installieren der AD DS-Tools:
   1. Klicken Sie im Server-Manager auf **Verwalten > Rollen und Features hinzufügen**.
   2. Klicken Sie auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie dann auf den aktuellen AD-Server. Führen Sie die Schritte aus, bis Sie zur Registerkarte **Features** gelangen.
   3. Erweitern Sie **Remoteserver-Verwaltungstools > Rollenverwaltungstools > Tools für AD DS und AD LDS**, und wählen Sie dann **AD DS-Tools** aus.
   4. Wählen Sie **Zielserver bei Bedarf automatisch neu starten** aus, und klicken Sie dann auf **Installieren**.

### <a name="create-a-group"></a>Erstellen einer Gruppe

Sie können AD DS-Gruppen verwenden, um einer Menge von Benutzern, die die gleichen Remoteressourcen verwenden müssen, Zugriff zu erteilen.

1. Klicken Sie im Server-Manager auf dem Server, der AD DS ausführt, auf **Extras > Active Directory-Benutzer und -Computer**.
2. Erweitern Sie die Domäne im linken Bereich, um ihre Unterordner anzuzeigen.
3. Klicken Sie mit der rechten Maustaste auf den Ordner, in dem Sie die Gruppe erstellen möchten, und klicken Sie dann auf **Neu > Gruppe**.
4. Geben Sie einen geeigneten Gruppennamen ein, und wählen Sie dann **Global** und **Sicherheit** aus.

### <a name="create-a-user-and-add-to-a-group"></a>Erstellen eines Benutzers und Hinzufügen zu einer Gruppe
1. Klicken Sie im Server-Manager auf dem Server, der AD DS ausführt, auf **Extras > Active Directory-Benutzer und -Computer**.
2. Erweitern Sie die Domäne im linken Bereich, um ihre Unterordner anzuzeigen.
3. Klicken Sie mit der rechten Maustaste auf **Benutzer** und anschließend auf **Neu > Benutzer**.
4. Geben Sie mindestens einen Vornamen und einen Benutzeranmeldenamen ein.
5. Geben Sie ein Kennwort für den Benutzer ein, und bestätigen Sie es. Legen Sie geeignete Benutzeroptionen fest, beispielsweise **Benutzer muss Kennwort bei der nächsten Anmeldung ändern**.
6. Fügen Sie den neuen Benutzer einer Gruppe hinzu:
   1. Klicken Sie im Ordner **Benutzer** mit der rechten Maustaste auf den neuen Benutzer.
   2. Klicken Sie auf **Zu einer Gruppe hinzufügen**.
   3. Geben Sie den Namen der Gruppe ein, der Sie den Benutzer hinzufügen möchten.

## <a name="assign-users-and-groups-to-collections"></a>Zuweisen von Benutzern und Gruppen zu Sammlungen
Jetzt, da Sie die Benutzer und Gruppen in Active Directory erstellt haben, können Sie mehr Granularität im Hinblick darauf hinzufügen, wer Zugriff auf die Remotedesktopsammlungen in Ihrer Bereitstellung hat.

1. Stellen Sie eine Verbindung mit dem Server her, der die Rolle des Remotedesktop-Verbindungsbrokers (RD-Verbindungsbroker) ausführt, und folgen Sie dazu den weiter oben beschriebenen Schritten.
2. Fügen Sie dem Pool der verwalteten Server des RD-Verbindungsbrokers die anderen Remotedesktopserver hinzu:
   1. Klicken Sie im Server-Manager auf **Verwalten > Server hinzufügen**.
   2. Klicken Sie auf **Jetzt suchen**.
   3. Klicken Sie auf jeden Server in Ihrer Bereitstellung, der eine Remotedesktopdienste-Rolle ausführt, und klicken Sie dann auf **OK**.
3. Bearbeiten Sie eine Sammlung, um den Zugriff zu bestimmten Benutzern oder Gruppen hinzuzufügen:
   1. Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht**, und klicken Sie dann auf eine bestimmte Sammlung.
   2. Klicken Sie unter **Eigenschaften** auf **Aufgaben > Eigenschaften bearbeiten**.
   3. Klicken Sie auf **Benutzergruppen**.
   4. Klicken Sie auf **Hinzufügen**, und geben Sie den Benutzer oder die Gruppe ein, dem bzw. der Sie Zugriff auf die Sammlung erteilen möchten. In diesem Fenster können Sie auch Benutzer und Gruppen entfernen, indem Sie den zu entfernenden Benutzer oder die zu entfernende Gruppe auswählen und dann auf **Entfernen** klicken. 
   
   >[!NOTE] 
   > Das Fenster „Benutzergruppen“ darf nie leer sein. Um den Bereich der Benutzer einzuschränken, die Zugriff auf die Sammlung haben, müssen Sie zuerst bestimmte Benutzer oder Gruppen hinzufügen, bevor Sie breitere Gruppen entfernen.