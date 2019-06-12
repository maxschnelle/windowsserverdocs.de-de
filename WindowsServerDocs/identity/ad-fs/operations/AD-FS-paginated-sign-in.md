---
title: AD FS paginierten-Anmeldung
description: Dieses Dokument beschreibt die neue Anmeldung für AD FS-2019.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c528b9c4e944849b7ed9a2fc5213a7b263be70c7
ms.sourcegitcommit: ccc802338b163abdad2e53b55f39addcfea04603
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66687378"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS paginierten-Anmeldung


Für AD FS in Windows Server-2019 haben wir die Anmeldeoberfläche neu entworfen.  Jetzt wird die AD FS-Anmeldung das gleiche Aussehen und Verhalten von Azure AD verfügen.  Dadurch erhalten Benutzer eine konsistentere-Anmeldung, zentriert und paginierten benutzerflow integrieren.

## <a name="whats-changing"></a>Was ändert sich
In AD FS in Windows Server 2012 R2 und 2016 sah Ihrer Anmeldeseite etwa wie folgt aus:

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

Wir Verschieben von einem einzigen Formular befindet sich auf der rechten Seite des Bildschirms angezeigt.

In AD FS in Windows Server-2019 sind dies die wichtige entwurfsänderungen an, denen angezeigt werden:


- **Ein zentriert UI**. Zuvor war die Anmeldeoberfläche auf der rechten Seite des Bildschirms vorhanden, wie oben gezeigt. Wir haben die Benutzeroberfläche und in den Mittelpunkt, die Oberfläche zu modernisieren verschoben.
- **Die Paginierung**. Statt Sie eine lange Form ausfüllen, haben wir einen neuen Datenfluss hinzugefügt, mit der Sie über den Anmeldevorgang schrittweise gelangen. Unsere Telemetrie angezeigt, dass bei diesem Ansatz unseren Kunden noch erfolgreicher Anmeldungen. Darüber hinaus werden wir mehr Flexibilität hinsichtlich der verschiedenen Authentifizierungsmethoden, wie Telefon-Factor Authentication integrieren.

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

Auf der ersten Seite werden Sie aufgefordert, Ihren Benutzernamen einzugeben. Sie können auch auswählen, die Option "Keep me angemeldet" verringern die Häufigkeit von anmeldeaufforderungen und angemeldet bleiben, wenn sie dazu sicher ist. (Diese Option ist standardmäßig deaktiviert.)

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

Klicken Sie auf der zweiten Seite werden Sie mit der Authentifizierungsoptionen, die von Ihrem Administrator konfiguriert angezeigt. Wenn externe Authentifizierung als primäre zulassen aktiviert ist, werden diese ebenfalls berücksichtigt.

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

Auf der dritten Seite werden Sie aufgefordert werden, geben Ihr Kennwort (vorausgesetzt, dass Sie auf "Password" ausgewählt, als Authentifizierung verwenden).

## <a name="how-to-get-the-new-experience"></a>Gewusst wie: Abrufen die neue Oberfläche

### <a name="new-installation-of-ad-fs"></a>Neue Installation von AD FS
Wenn Sie einen neuen Kunden mit AD FS sind, erhalten Sie standardmäßig das neue Design.

### <a name="upgrading-a-farm"></a>Aktualisieren einer farm
Wenn Sie Bestandskunde AD FS 2012 R2 oder 2016 sind, gibt es zwei Möglichkeiten, um das neue Design empfangen wird, nach dem Aktualisieren von Servern mit AD FS-2019 und aktivieren die FBL zu 2019.

- Die neue Anmeldung mithilfe von Powershell zulassen. Führen Sie den folgenden Befehl aus, um die Paginierung zu aktivieren: ``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Aktivieren Sie die externe Authentifizierung als primäres, entweder über Powershell oder über die AD FS-Server-Manager. Die neuen paginierten Anmeldeseiten werden aktiviert werden, wenn dieses Feature aktiviert ist.
Wenn Sie einen neuen Kunden mit AD FS sind, erhalten Sie standardmäßig das neue Design. Wenn Sie Bestandskunde mit AD FS 2012 R2 oder 2016 sind, gibt es jedoch mehrere Schritte, die Sie durchführen müssen, um das neue Design empfangen müssen: ``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>Anpassung
Die Optionen für die Anpassung werden für AD FS-2019 weiterhin angewendet werden.
Im folgenden sind einige Links zu anderen Dokumenten zu Referenzzwecken aus.

• Für diejenigen, die das neue Design möchten aber nicht möchten, aktualisieren Sie ihre Server mit AD FS-2019: [Verwenden ein Azure AD-UX-Web-Design in Active Directory-Verbunddienste](azure-ux-web-theme-in-ad-fs.md)

• Einem zentralen Ort für die Anpassung: [AD FS: Anpassung der Benutzeranmeldung](ad-fs-user-sign-in-customization.md)
