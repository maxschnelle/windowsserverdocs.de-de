---
title: Speicherplätze – Übersicht
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: 9977bb35be3676e31cdcab7322b5b5a2cfc67609
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832911"
---
# <a name="storage-spaces-overview"></a>Speicherplätze – Übersicht

Speicherplätze sind eine Technologie in Windows und Windows-Server, mit denen Ihre Daten vor Laufwerksfehlern schützen können. Es ist konzeptionell identisch mit RAID, in der Software implementiert. Sie können Speicherplätze verwenden, zum Gruppieren von mindestens drei Laufwerke zusammen in einem Speicherpool, und verwenden Sie dann die Kapazität aus diesem Pool zum Erstellen von Speicherplätzen. Diese wird in der Regel zusätzliche Kopien Ihrer Daten speichern müssen, wenn eines Ihrer Laufwerke ein Fehler auftritt, Sie immer noch eine intakte Kopie Ihrer Daten. Wenn Sie auf der Kapazität erschöpft ist, müssen Sie einfach fügen Sie weitere Laufwerke zum Speicherpool hinzu.

Es gibt vier Arten von Speicherplätzen verwenden:

- **Auf einem Windows-PC** – Weitere Informationen finden Sie unter [Speicherplätze in Windows 10](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10).
- **Auf einem eigenständigen Server mit allen Speicher in einem einzelnen Server** – Weitere Informationen finden Sie unter [Bereitstellen von Speicherplätzen auf einem eigenständigen Server](deploy-standalone-storage-spaces.md).
- **Auf einem Clusterserver mit mit lokaler, direkt angeschlossener Speicher in jedem Cluster "direkte Speicherplätze"** – Weitere Informationen finden Sie unter ["direkte Speicherplätze" Übersicht über die](storage-spaces-direct-overview.md).
- **Auf einem Clusterserver mit ein oder mehrere shared SAS Speichergehäuse, enthält alle Laufwerke** – Weitere Informationen finden Sie unter [Speicherplätze auf einem Cluster mit freigegebenen SAS-Übersicht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11)).

