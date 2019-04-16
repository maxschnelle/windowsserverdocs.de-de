---
title: Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 80f6d68816a58b2ac30010e0917ce0f816a30234
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können dieses Verfahren verwenden, so konfigurieren Sie die Windows-Verwaltungsinstrumentation (Certificate Revocation List, CRL) Verteilungspunkt (CDP) und die Einstellungen (Authority Information Access, AIA) für Zertifizierungsstelle 1.  
  
Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Domänen-Admins sein.  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren die CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1  
  
1.  Klicken Sie im Server-Manager auf **Tools** , und klicken Sie dann auf **Zertifizierungsstelle**.  
  
2.  In der Konsolenstruktur der Zertifizierungsstelle mit der rechten Maustaste **corp-Zertifizierungsstelle 1-CA**, und klicken Sie dann auf **Eigenschaften**.  
  
    > [!NOTE]  
    > Der Name der Zertifizierungsstelle unterscheidet sich, wenn Sie nicht den Namen des Computers CA1 und Ihren Domänennamen sich in diesem Beispiel unterscheidet. Der Name der Zertifizierungsstelle wird im Format *Domäne*-*CAComputerName*-Zertifizierungsstelle.  
  
3.  Klicken Sie auf die **Erweiterungen** Registerkarte sicher, dass **Erweiterung auswählen** festgelegt ist **(CRL Distribution Point, CDP)**, und in der Speicherorte, von denen Benutzer eine Zertifikatsperrliste (CRL), gehen Sie folgendermaßen vor:  
  
    1.  Wählen Sie den Eintrag `file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    2.  Wählen Sie den Eintrag `http:\/\/<ServerDNSName>\/CertEnroll\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    3.  Wählen Sie den Eintrag, der mit dem Pfad startet `ldap:\/\/CN\=<CATruncatedName><CRLNameSuffix>,CN\=<ServerShortName>`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
4.  In **Speicherorte, von denen Benutzer eine Zertifikatsperrliste (CRL) erhalten können**, klicken Sie auf **hinzufügen**. Die **Speicherort hinzufügen** Dialogfeld wird geöffnet.  
  
5.  In **Speicherort hinzufügen**im **Speicherort**, Typ `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **OK**. Dadurch wird Sie im Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
6.  Auf der **Erweiterungen** Registerkarte, die folgenden Kontrollkästchen:  
  
    -   **In CRLs einbeziehen. Clients mit diesem Parameter finden Sie die Speicherorte der Delta-Zertifikatsperrliste**  
  
    -   **In die CDP-Erweiterung des ausgestellten Zertifikats einbeziehen**  
  
7.  In **Speicherorte, von denen Benutzer eine Zertifikatsperrliste (CRL) erhalten können**, klicken Sie auf **hinzufügen**. Die **Speicherort hinzufügen** Dialogfeld wird geöffnet.  
  
8.  In **Speicherort hinzufügen**im **Speicherort**, Typ `file:\/\/\\\\pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **OK**. Dadurch wird Sie im Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
9. Auf der **Erweiterungen** Registerkarte, die folgenden Kontrollkästchen:  
  
    -   **Veröffentlichen von CRLs an diesem Ort**  
  
    -   **Veröffentlichen von Delta-CRLs an diesem Ort**  
  
10. Änderung **Erweiterung auswählen** auf **(Authority Information Access, AIA)**, und in der **Speicherorte, von denen Benutzer eine Zertifikatsperrliste (CRL) erhalten können**, gehen Sie folgendermaßen vor:  
  
    1.  Wählen Sie den Eintrag, der mit dem Pfad startet `ldap:\/\/CN\=<CATruncatedName>,CN\=AIA,CN\=Public Key Services`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    2.  Wählen Sie den Eintrag `http:\/\/<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    3.  Wählen Sie den Eintrag `file:\/\/\\\\<ServerDNSName>\/CertEnroll\/<ServerDNSName>\_<CaName><CertificateName>.crt`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
11. In **Speicherorte, von denen Benutzer eine Zertifikatsperrliste (CRL) erhalten können**, klicken Sie auf **hinzufügen**. Die **Speicherort hinzufügen** Dialogfeld wird geöffnet.  
  
12. In **Speicherort hinzufügen**im **Speicherort**, Typ `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`, und klicken Sie dann auf **OK**. Dadurch wird Sie im Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
13. Auf der **Erweiterungen** Registerkarte **in die AIA des ausgestellten Zertifikats einbeziehen**.  
  
14. In **Speicherort hinzufügen**im **Speicherort**, Typ `file:\/\/\\\\pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`, und klicken Sie dann auf **OK**. Dadurch wird Sie im Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
    > [!IMPORTANT]  
    > Stellen Sie sicher, dass **in die AIA-Erweiterung des ausgestellten Zertifikats einbeziehen** nicht aktiviert ist.  
  
15. Wenn Sie dazu aufgefordert werden, um Active Directory-Zertifikatdienste neu zu starten, klicken Sie auf **keine**. Sie können den Dienst später neu zu starten.  
  


