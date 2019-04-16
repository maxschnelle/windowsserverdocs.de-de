---
title: Anpassen der Serversicherung
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19b2559c-6090-45af-9a08-2eefc28473c8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d18dca276bccdf672664a5a3c2bd28e0221fff94
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="customize-server-backup"></a>Anpassen der Serversicherung

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

## <a name="turn-off-server-backup-by-default"></a>Server-Sicherung standardmäßig deaktivieren  
 Sie können den Server-Sicherung standardmäßig deaktivieren. Sie müssen den Wert der **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** auf 1 fest, um diese Option zu aktivieren.  
  
 Wenn dieser Schlüssel festgelegt ist, wird die Benutzeroberfläche von Server-Sicherung nicht über das Dashboard oder Launchpad verfügbar gemacht werden. Dadurch können Sie Drittanbieteranwendungen für Server-Sicherung verwenden.  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>ServerBackup\ProviderDisabled hinzufügen? Registrierungsschlüssel, und setzen Sie den Wert auf 1  
  
1.  Klicken Sie auf dem Server, auf **starten**, klicken Sie auf **ausführen**, Typ **Regedit** in die **öffnen** Textbox, und klicken Sie dann auf **OK**.  
  
2.  Erweitern Sie im Navigationsbereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**, und erweitern Sie dann **ServerBackup**.  
  
3.  Mit der rechten Maustaste **ServerBackup**, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert**.  
  
4.  Geben Sie Namen **ProviderDisabled**.  
  
5.  Maustaste auf den Namen, und wählen Sie **ändern**, geben Sie **1** für die Wertdaten ein, und klicken Sie dann auf **OK**.  
  
## <a name="turn-on-server-backup"></a>Schalten Sie Server-Sicherung  
 Sie können Server-Sicherung einschalten, wenn sie durch das Erstellen deaktiviert wurde **ProviderDisabled** Registrierungsschlüssel (wie weiter oben in diesem Dokument beschrieben).  
  
 Sie müssen den Schlüssel löschen **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** um standardmäßig aktivieren, ändern Sie den Dienststarttyp der Windows Server-Server Backup-Dienst und den Server neu starten.  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>So löschen Sie ServerBackup\ProviderDisabled? Registrierungsschlüssel  
  
1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
2.  Geben Sie in das Suchfeld **Regedit**, und klicken Sie dann auf die **Regedit** Anwendung.  
  
3.  Erweitern Sie im Navigationsbereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**, und erweitern Sie dann **ServerBackup**.  
  
4.  Mit der rechten Maustaste **ProviderDisabled**, und klicken Sie dann auf **löschen**.  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Ändern des Starttyps des Windows Server-Sicherung Serverdiensts  
  
1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
2.  Geben Sie in das Suchfeld **Services.msc**, und klicken Sie dann auf **Dienste** Anwendung.  
  
3.  Im Bereich Dienste mit der rechten Maustaste die **Windows Server-Sicherung Serverdienst**, und klicken Sie auf **Eigenschaften**.  
  
4.  In **allgemeine** Registerkarte **automatische** für **Starttyp**.  
  
5.  Klicken Sie auf **OK** um das Dialogfeld zu schließen.  
  
#### <a name="restart-the-server"></a>Starten Sie den Server  
  
1.  Klicken Sie auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, auf **Einstellungen**, klicken Sie auf **Power**, und klicken Sie dann auf neu starten.