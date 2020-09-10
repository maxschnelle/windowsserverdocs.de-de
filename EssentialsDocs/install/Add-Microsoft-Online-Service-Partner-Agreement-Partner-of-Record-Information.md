---
title: Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 0f8a1b769b207bd40add46f3e7e9273c67409ac1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624046"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Hinzufügen von Informationen zum zuständigen Partner im Rahmen des Microsoft Online Services-Partnervertrags

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>
 Wenn Sie ein Microsoft Online Services-Partner Vertragspartner (Microsoft Online Services Partner Agreement, Microsoft) für Microsoft 365 sind, müssen Sie einen Registrierungsschlüssel erstellen, der Ihre ID (Partner-of-Record Identification, por ID) enthält, um sicherzustellen, dass Sie ordnungsgemäß kompensiert werden, wenn eine Abonnement Anforderung über das Microsoft 365-Integrationsmodul von Windows Server Essentials stammt. Die folgenden Informationen werden gelesen und über die Microsoft 365 Registrierungs-URLs an den Dienstanbieter weitergeleitet.

-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO

-   Typ = Zeichenfolge

-   Schlüsselname = Partner

-   Wert = xxxxx, wobei xxxxx die POR ID ist

#### <a name="to-add-the-por-id-key-to-the-registry"></a>So fügen Sie der Registrierung den Schlüssel für die POR ID hinzu

1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit** ein, und drücken Sie dann die EINGABETASTE.

2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, dann **Microsoft** und schließlich **Windows Server**.

3.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.

4.  Geben Sie **MSO** als Schlüsselnamen ein.

5.  Klicken Sie mit der rechten Maustaste auf den gerade erstellten Schlüssel, und klicken Sie dann auf **Zeichenfolgenwert**.

6.  Geben Sie **Partner** als Namen der Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.

7.  Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Partner**, und klicken Sie dann auf **Ändern**.

8.  Geben Sie im Feld **Wert** die POR ID ein, und klicken Sie anschließend auf **OK**.

## <a name="see-also"></a>Weitere Informationen

 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)

