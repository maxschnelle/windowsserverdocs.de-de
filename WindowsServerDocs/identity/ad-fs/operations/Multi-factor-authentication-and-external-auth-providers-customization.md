---
title: Multi-Factor Authentication und externe Authentifizierungs Anbieter Anpassung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: c4c775ac330c1a5f81bf97f1f6aa29204efbf75c
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519729"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>Multi-Factor Authentication und externe Authentifizierungs Anbieter Anpassung

In AD FS wird die Unterstützung für die mehrstufige Authentifizierung standardmäßig bereitgestellt \- \- \- . Beispielsweise können Sie AD FS für die Verwendung der integrierten \- Zertifikat Authentifizierung als zweistufige Authentifizierung konfigurieren. Sie können auch externe Authentifizierungsanbieter verwenden. Mit diesem Ansatz können AD FS in zusätzliche Dienste wie Azure Multi-Factor Authentication integriert werden, oder Sie können einen eigenen Anbieter entwickeln. Weitere Informationen zum Registrieren eines externen Authentifizierungs Anbieters mithilfe von AD FS finden Sie unter [Lösungs Handbuch: Verwalten von Risiken mit Multi- \- Factor Access Control](./manage-risk-with-conditional-access-control.md) .

Es wird empfohlen, dass ein externer Authentifizierungs Anbieter die Klassen verwendet, die in der CSS-Datei definiert sind, die AD FS bereitstellt, um die Authentifizierungs Benutzeroberfläche zu erstellen. Mit dem folgenden Cmdlet können Sie das Standardwebdesign exportieren und die Benutzeroberflächenklassen und -elemente inspizieren, die in der CSS-Datei definiert sind. Die CSS-Datei kann bei der Entwicklung der Anmelde \- Benutzeroberfläche eines externen Authentifizierungs Anbieters verwendet werden.

```powershell
Export-AdfsWebTheme -Name default -DirectoryPath C:\theme
```

Im folgenden finden Sie ein Beispiel für die \- Benutzeroberfläche für die Anmeldung, die rot hervorgehoben ist, von einem externen Authentifizierungs Anbieter. Die Benutzeroberfläche verwendet die UI-Klassen in der AD FS. CSS-Datei.

![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)

Bevor Sie eine neue benutzerdefinierte Authentifizierungsmethode schreiben, empfiehlt es sich, die AD FS Design-und Formatvorlagen Definitionen zu untersuchen, um die Anforderungen an die Inhaltserstellung zu verstehen.

-   Bei einer benutzerdefinierten Authentifizierungsmethode wird nur ein HTML-Segment auf der AD FS Anmelde \- Seite und nicht auf der vollständigen Seite angezeigt. Verwenden Sie die Format Definition AD FS, um das konsistente Aussehen und Verhalten zu erzielen.

![AD FS und MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)

-   Beachten Sie, dass AD FS Administratoren die AD FS Stile anpassen können. . Eine Hartcodierung eigener Formatvorlagen wird nicht empfohlen. Stattdessen empfiehlt es sich, nach Möglichkeit AD FS Stile zu verwenden.

-   Standard \- mäßig \- werden AD FS Stile von Links \- nach \- rechts im \( Ltr \) -Stil und von rechts \- nach links von RTL \- verfasst \( \) . Administratoren können beide anpassen und sprach \- spezifische Stile über die Webdesign Definition bereitstellen. Jedes Stylesheet verfügt über drei Abschnitt mit entsprechenden Kommentaren:

    -   Design **Stile** \- Diese Stile sollten nicht verwendet werden und können nicht verwendet werden. Sie sind für die Definition des Designs für alle Seiten vorgesehen. Sie werden absichtlich von einer Element-ID definiert, damit sie nicht wiederverwendet werden.

    -   **Allgemeine Stile** \- Dies sind die Stile, die für Ihre Inhalte verwendet werden sollen.

    -   **Formfaktor Stile** \- Dabei handelt es sich um Stile für verschiedene Formfaktoren. Sie sollten diesen Abschnitt verstehen, um sicherzustellen, dass Ihre Inhalte mit verschiedenen Formfaktoren arbeiten, beispielsweise Telefone und Tablets.

Weitere Informationen finden Sie unter [Lösungs Handbuch: Verwalten von Risiken mit Multi- \- Factor Access Control](./manage-risk-with-conditional-access-control.md) und [Lösungs Handbuch: Verwalten von Risiken mit zusätzlicher mehrstufiger \- Authentifizierung für sensible Anwendungen](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx).

## <a name="additional-references"></a>Zusätzliche Verweise
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)
