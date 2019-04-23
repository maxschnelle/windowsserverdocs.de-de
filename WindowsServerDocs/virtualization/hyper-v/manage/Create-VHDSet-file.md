---
title: Legen Sie Hyper-V VHD-Dateien erstellen
description: Schritte zum Erstellen einer VHDset-Datei auf dem Hyper-V-2016
author: jiwool
ms.author: jiwool
manager: senthilr
ms.date: 01/26/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: compute-hyper-v
ms.assetid: 444e1496-9e5a-41cf-bfbc-306e2ed8e00a
audience: IT Pros
ms.reviewer: kathydav
ms.openlocfilehash: 61f2450857cbeaffd7f75f7b259e9f9de06ba5c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870401"
---
# <a name="create-hyper-v-vhd-set-files"></a>Legen Sie Hyper-V VHD-Dateien erstellen
Legen Sie die VHD-Dateien sind ein neues Modell mit der freigegebenen virtuellen Festplatte in für gastcluster in Windows Server 2016. Legen Sie die VHD-Dateien der freigegebene virtuelle Festplatten im Onlinemodus zu unterstützen, unterstützt Hyper-V-Replikat und können in anwendungskonsistente Prüfpunkte enthalten sein. 

Legen Sie die VHD-Dateien verwenden einen neuen Dateityp für die virtuelle Festplatte. VIRTUELLE FESTPLATTEN. Legen Sie die VHD-Dateien speichern, Prüfpunktinformationen zur Gruppe virtuelle Festplatte, die in gastclustern in Form von Metadaten verwendet wird.

Hyper-V behandelt alle Aspekte der Verwaltung von prüfpunktketten, und legen Sie die Zusammenführung der freigegebenen virtuellen Festplatte. Verwaltungssoftware kann Datenträgervorgänge wie im Onlinemodus legen Sie die VHD-Dateien auf die gleiche Weise, die für ausführen. VHDX-Dateien. Dies bedeutet, dass Verwaltungssoftware nicht wissen, über das Festlegen von VHD-Dateiformat.

## <a name="create-a-vhd-set-file-from-hyper-v-manager"></a>Erstellen Sie eine legen Sie die VHD-Datei von Hyper-V-Manager

1.  Öffnen Sie den Hyper-V-Manager. Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Hyper-V-Manager**.
2.  Klicken Sie im Aktionsbereich auf **Neu**, und klicken Sie dann auf **Festplatte**.
3.  Auf der **Datenträgerformat auswählen** Seite **legen Sie die VHD** als das Format der virtuellen Festplatte.
4.  Durchlaufen Sie die Seiten des Assistenten zum Anpassen der virtuellen Festplatte aus. Sie können auf **Weiter** klicken, um alle Seiten des Assistenten nacheinander zu bearbeiten. Sie können aber auch im linken Bereich auf den Namen einer Seite klicken, um direkt zu einer Seite zu wechseln.
5.  Wenn Sie mit dem Konfigurieren der virtuellen Festplatte fertig sind, klicken Sie auf **Fertig stellen**.

## <a name="create-a-vhd-set-file-from-windows-powershell"></a>Erstellen Sie eine legen Sie die VHD-Datei aus Windows PowerShell

Verwenden der [New-VHD](https://technet.microsoft.com/library/hh848503.aspx) -Cmdlet mit dem Dateinamen. Virtuelle Festplatten im Dateipfad. Dieses Beispiel erstellt eine legen Sie die VHD-Datei, die mit dem Namen base.vhds, das 10 GB groß ist.

``` PowerShell
PS c:\>New-VHD -Path c:\base.vhds -SizeBytes 10GB
```

## <a name="migrate-a-shared-vhdx-file-to-a-vhd-set-file"></a>Migrieren Sie eine freigegebene VHDX-Datei in eine legen Sie die VHD-Datei

Migrieren einen vorhandenen freigegebenen VHDX in eine VHD, ist das Offlineschalten des virtuellen Computers erforderlich. Dies ist die empfohlene Vorgehensweise, die mithilfe von Windows PowerShell:

1.  Entfernen Sie die VHDX auf dem virtuellen Computer an. Führen Sie zum Beispiel aus: 
  ``` PowerShell
  PS c:\>Remove-VMHardDiskDrive existing.vhdx
  ```
  
2.  Konvertieren Sie die VHDX auf einer virtuellen Festplatten. Führen Sie zum Beispiel aus:
  ``` PowerShell
  PS c:\>Convert-VHD existing.vhdx new.vhds
  ```
  
3.  Fügen Sie die virtuellen Festplatten mit dem virtuellen Computer hinzu. Führen Sie zum Beispiel aus:
  ``` PowerShell
  PS c:\>Add-VMHardDiskDrive new.vhds
  ```
  



