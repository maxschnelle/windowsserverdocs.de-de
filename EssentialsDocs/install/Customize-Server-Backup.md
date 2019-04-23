---
title: Anpassen der Serversicherung
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838541"
---
# <a name="customize-server-backup"></a>Anpassen der Serversicherung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="turn-off-server-backup-by-default"></a>Standardmäßiges Deaktivieren der Serversicherung  
 Sie haben die Möglichkeit, die Serversicherung standardmäßig zu deaktivieren. Um diese Option zu aktivieren, müssen Sie den Wert für **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** auf 1 festlegen.  
  
 Wenn dieser Schlüssel festgelegt ist, ist die Benutzerschnittstelle der Serversicherung über das Dashboard oder das Launchpad nicht verfügbar. Dies ermöglicht Ihnen bei der Serversicherung den Einsatz von Anwendungen von Drittanbietern.  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>ServerBackup\ProviderDisabled hinzufügen? Registrierungsschlüssel und legen Sie den Wert auf 1  
  
1.  Klicken Sie auf dem Server auf **Start**, klicken Sie auf **Ausführen**, geben Sie **regedit** im Textfeld **Öffnen** ein, und klicken Sie dann auf **OK**.  
  
2.  Erweitern Sie im Navigationsbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** und **ServerBackup**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **ServerBackup**, klicken Sie auf **Neu** und anschließend auf **DWORD-Wert**.  
  
4.  Geben Sie als Namen **ProviderDisabled** ein.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Namen, wählen Sie **Ändern**aus, geben Sie **1** für die Wertdaten ein, und klicken Sie anschließend auf **OK**.  
  
## <a name="turn-on-server-backup"></a>Aktivieren der Serversicherung  
 Sie können die Serversicherung aktivieren, wenn sie durch die Erstellung des Registrierungsschlüssels **ProviderDisabled** (weiter oben in diesem Dokument beschrieben) deaktiviert wurde.  
  
 Wenn Sie die Serversicherung standardmäßig aktivieren möchten, müssen Sie den Schlüssel **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** löschen, den Dienststarttyp der Windows Server-Serversicherung ändern und den Server erneut starten.  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>ServerBackup\ProviderDisabled löschen? Registrierungsschlüssel  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **regedit**ein, und klicken Sie dann auf die Anwendung **Regedit** .  
  
3.  Erweitern Sie im Navigationsbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** und **ServerBackup**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **ProviderDisabled**, und klicken Sie dann auf **Löschen**.  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Ändern des Starttyps des Windows Server-Diensts für die Serversicherung  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **services.msc** ein, und klicken Sie dann auf die Anwendung **Dienste**.  
  
3.  Klicken Sie im Bereich der Dienste mit der rechten Maustaste auf **Windows Server-Dienst für die Serversicherung**, und klicken Sie auf **Eigenschaften**.  
  
4.  Wählen Sie auf der Registerkarte **Allgemein** als **Starttyp** die Option **Automatisch**aus.  
  
5.  Klicken Sie auf **OK**, um das Dialogfeld zu schließen.  
  
#### <a name="restart-the-server"></a>Neustart des Servers  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie nacheinander auf **Einstellungen**, **Stromversorgung** und "Neu starten".