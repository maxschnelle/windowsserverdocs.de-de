---
title: Speichern und Freigeben von Dateien auf einem USB-Flashlaufwerk
description: Erfahren Sie, wie Sie in Multipoint Services auf einem USB-Speicherstick speichern.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 51f6564e-a07f-4b13-8567-a5f080cc2e0d
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: e5eb73bdc630d375a19da5c42ed6ceb265eab2e4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855653"
---
# <a name="save-and-share-files-on-a-usb-flash-drive"></a>Speichern und Freigeben von Dateien auf einem USB-Flashlaufwerk
Zusätzlich zur Freigabe von Inhalten mithilfe von öffentlichen Ordnern in Windows-Explorer können Sie Inhalte auch über ein USB-Speichergerät, z. b. einen USB-Speicherstick oder ein Massen Speichergerät, freigeben. Wenn ein USB-Speichergerät direkt an den Hostcomputer oder einen USB-Hub, der nicht als Stationshub fungiert, angeschlossen wird, wird dieses Speichergerät für alle Benutzer – sowohl *Standardbenutzer* als auch *Administratoren* – im gesamten MultiPoint Services-System als Wechseldatenträger angezeigt.  
  
Sie können einen Wechseldatenträger auch verwenden, um private Dokumente im Windows-Explorer in einem privaten Ordner zu speichern, z.B. im Ordner **Eigene Dokumente** in der Bibliothek **Dokumente**.  
  
 > [!NOTE]  
 > Dashboardbenutzer können die Verwendung von USB-Speicher blockieren. Weitere Informationen finden Sie unter [Block or Unblock USB Storage](Block-or-Unblock-USB-Storage.md) (Blockieren oder Aufheben der Blockierung von USB-Speicher).  
  
## <a name="to-share-content-that-is-stored-directly-on-a-removable-storage-device"></a>So geben Sie Inhalte frei, die direkt auf einem Wechseldatenträger gespeichert sind  
  
1.  Verbinden Sie den Wechseldatenträger mit einem freien USB-Anschluss des Hostcomputers oder mit einem USB-Hub, der im MultiPoint Services-System nicht als *Stationshub* fungiert.  
2.  Weisen Sie die Benutzer an anderen *Stationen* an, im Windows-Explorer zu, Laufwerk des Wechseldatenträgers zu navigieren und diesen zu öffnen. Auf dieselbe Weise können auch andere Benutzer Inhalte von ihren eigenen Wechseldatenträgern für Sie freigeben.  
  
## <a name="to-share-content-that-is-stored-on-a-removable-storage-device-by-using-public-folders"></a>So geben Sie Inhalte über öffentliche Ordner frei, die auf einem Wechseldatenträger gespeichert sind  
  
1.  Verbinden Sie den Wechseldatenträger mit einem freien USB-Anschluss des Hostcomputers oder mit einem USB-Hub, der im MultiPoint Services-System nicht als *Stationshub* fungiert.  
2.  Kopieren Sie den freizugebenden Inhalt in einen öffentlichen Ordner im Windows-Explorer, z.B. **Öffentliche Dokumente** in der Bibliothek **Dokumente**.  
  
## <a name="to-privately-work-with-content-that-is-stored-on-a-usb-storage-device"></a>So arbeiten Sie privat mit Inhalten, die auf einem USB-Speichergerät gespeichert sind  
  
Verbinden Sie den Wechseldatenträger mit einem freien USB-Anschluss des Stationshubs.  
  
## <a name="see-also"></a>Weitere Informationen  
[Schützen von Dateien](Keep-Files-Private.md)  
[Freigeben von Dateien](Share-Files.md)  
[Verwalten von Benutzerdateien](Manage-User-Files.md)