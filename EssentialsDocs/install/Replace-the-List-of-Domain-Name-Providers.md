---
title: "Die Liste der Domänennamenanbieter ersetzen"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: ebaef0f88456f61fa229c9a18ee8014987fe7fa7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="replace-the-list-of-domain-name-providers"></a>Die Liste der Domänennamenanbieter ersetzen

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können die Liste der domänennamenanbieter ersetzen, die in den Domain Name-Assistenten angezeigt wird, indem Sie die folgenden Aufgaben:  
  

-   [Erstellen der referenzdienstdateien Service-Dateien](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer](Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

-   [Erstellen der referenzdienstdateien Service-Dateien](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles)  
  
-   [Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_AddRegistry)  

  
###  <a name="BKMK_ReferralFiles"></a>Erstellen der referenzdienstdateien Service-Dateien  
 Der Referenzdienst erstellt eine Reihe von Dateien, die verwendet werden, um die Liste der domänennamenanbieter definieren, die in den Domain Name-Assistenten angezeigt werden. Eine XML-formatierte Datei wird für jede Region weltweit erstellt und enthält Informationen für die domänennamenanbieter, die Sie im Tool angeben. Die Dateien, die vom Tool erstellt werden müssen sich in einem Ordner befinden, die über eine sichere Verbindung (HTTPS) zugegriffen werden kann, die Sie über das Internet verwalten.  
  
##### <a name="to-create-the-referral-files"></a>Erstellen Sie die Referenzdateien  
  
1.  Öffnen Sie den Referenzdienst.  
  
2.  Klicken Sie auf **hinzufügen**.  
  
3.  Geben Sie in einem Dialogfeld Domänennamenanbieter hinzufügen den Namen des domänennamenanbieters ein.  
  
4.  Fügen Sie die Domänen der obersten Ebene, die durch die domänennamenanbieter unterstützt werden. Klicken Sie dazu **hinzufügen**, den Domänenbezeichner der obersten Ebene eingeben und dann die unterstützten Regionen auswählen. Sie können auswählen, **alle Regionen**.  
  
5.  Geben Sie die Beschreibung des domänennamenanbieters ein.  
  
6.  Fügen Sie die URLs für alle Websites, die mit dem domänennamenanbieter verbunden sind.  
  
7.  Wenn ein Logo für die domänennamenanbieter verfügbar ist, fügen Sie das Logo, indem Sie auf **Logo ändern**.  
  
8.  Klicken Sie auf **speichern**.  
  
9. Wiederholen Sie die Schritte2 bis 8 für alle domänennamenanbieter, die Sie im Assistenten zum anbieten möchten.  
  
10. Nachdem Sie alle domänennamenanbieter hinzugefügt haben, wählen Sie den Ordner, in denen die Referenzdateien gespeichert werden sollen. Beachten Sie, wenn Sie einen Ordner auswählen, die die Referenzdateien über eine HTTPS-Verbindung zugegriffen werden müssen.  
  
11. Klicken Sie auf **Dateien für das Dateisystem generieren**.  
  
###  <a name="BKMK_AddRegistry"></a>Fügen Sie einen Eintrag in der Registrierung auf dem Referenzcomputer  
 Ein Registrierungseintrag muss hinzugefügt werden, um anzugeben, in denen das Betriebssystem die referenzdienstdateien finden kann.  
  
##### <a name="to-add-a-key-to-the-registry"></a>Hinzufügen eines Schlüssels zur Registrierung  
  
1.  Klicken Sie auf dem Referenzcomputer auf **starten**, geben Sie **Regedit**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**, erweitern Sie **Manager**, und erweitern Sie dann **Anbieter**.  
  
3.  Mit der rechten Maustaste die **E423C85D-6B1F-4583-95E0-449D8263BAC4** Taste, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
4.  Typ **ReferralServerHttpsUri** für den Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  
  
5.  Mit der rechten Maustaste die neue **ReferralServerHttpsUri** im rechten Bereich eine Zeichenfolge, und klicken Sie dann auf **ändern**.  
  

6.  Geben Sie die HTTPS-URL, die verwendet wird, um den Zugriff auf die in erstellte [Erstellen der referenzdienstdateien Dienstdateien](Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles), und klicken Sie dann auf **OK**.  

6.  Geben Sie die HTTPS-URL, die verwendet wird, um den Zugriff auf die in erstellte [Erstellen der referenzdienstdateien Dienstdateien](../install/Replace-the-List-of-Domain-Name-Providers.md#BKMK_ReferralFiles), und klicken Sie dann auf **OK**.  

  
    > [!IMPORTANT]
    >  Ein Schrägstrich (/) ist am Ende der URL erforderlich.  
  
###  <a name="BKMK_ReplaceDomainNameProviders"></a>Domänennamen-statusprobleme  
 Wenn ein Partner domänennamenanbieter hinzufügt und eine Anwendungsprogrammierschnittstelle (API) im SDK für Windows Server Essentials verwendet, um den Status "unbekannt, Fehler und CertificateRequestNotSubmitted" für das Zertifikat festzulegen, erhält der Kunde eine nicht korrekte Fehlermeldung und Ergebnis. Dies ist, da die Fälle von Ausnahmen behandelt werden und kein Status zurückgegeben.  
  
 Die folgenden Statusangaben sind falsch und sollten als Fehler gemeldet werden:  
  
-   Fehler bei  
  
-   PendingCustomerInterventionRequired  
  
-   PurchaseFailed  
  
-   DomainNotFound  
  
-   InRenewalCustomerInterventionRequired  
  
-   RenewalFailed  
  
 Die folgenden Statusangaben sind korrekt und sollten als Erfolg gemeldet werden:  
  
-   Bereit  
  
-   Ausstehende  
  
-   InRenewal  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

