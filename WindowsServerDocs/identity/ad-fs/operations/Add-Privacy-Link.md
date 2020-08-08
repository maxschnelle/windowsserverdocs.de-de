---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: Hinzufügen eines Datenschutzlinks
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c0e65053529999b8463223f7654b357464b90642
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954276"
---
# <a name="add-privacy-link"></a>Hinzufügen eines Datenschutzlinks


Verwenden Sie zum Hinzufügen des Datenschutz Links, der auf der Anmeldeseite angezeigt wird \- , das folgende Windows PowerShell-Cmdlet und die folgende Syntax.

![Datenschutz Link hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`


> [!IMPORTANT]
> Der `linkText`-Parameter in diesem Cmdlet ist nur erforderlich, wenn Sie einen anderen Wert als den Standardwert *Privacy* verwenden. Der Vorteil des Standardwerts ist, dass die Seiten für alle Clientgebietsschemata lokalisiert sind. Nachdem die Anmelde \- Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten Sie diese zunächst mit einem Gebiets Schema ohne Land (z. b. \- "en") konfigurieren, bevor Sie das Gebiets Schema für Land und Region ( \- z. b. "en \- US") konfigurieren.

## <a name="additional-references"></a>Weitere Verweise
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
