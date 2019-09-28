---
title: Schützen des Systemvolumes mit Datenträgerschutz
description: Bietet Informationen zum Datenträger Schutz für Multipoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18694665-ed65-4d84-8505-f460cf3df907
author: evaseydl
manager: scotman
ms.author: evas
ms.openlocfilehash: 27bcce68cfe5856e987f5ad93460abd12217c26b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389510"
---
# <a name="protecting-the-system-volume-with-disk-protection"></a>Schützen des Systemvolumes mit Datenträgerschutz
Multipoint Services bietet die Option, alle Änderungen am System Volume jedes Mal, wenn der Computer gestartet wird, unverzüglich zu löschen. Wenn Sie das Datenträger Schutz Feature aktivieren, werden alle Änderungen am Laufwerk, z. b. eine Beschädigung der Konfiguration oder die Einführung von Schadsoftware, beim nächsten Neustart des Computers rückgängig gemacht. Dies ist ein nützliches Feature für Administratoren, die sicherstellen möchten, dass jedes Mal ein bekanntes "gutes" oder "Golden" Software Image geladen wird. Automatische Updates oder das Patchen von Software kann beispielsweise in der Mitte der Nacht geplant werden. Der Planungs Aspekt ist, ob Endbenutzer in der Lage sein sollen, Änderungen, z. b. das Installieren von Software, über das Internet vorzunehmen. Wenn diese Funktion aktiviert ist und Benutzer in der Lage sein sollen, Dateien zu speichern, muss sich die Dateifreigabe außerhalb des System Volume befinden.  
  
