---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Hinzufügen einer Beschreibung für die Anmeldeseite
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 033663720750ee2990cbc6eb4dd0c6d9abe1a002
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962634"
---
# <a name="add-sign-in-page-description"></a>\-Beschreibung der Anmeldeseite hinzufügen

## <a name="to-add-sign-in-page-description"></a>So fügen Sie die \- Beschreibung der Anmeldeseite hinzu
\- \- Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um der Anmeldeseite eine Beschreibung der Anmeldeseite hinzuzufügen.

![Anmelde Beschreibung hinzufügen](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

```powershell
Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"
```

> [!IMPORTANT]
> Die Zeichenfolge für den `SignInPageDescriptionText`-Parameter unterstützt reines HTML mit und ohne Tags. Aus diesem Grund können Sie auch das folgende Cmdlet ausführen, ohne das p-Tag zu verwenden &lt; &gt; .  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." `

Nachdem die Anmelde \- Seite angepasst ist, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, sollten diese zunächst mit einem Gebiets Schema ohne Land konfiguriert werden, \- z. b. "en", bevor Sie das Gebiets Schema für Land und Region ( \- z. b. "en \- US") konfigurieren.

## <a name="additional-references"></a>Weitere Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
