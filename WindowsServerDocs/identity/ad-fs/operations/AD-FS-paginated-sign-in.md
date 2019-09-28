---
title: AD FS paginierte Anmeldung
description: In diesem Dokument wird die neue Anmelde Funktion für AD FS 2019 beschrieben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ca13ebe29b0a9260302599110f333d166681abdb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358559"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS paginierte Anmeldung


Für AD FS in Windows Server 2019 haben wir die Anmelde Benutzeroberfläche umgestaltet.  Nun hat das AD FS Anmeldung dasselbe Aussehen und Gefühl Azure AD.  Dadurch erhalten Benutzer eine konsistentere Anmelde Leistung, die einen zentrierten und paginierten benutzerflow umfasst.

## <a name="whats-changing"></a>Änderungen
In AD FS in Windows Server 2012 R2 und 2016 hat ihr Anmeldebildschirm etwa wie folgt aussehen:

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

Wir wechseln von der Anzeige eines einzelnen Formulars, das sich auf der rechten Seite des Bildschirms befindet.

In AD FS in Windows Server 2019 sind dies die wichtigsten Entwurfs Änderungen, die Sie sehen:


- **Eine zentrierte Benutzeroberfläche**. Zuvor war die Anmelde Benutzeroberfläche auf der rechten Seite des Bildschirms vorhanden, wie oben gezeigt. Wir haben die Benutzeroberfläche vor und zentriert verschoben, um die Benutzererfahrung zu modernisieren.
- **Paginierung**. Anstatt Ihnen eine lange Form zum Ausfüllen bereitzustellen, haben wir einen neuen Flow integriert, der Sie Schritt für Schritt durch den Anmeldevorgang führt. Unsere Telemetrie zeigt, dass unsere Kunden bei diesem Ansatz eine größere Anzahl erfolgreicher Anmeldungen aufweisen. Außerdem bietet Sie mehr Flexibilität bei der Integration verschiedener Authentifizierungsmethoden, z. b. der Authentifizierung von US-Telefon Faktoren.

![neusignin](media/AD-FS-paginated-sign-in/signin2.png)

Auf der ersten Seite werden Sie aufgefordert, Ihren Benutzernamen einzugeben. Sie können auch die Option "angemeldet bleiben" auswählen, um die Häufigkeit der Anmeldeaufforderungen zu verringern und angemeldet zu bleiben, wenn dies sicher ist. (Diese Option ist standardmäßig deaktiviert.)

![neusignin](media/AD-FS-paginated-sign-in/signin3.png)

Auf der zweiten Seite werden die von Ihrem Administrator konfigurierten Authentifizierungs Optionen angezeigt. Wenn die Option externe Authentifizierung als primär zulassen aktiviert ist, wird diese ebenfalls eingeschlossen.

![neusignin](media/AD-FS-paginated-sign-in/signin4.png)

Auf der dritten Seite werden Sie aufgefordert, Ihr Kennwort einzugeben (vorausgesetzt, Sie haben als Authentifizierungs Option "Kennwort" ausgewählt).

## <a name="how-to-get-the-new-experience"></a>So erhalten Sie die neue Funktion

### <a name="new-installation-of-ad-fs"></a>Neue Installation von AD FS
Wenn Sie ein neuer Kunde sind AD FS, erhalten Sie den neuen Entwurf standardmäßig.

### <a name="upgrading-a-farm"></a>Aktualisieren einer Farm
Wenn Sie ein vorhandener Kunde AD FS 2012 R2 oder 2016 sind, gibt es zwei Möglichkeiten, den neuen Entwurf nach dem Upgrade der Server auf AD FS 2019 zu erhalten und den FBL auf 2019 zu aktivieren.

- Hiermit wird die neue Anmeldung über PowerShell zugelassen. Führen Sie den folgenden Befehl aus, um die Paginierung zu aktivieren:``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Aktivieren Sie die externe Authentifizierung als primär, entweder über PowerShell oder über die AD FS Server-Manager. Die neuen paginierten Anmelde Seiten werden aktiviert, wenn dieses Feature aktiviert ist.
Wenn Sie ein neuer Kunde sind AD FS, erhalten Sie den neuen Entwurf standardmäßig. Wenn Sie jedoch ein vorhandener Kunde mit AD FS 2012 R2 oder 2016 sind, müssen Sie mehrere Schritte ausführen, um den neuen Entwurf zu erhalten:``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>Anpassung
Die Anpassungsoptionen gelten weiterhin für AD FS 2019.
Im folgenden finden Sie einige Links zu anderen Dokumenten für Ihre Referenz.

• Für diejenigen, die nicht beabsichtigen, Ihre Server auf AD FS 2019 zu aktualisieren, aber trotzdem den neuen Entwurf wünschen: [Verwenden eines Azure AD UX-Webdesigns in Active Directory-Verbunddienste (AD FS)](azure-ux-web-theme-in-ad-fs.md)

• Ein zentraler Speicherort für die Anpassung: [AD FS: Anpassung der Benutzeranmeldung](ad-fs-user-sign-in-customization.md)
