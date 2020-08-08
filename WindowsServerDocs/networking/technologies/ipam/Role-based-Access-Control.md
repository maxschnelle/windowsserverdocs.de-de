---
title: Rollenbasierte Zugriffssteuerung
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f79dc7ab4283de5ab1ec63861d5f543658947964
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944672"
---
# <a name="role-based-access-control"></a>Rollenbasierte Zugriffssteuerung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält Informationen zur Verwendung der rollenbasierten Zugriffs Steuerung in IPAM.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende Dokumentation zur IPAM-Zugriffs Steuerung in diesem Abschnitt verfügbar.
>
> -   [Verwalten der rollenbasierten Zugriffssteuerung mit Server-Manager](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)
> -   [Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)

Mithilfe der rollenbasierten Zugriffs Steuerung können Sie Zugriffsberechtigungen auf unterschiedlichen Ebenen angeben, einschließlich des DNS-Servers, der DNS-Zone und der DNS-Ressourcen Daten Satz Ebenen.
Mithilfe der rollenbasierten Zugriffs Steuerung können Sie angeben, wer über die granulare Kontrolle über Vorgänge zum Erstellen, bearbeiten und löschen verschiedener Typen von DNS-Ressourcen Einträgen verfügt.

Sie können die Zugriffs Steuerung so konfigurieren, dass Benutzer auf die folgenden Berechtigungen beschränkt sind.

-   Benutzer können nur bestimmte DNS-Ressourcen Einträge bearbeiten.

-   Benutzer können DNS-Ressourcen Einträge eines bestimmten Typs bearbeiten, z. b. PTR oder MX.

-   Benutzer können DNS-Ressourcen Einträge für bestimmte Zonen bearbeiten.

## <a name="see-also"></a>Weitere Informationen
[Verwalten von rollenbasierten Access Control mit Server-Manager](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md) 
 [Verwalten von rollenbasierten Access Control mit Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 
 [Verwalten von IPAM](Manage-IPAM.md)



