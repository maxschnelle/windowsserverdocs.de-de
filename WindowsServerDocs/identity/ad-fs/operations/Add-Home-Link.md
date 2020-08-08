---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Hinzufügen eines Startseitenlinks
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4bd64d19f5e203086c4a5576f331fde9d1b33cf7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954286"
---
# <a name="add-home-link"></a>Hinzufügen eines Startseitenlinks

Verwenden Sie zum Hinzufügen des Start Links, der auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax.


![Start Link hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home `


> [!IMPORTANT]
> Der `linkText`-Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Home* verwenden. Der Vorteil des Standardwerts ist, dass er für alle Clientgebietsschemata lokalisiert ist. Nachdem die Anmelde \- Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten.

## <a name="additional-references"></a>Weitere Verweise
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
