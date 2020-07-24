---
title: Schritt 3 Planen der OTP-Zertifikat Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eca02eeb-d92d-463e-aae0-1f7038ba26fe
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a65ddec97bcdd911d0cf81bfd54e2ddbb286ed54
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965262"
---
# <a name="step-3-plan-otp-certificate-deployment"></a>Schritt 3 Planen der OTP-Zertifikat Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Nach der Planung des RADIUS-Servers müssen Sie die Anforderungen an die Zertifizierungsstelle (Certification Authority, ca) planen, einschließlich der Zertifizierungsstelle, von der ein einmal Kennwort (OTP) (einmal Kennwort), die OTP-Zertifikat Vorlage und das Registrierungsstellen Zertifikat, das vom RAS-Server verwendet wird, zum Signieren aller OTP-Zertifikat Anforderungen von DirectAccess Diese Zertifikate werden wie folgt verwendet:  
  
1.  Der DirectAccess-Client fordert ein OTP-Zertifikat an, und der Remote Zugriffs Server empfängt die Anforderung.  
  
2.  Der RAS-Server überprüft die OTP-Anmelde Informationen. wenn diese gültig sind, fungiert der Server als Registrierungsstelle und signiert die OTP-Zertifikat Registrierungs Anforderung mithilfe eines kurzlebigen Signatur Zertifikats.  
  
3.  Der Remote Zugriffs Server sendet die signierte Zertifikat Registrierungs Anforderung an den DirectAccess-Client zurück.  
  
4.  Der Client registriert dann das OTP-Zertifikat von der Zertifizierungsstelle mithilfe der Zertifikat Registrierungsanforderungen, die vom Server signiert wurden.  
  
5.  Die Zertifizierungsstelle überprüft die Anmelde Informationen und die Anforderung.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3,1 Planen der OTP-Zertifizierungsstelle](#bkmk_3_1_CA)|Planen Sie die Zertifizierungsstelle, die zum Ausstellen von Zertifikaten für DirectAccess-Clients für die OTP-Authentifizierung verwendet werden soll.|  
|[3,2 Planen der OTP-Zertifikat Vorlage](#bkmk_3_2_OTP_Cert)|Planen Sie die OTP-Zertifikat Vorlage.|
|[3,3 Planen des Registrierungsstellen Zertifikats](#bkmk_33RACert)|Planen Sie das Registrierungsstellen Zertifikat, um alle OTP-Authentifizierungszertifikat Anforderungen zu signieren.|

## <a name="31-plan-the-otp-ca"></a><a name="bkmk_3_1_CA"></a>3,1 Planen der OTP-Zertifizierungsstelle  
Zum Bereitstellen von DirectAccess mithilfe von einmal Kennwort-Authentifizierung (einmal Kennwort-Authentifizierung) benötigen Sie eine interne Zertifizierungsstelle, um die OTP-Authentifizierungs Zertifikate für DirectAccess-Client Computer auszustellen. Zu diesem Zweck können Sie dieselbe interne Zertifizierungsstelle verwenden, mit der Sie die Zertifikate ausstellen, die für die reguläre IPSec-Computer Authentifizierung verwendet werden.  
  
## <a name="32-plan-the-otp-certificate-template"></a><a name="bkmk_3_2_OTP_Cert"></a>3,2 Planen der OTP-Zertifikat Vorlage  
Jeder DirectAccess-Client benötigt ein OTP-Authentifizierungszertifikat, um Zugriff auf das interne Netzwerk zu erhalten. Sie müssen eine Vorlage für die interne Zertifizierungsstelle für das OTP-Zertifikat konfigurieren. Beachten Sie beim Konfigurieren der OTP-Zertifikat Vorlage Folgendes:  
  
-   Alle Benutzer, die die OTP-Authentifizierung durchführen müssen, müssen über die Berechtigungen Lesen und anmelden für diese Vorlage verfügen.  
  
-   Der Name des Antragstellers sollte aus Active Directory Informationen erstellt werden, um sicherzustellen, dass der Antragsteller Name mit dem OTP-Benutzernamen übereinstimmt, und nicht mit dem Namen des RAS-Servers, von dem die Zertifikat Anforderung durchführt. Der Antragsteller Name muss das vollständig gekennzeichnete Namensformat aufweisen, und der alternative Antragsteller Name muss das UPN-Format aufweisen. Dadurch wird sichergestellt, dass das registrierte OTP-Zertifikat für die Smartcard-Kerberos-Authentifizierung gültig ist.  
  
-   Der beabsichtigte Zweck des Zertifikats muss die Smartcard-Anmeldung sein.  
  
-   Die Ausstellung muss eine autorisierte Signatur erfordern. Die Signatur muss mit der vordefinierten DirectAccess OTP-Anwendungs Richtlinie konfiguriert werden, die in der Registrierungsstelle-Signaturzertifikat Vorlage festgelegt ist.  
  
-   Der Gültigkeits Zeitraum muss auf eine Stunde festgelegt werden.  
  
    > [!NOTE]  
    > In Fällen, in denen der Zertifizierungsstellen Server ein Windows Server 2003-Computer ist, muss die Vorlage auf einem anderen Computer konfiguriert werden. Dies liegt daran, dass das Festlegen der **Gültigkeitsdauer** in Stunden nicht möglich ist, wenn Windows-Versionen vor 2008/Vista ausgeführt werden. Wenn auf dem Computer, den Sie zum Konfigurieren der Vorlage verwenden, die Zertifizierungsdienst Rolle nicht installiert ist, oder es sich um einen Client Computer handelt, müssen Sie möglicherweise das Zertifikat Vorlagen-Snap-in installieren. Weitere Informationen zu diesem Betreff finden Sie [hier](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732445(v=ws.11)).  
  
-   Der Erneuerungs Zeitraum muss auf 0 festgelegt werden.  
  
-   Optionale Zertifikate und Anforderungen dürfen nicht in der Zertifizierungsstellen-Datenbank gespeichert werden.  
  
-   Der erweiterte Schlüssel Verwendungs Parameter des Zertifikats muss wie folgt ordnungsgemäß festgelegt werden:  
  
    -   Verwenden Sie für die DirectAccess-Registrierungs Signaturzertifikat-Vorlage den Schlüssel 1.3.6.1.4.1.311.81.1.1.  
  
    -   Verwenden Sie für die OTP-Authentifizierungszertifikat Vorlage den Schlüssel 1.3.6.1.4.1.311.20.2.2 Key.  
  
## <a name="33-plan-the-registration-authority-certificate"></a><a name="bkmk_33RACert"></a>3,3 Planen des Registrierungsstellen Zertifikats  
Wenn DirectAccess-Clients ein OTP-Zertifikat anfordern, empfängt der RAS-Server die Anforderung vom Client. Der RAS-Server signiert alle OTP-Zertifikat Anforderungen von Clients mithilfe des Registrierungsstellen Zertifikats. Die Zertifizierungsstelle gibt Zertifikate nur dann aus, wenn die Anforderung vom Registrierungsstellen Zertifikat auf dem RAS-Server signiert wurde. Das Zertifikat muss von einer internen Zertifizierungsstelle ausgestellt werden, das Zertifikat kann nicht selbst signiert werden. Er muss nicht von der Zertifizierungsstelle ausgestellt werden, die die OTP-Zertifikate ausgestellt hat, aber die Zertifizierungsstelle, die die OTP-Zertifikate ausgibt, muss der Zertifizierungsstelle vertrauen, die das Signaturzertifikat der Registrierungsstelle ausgibt.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 4: Planen von OTP für den Remote Zugriffs Server](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
