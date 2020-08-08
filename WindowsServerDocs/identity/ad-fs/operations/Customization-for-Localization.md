---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: Anpassung für die Lokalisierung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 41a540b43fde264718ca7aa81ba0e48184cf1265
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956387"
---
# <a name="customization-for-localization"></a>Anpassung für die Lokalisierung

Eine Lokalisierung von Webinhalten in andere Sprachen als Englisch ist möglich. Berücksichtigen bei der Lokalisierung die folgenden Überlegungen.

Nachdem die Inhalte angepasst sind, hat die Anpassung Vorrang, daher sollten Sie für alle Sprachen anpassen, die Sie unterstützen möchten. Alle angepassten Inhalte übernehmen einen Locale-Parameter. Wenn Sie lokalisierte Inhalte konfigurieren, konfigurieren Sie Sie zunächst mit einem \- Gebiets Schema ohne Land, z. b. "en", bevor Sie ein Gebiets Schema für Länder und Regionen \- wie z. b. "en \- US" konfigurieren.

Im Folgenden sind einige weitere Codebeispiele aufgeführt.

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}
Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}
```

Im Folgenden sind einige weitere Codebeispiele aufgeführt.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"

Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"
```

Wenn Sie die Webinhalte an andere Sprachen als Englisch anpassen möchten, für die die Eingabe von Unicode erforderlich ist, empfiehlt es sich, dass Sie die Windows PowerShell ISE verwenden. Weitere Informationen finden Sie [unter Einführung in die Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Weitere Verweise

[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
