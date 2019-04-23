---
title: Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: dougkim
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/26/2018
ms.openlocfilehash: 2bdd03636d1cbbcf5b0355358cbedeb63f97af1b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834221"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, zum Konfigurieren der Windows-Verwaltungsinstrumentation (Certificate Revocation List, CRL) Verteilungspunkt (CDP) und die Einstellungen (Authority Information Access, AIA) CA1.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der Domänen-Admins sein.  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren die CDP- und AIA-Erweiterungen auf CA1  
  
1.  Klicken Sie in Server-Manager auf **Extras** und dann auf **Zertifizierungsstelle**.  
  
2.  In der Konsolenstruktur der Zertifizierungsstelle mit der Maustaste **corp-CA1-CA**, und klicken Sie dann auf **Eigenschaften**.  
  
    > [!NOTE]  
    > Der Name der Zertifizierungsstelle unterscheidet sich, wenn Sie nicht den Namen des Computers CA1 und Ihren Domänennamen unterscheiden, die in diesem Beispiel wird. Der Name der Zertifizierungsstelle hat das Format *Domäne*-*CAComputerName*- Zertifizierungsstelle.  
  
3.  Klicken Sie auf die Registerkarte **Erweiterungen**. Sicherstellen, dass **Erweiterung auswählen** nastaven NA hodnotu **(CRL Distribution Point, CDP)**, und klicken Sie in der **Geben Sie Speicherorte, die von dem Benutzer eine Zertifikatsperrliste (CRL) abrufen können**, Führen Sie folgende:  
  
    1.  Wählen Sie den Eintrag `file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    2.  Wählen Sie den Eintrag `https://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    3.  Wählen Sie den Eintrag, der mit dem Pfad beginnt `ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
4.  In **Geben Sie Speicherorte, die von dem Benutzer eine Zertifikatsperrliste (CRL) abrufen können**, klicken Sie auf **hinzufügen**. Die **-Ort hinzufügen** Dialogfeld wird geöffnet.  
  
5.  In **-Ort hinzufügen**im **Speicherort**, Typ `https://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **OK**. Wird das Dialogfeld Eigenschaften von Zertifizierungsstelle.  
  
6.  Auf der **Erweiterungen** Registerkarte, die folgenden Kontrollkästchen:  
  
    -   **In Sperrlisten einbeziehen. Clients mit diesem Parameter finden Sie die Speicherorte der Delta-Zertifikatsperrliste**  
  
    -   **In CDP-Erweiterung der ausgestellten Zertifikate einbeziehen**  
  
7.  In **Geben Sie Speicherorte, die von dem Benutzer eine Zertifikatsperrliste (CRL) abrufen können**, klicken Sie auf **hinzufügen**. Die **-Ort hinzufügen** Dialogfeld wird geöffnet.  
  
8.  In **-Ort hinzufügen**im **Speicherort**, Typ `file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`, und klicken Sie dann auf **OK**. Wird das Dialogfeld Eigenschaften von Zertifizierungsstelle.  
  
9. Auf der **Erweiterungen** Registerkarte, die folgenden Kontrollkästchen:  
  
    -   **Veröffentlichen von CRLs an diesem Ort**  
  
    -   **Veröffentlichen von Delta-CRLs an diesem Ort**  
  
10. Änderung **Erweiterung auswählen** zu **(Authority Information Access, AIA)**, und klicken Sie in der **Geben Sie Speicherorte, die von dem Benutzer eine Zertifikatsperrliste (CRL) abrufen können**, sind Das folgende:  
  
    1.  Wählen Sie den Eintrag, der mit dem Pfad beginnt `ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    2.  Wählen Sie den Eintrag `https://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
    3.  Wählen Sie den Eintrag `file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt`, und klicken Sie dann auf **entfernen**. In **Entfernen bestätigen**, klicken Sie auf **Ja**.  
  
11. In **geben Standorte, von denen Benutzer das Zertifikat für diese Zertifizierungsstelle erhalten**, klicken Sie auf **hinzufügen**. Die **-Ort hinzufügen** Dialogfeld wird geöffnet.  
  
12. In **-Ort hinzufügen**im **Speicherort**, Typ `https://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt`, und klicken Sie dann auf **OK**. Wird das Dialogfeld Eigenschaften von Zertifizierungsstelle.  
  
13. Auf der **Erweiterungen** Registerkarte **in die AIA des ausgestellten Zertifikats einbeziehen**.  
  
14. Wenn Sie dazu aufgefordert werden, um Active Directory-Zertifikatdienste neu zu starten, klicken Sie auf **keine**. Sie werden den Dienst später neu starten.  
  

