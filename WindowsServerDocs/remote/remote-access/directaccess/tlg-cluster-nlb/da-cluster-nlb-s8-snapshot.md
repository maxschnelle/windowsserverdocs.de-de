---
title: 'Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)'
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c2f458570f4e584be1f73f9825d39d396546edf3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951005"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>Schritt 8: Momentaufnahme des DirectAccess-Clusters (NLB-Konfiguration)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dadurch wird die DirectAccess-Testumgebung abgeschlossen. Gehen Sie folgendermaßen vor, um diese Konfiguration zu speichern, sodass Sie schnell zu einer funktionierenden DirectAccess-Konfiguration mit NLB-Cluster Konfiguration zurückkehren können, mit der Sie andere Test Umgebungs Anleitungen für DirectAccess, Test Umgebungs Anleitungen oder eigene Experimente testen können:

1.  Schließen Sie alle Fenster auf allen physischen oder virtuellen Computern in der Testumgebung, und fahren Sie die Computer dann normal herunter.

2.  Wenn Ihre Testumgebung auf virtuellen Computern basiert, speichern Sie eine Momentaufnahme der einzelnen virtuellen Computer, und benennen Sie die Momentaufnahmen DirectAccess-Cluster und NLB. Wenn Ihr Lab physische Computer verwendet, erstellen Sie Datenträger Images, um die Konfiguration der DirectAccess-Testumgebung zu speichern.
