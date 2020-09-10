---
title: Replace Microsoft 365 Integration Module kaufen-try-Endpunkt-URL zur Unterstützung der Microsoft Online Services Reseller Agreement
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: a8a5cf91c6de2971bc8270cc3c7ea92327b71224
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623376"
---
# <a name="replace-microsoft-365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Replace Microsoft 365 Integration Module kaufen-try-Endpunkt-URL zur Unterstützung der Microsoft Online Services Reseller Agreement

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>
 Wenn Sie ein Microsoft Online Service Reseller Agreement-Partner (mosra) sind, müssen Sie die Endpunkt-URLs ersetzen, die vom Windows Server Essentials Microsoft 365-Integrationsmodul verwendet werden, um sicherzustellen, dass die Kunden Registrierungs Transaktionen über Ihr Portal verarbeitet werden.

 Vom Integrationsmodul werden die folgenden vier Endpunkt-URLs verwendet:

1.  Ein Microsoft 365 Enterprise Abonnement-Kauf Endpunkt.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Typ = REG-SZ

    -   Schlüsselname = MOSRASTDBUY

    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Beispiel: Wert = http://syndicatepartner.office365.com/enterprisebuy.html

2.  Ein Microsoft 365 Enterprise-Test Endpunkt für Abonnements.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Typ = REG-SZ

    -   Schlüsselname = MOSRASTDTRY

    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Beispiel: Wert = http://syndicatepartner.office365.com/enterprisetry.html

3.  Einen Microsoft 365 Kauf Endpunkt für einen Small Business Premium-Abonnement.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Typ = REG-SZ

    -   Schlüsselname = MOSRALITEBUY

    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Beispiel: Wert = http://syndicatepartner.office365.com/smallbizbuy.html

4.  Ein Microsoft 365 Test-Endpunkt für Small Business Premium-Abonnements.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Typ = REG-SZ

    -   Schlüsselname = MOSRALITETRY

    -   Wert = *xxxxx*, wobei xxxxx die Abonnement-URL Ihres Unternehmens ist. Beispiel: Wert = http://syndicatepartner.office365.com/smallbiztry.html

#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>So fügen Sie der Registrierung einen Schlüssel für die Endpunkt-URL hinzu

1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit** ein, und drücken Sie dann die EINGABETASTE.

2.  Erweitern Sie im linken Fensterbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** und **MSO**.

3.  Wenn **MSO** nicht vorhanden ist, klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, klicken Sie auf „Schlüssel“, und geben Sie dann **MSO** als Namen des Schlüssels ein.

4.  Klicken Sie mit der rechten Maustaste auf "MSO", und klicken Sie dann auf **Zeichenfolgenwert**. Geben Sie einen der folgenden Zeichenfolgennamen für Endpunkte als Namen der Zeichenfolge ein:

    -   MOSRASTDBUY

    -   MOSRASTDTRY

    -   MOSRALITEBUY

    -   MOSRALITETRY

5.  Klicken Sie im rechten Fensterbereich mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie anschließend auf **Ändern**.

6.  Geben Sie im Feld **Wert** die neue Endpunkt-URL ein, und klicken Sie anschließend auf **OK**.

7.  Wiederholen Sie die Schritte 4 bis 6 für jeden in Schritt 4 aufgeführten Zeichenfolgennamen.

## <a name="see-also"></a>Weitere Informationen

 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)

