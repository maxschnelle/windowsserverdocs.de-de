---
title: Ersetzen der Liste von Domänennamenanbietern
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 104d0412-2d77-4cd4-99f7-65a885522850
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c087cdad4d2c047db40b370673fb04b232036b61
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433493"
---
# <a name="replace-the-list-of-domain-name-providers"></a>Ersetzen der Liste von Domänennamenanbietern

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Mit den folgenden Schritten können Sie die Liste der Domänennamenanbieter ersetzen, die im Assistenten zum Einrichten von Domänennamen angezeigt wird:  


-   [Erstellen der referenzdienstdateien](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [Erstellen der referenzdienstdateien](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  

-   [Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  


###  <a name="BKMK_ReferralFiles"></a> Erstellen der referenzdienstdateien  
 Das Verwaltungstool für den Referenzdienst erstellt eine Reihe von Dateien, mit denen die Liste der Domänennamenanbieter definiert wird, die im Assistenten zum Einrichten von Domänennamen angezeigt werden. Eine XML-formatierte Datei wird für jede Region weltweit erstellt und enthält Informationen für die Domänennamenanbieter, die Sie im Tool angeben. Die vom Tool erstellten Dateien müssen sich in einem Ordner befinden, auf den über eine sichere Verbindung (HTTPS) zugegriffen werden kann, die Sie über das Internet verwalten.  

##### <a name="to-create-the-referral-files"></a>So erstellen Sie Referenzdateien  

1.  Öffnen Sie das Verwaltungstool für den Referenzdienst.  

2.  Klicken Sie auf **Hinzufügen**.  

3.  Geben Sie im Dialogfeld "Domänennamenanbieter hinzufügen" den Namen des Domänennamenanbieters ein.  

4.  Fügen Sie die Domänen der obersten Ebene hinzu, die vom Domänennamenanbieter unterstützt werden. Dazu können Sie auf **Hinzufügen**klicken, den Domänenbezeichner der obersten Ebene eingeben und dann die unterstützten Regionen auswählen. Sie können **Alle Regionen** auswählen.  

5.  Geben Sie die Beschreibung des Domänennamenanbieters ein.  

6.  Fügen Sie die URLs für alle Websites hinzu, die mit dem Domänennamenanbieter verbunden sind.  

7.  Wenn für den Domänennamenanbieter ein Logo verfügbar ist, fügen Sie das Logo hinzu, indem Sie auf **Logo ändern** klicken.  

8.  Klicken Sie auf **Speichern**.  

9. Wiederholen Sie die Schritte 2 bis 8 für alle Domänennamenanbieter, die Sie der Liste im Assistenten hinzufügen möchten.  

10. Nachdem Sie alle Domänennamenanbieter hinzugefügt haben, wählen Sie den Ordner für die Referenzdateien aus. Beachten Sie bei der Auswahl eines Ordners, dass auf die Referenzdateien über eine HTTPS-Verbindung zugegriffen werden muss.  

11. Klicken Sie auf **Dateien für das Dateisystem generieren**.  

###  <a name="BKMK_AddRegistry"></a> Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer  
 Ein Registrierungseintrag muss hinzugefügt werden, um anzugeben, wo das Betriebssystem die Referenzdienstdateien finden kann.  

##### <a name="to-add-a-key-to-the-registry"></a>So fügen Sie einen Schlüssel zur Registrierung hinzu  

1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit**ein, und drücken Sie die **Eingabetaste**.  

2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, dann **Domain Managers** und schließlich **Providers**.  

3.  Klicken Sie mit der rechten Maustaste auf den Schlüssel **E423C85D-6B1F-4583-95E0-449D8263BAC4**, und klicken Sie anschließend auf **Zeichenfolgenwert**.  

4.  Geben Sie **ReferralServerHttpsUri** als Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  

5.  Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **ReferralServerHttpsUri**, und klicken Sie dann auf **Ändern**.  


6.  Geben Sie die HTTPS-URL ein, die für den Zugriff auf die in [Erstellen der Referenzdienstdateien](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles) erstellten Referenzdateien verwendet wird, und klicken Sie dann auf **OK**.  

6.  Geben Sie die HTTPS-URL ein, die für den Zugriff auf die in [Erstellen der Referenzdienstdateien](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles) erstellten Referenzdateien verwendet wird, und klicken Sie dann auf **OK**.  


~~~
> [!IMPORTANT]
>  A slash (/) is required at the end of the URL.  
~~~

###  <a name="BKMK_ReplaceDomainNameProviders"></a> Domänennamen-statusprobleme  
 Wenn ein Partner domänennamenanbieter hinzufügt und eine Anwendungsprogrammierschnittstelle (API) in Windows Server Essentials SDK verwendet, um die Status unbekannt, Fehler und "certificaterequestnotsubmitted" für das Zertifikat festzulegen, erhält der Kunde ein falsches Meldungs- und konfigurationsergebnis. Der Grund hierfür ist, dass die Fälle von Ausnahmen behandelt werden und kein Status zurückgegeben wird.  

 Die folgenden Statusangaben für Domänen sind falsch und sollten als Fehler gemeldet werden:  

- Failed  

- PendingCustomerInterventionRequired  

- PurchaseFailed  

- DomainNotFound  

- InRenewalCustomerInterventionRequired  

- RenewalFailed  

  Die folgenden Statusangaben für Domänen sind korrekt und sollten als Erfolg gemeldet werden:  

- Bereit  

- Pending  

- InRenewal  

## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

