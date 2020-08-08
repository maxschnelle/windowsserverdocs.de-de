---
title: Anzeigen von DNS-Ressourceneinträgen für eine bestimmte IP-Adresse
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 211dcfdc17cfa81aad7adb1a424a9fadc0c932c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944601"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>Anzeigen von DNS-Ressourceneinträgen für eine bestimmte IP-Adresse

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema können Sie die DNS-Ressourcen Einträge anzeigen, die der gewählten IP-Adresse zugeordnet sind.

Die Mitgliedschaft in **Administratoren** oder einer entsprechenden Gruppe ist die Mindestanforderung für die Durchführung dieses Verfahrens.

### <a name="to-view-resource-records-for-an-ip-address"></a>So zeigen Sie Ressourcen Einträge für eine IP-Adresse an

1.  Klicken Sie in Server-Manager auf **IPAM**. Die IPAM-Client Konsole wird angezeigt.

2.  Klicken Sie im Navigationsbereich unter **IP-Adressraum**auf **IP-Adress bestand**. Klicken Sie im unteren Navigationsbereich auf **IPv4** oder **IPv6**. Der IP-Adress Bestand wird in der Such Ansicht des Anzeige Bereichs angezeigt. Suchen Sie die IP-Adresse, deren DNS-Ressourcen Einträge Sie anzeigen möchten, und wählen Sie Sie aus.

    ![IP-Adress bestand anzeigen](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)

3.  Klicken Sie in der **Detailansicht**des Anzeige Bereichs auf **DNS-Ressourcen Einträge**. Die Ressourcen Einträge, die der ausgewählten IP-Adresse zugeordnet sind, werden angezeigt.

    ![Anzeigen von DNS-Ressourcen Einträgen](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)

## <a name="see-also"></a>Weitere Informationen
Verwaltung von DNS- [Ressourcen](DNS-Resource-Record-Management.md) 
 Einträgen [Verwalten von IPAM](Manage-IPAM.md)



