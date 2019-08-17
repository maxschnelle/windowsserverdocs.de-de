---
title: Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: dougkim
ms.topic: article
ms.assetid: f77a3989-9f92-41ef-92a8-031651dd73a8
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/26/2018
ms.openlocfilehash: 74d77347e0ca1dffbca4e2cf6f17b9faa25d55bf
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560495"
---
# <a name="configure-the-cdp-and-aia-extensions-on-ca1"></a>Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie die Zertifikat Sperr Listen-Verteilungs Punkte (CRL) und die AIA-Einstellungen (Authority Information Access) auf CA1 konfigurieren.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.  
  
#### <a name="to-configure-the-cdp-and-aia-extensions-on-ca1"></a>So konfigurieren Sie die CDP-und AIA-Erweiterungen auf CA1  
  
1.  Klicken Sie in Server-Manager auf **Extras** und dann auf **Zertifizierungsstelle**.  
  
2.  Klicken Sie in der Konsolen Struktur der Zertifizierungsstelle mit der rechten Maustaste auf **Corp-CA1-ca**, und klicken Sie dann auf **Eigenschaften**.  
  
    > [!NOTE]  
    > Der Name der Zertifizierungsstelle ist anders, wenn Sie den Computer nicht benennen CA1 und der Domänen Name unterscheidet sich von dem in diesem Beispiel. Der Name der Zertifizierungsstelle hat das Format *Domäne*-*CAComputername*-ca.  
  
3.  Klicken Sie auf die Registerkarte **Erweiterungen**. Stellen Sie sicher, dass die Option **Erweiterung auswählen** auf **CRL-Verteilungs Punkt (CDP)** festgelegt ist, und führen Sie in den Speicher **Orten, von denen Benutzer eine Zertifikat Sperr Liste abrufen können**, folgende Schritte aus:  
  
    1.  Wählen Sie den `file://\\<ServerDNSName>\CertEnroll\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`Eintrag aus, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
    2.  Wählen Sie den `http://<ServerDNSName>/CertEnroll/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`Eintrag aus, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
    3.  Wählen Sie den Eintrag aus, der mit `ldap:///CN=<CATruncatedName><CRLNameSuffix>,CN=<ServerShortName>`dem Pfad beginnt, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
4.  Klicken Sie in Speicher **Orte angeben, von denen Benutzer eine Zertifikat Sperr Liste abrufen können (CRL)** auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.  
  
5.  Geben`http://pki.corp.contoso.com/pki/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`Sie unter **Speicherort hinzufügen**in **Speicherort**ein, und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
6.  Aktivieren Sie auf der Registerkarte **Erweiterungen** die folgenden Kontrollkästchen:  
  
    -   **In CRLs einschließen. Clients finden die Speicherorte der Delta-CRLs mithilfe dieser Informationen**  
  
    -   **In die CDP-Erweiterung der ausgestellten Zertifikate einbeziehen**  
  
7.  Klicken Sie in Speicher **Orte angeben, von denen Benutzer eine Zertifikat Sperr Liste abrufen können (CRL)** auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.  
  
8.  Geben`file://\\pki.corp.contoso.com\pki\<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`Sie unter **Speicherort hinzufügen**in **Speicherort**ein, und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
9. Aktivieren Sie auf der Registerkarte **Erweiterungen** die folgenden Kontrollkästchen:  
  
    -   **Veröffentlichen von CRLs an diesem Speicherort**  
  
    -   **Delta-CRLs an diesem Speicherort veröffentlichen**  
  
10. Ändern **Sie SELECT Extension** to **Authority Information Access (AIA)** , und führen Sie in den Speicher **Orten, von denen Benutzer eine Zertifikat Sperr Liste abrufen können**, die folgenden Schritte aus:  
  
    1.  Wählen Sie den Eintrag aus, der mit `ldap:///CN=<CATruncatedName>,CN=AIA,CN=Public Key Services`dem Pfad beginnt, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
    2.  Wählen Sie den `http://<ServerDNSName>/CertEnroll/<ServerDNSName>_<CaName><CertificateName>.crt`Eintrag aus, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
    3.  Wählen Sie den `file://\\<ServerDNSName>\CertEnroll\<ServerDNSName><CaName><CertificateName>.crt`Eintrag aus, und klicken Sie dann auf **Entfernen**. Klicken Sie unter **Entfernen bestätigen**auf **Ja**.  
  
11. Klicken Sie in Speicher **Orte angeben, von denen Benutzer das Zertifikat für diese Zertifizierungsstelle abrufen können**auf **Hinzufügen**. Das Dialogfeld **Speicherort hinzufügen** wird geöffnet.  
  
12. Geben`http://pki.corp.contoso.com/pki/<ServerDNSName>_<CaName><CertificateName>.crt`Sie unter **Speicherort hinzufügen**in **Speicherort**ein, und klicken Sie dann auf **OK**. Dadurch wird das Dialogfeld Eigenschaften der Zertifizierungsstelle zurückgegeben.  
  
13. Wählen Sie auf der Registerkarte **Erweiterungen** **in den AIA der ausgestellten Zertifikate einbeziehen aus**.  
  
14. Wenn Sie zum Neustart Active Directory Zertifikat Dienste aufgefordert werden, klicken Sie auf **Nein**. Der Dienst wird zu einem späteren Zeitpunkt neu gestartet.  
  

