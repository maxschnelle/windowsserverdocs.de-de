---
title: Schritt 3 Plan OTP-Zertifikatbereitstellung
description: Dieses Thema ist Teil des Leitfadens Bereitstellen von Remotezugriff mit OTP-Authentifizierung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eca02eeb-d92d-463e-aae0-1f7038ba26fe
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4102fc4f7eacf0b407446717caa83e4e5f70ae57
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282371"
---
# <a name="step-3-plan-otp-certificate-deployment"></a>Schritt 3 Plan OTP-Zertifikatbereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach der Planung des RADIUS-Servers, müssen Sie planen, für die Anforderungen der Zertifizierungsstelle (CA), einschließlich der Zertifizierungsstelle, die Einmalkennwort (OTP) Zertifikate, die OTP-Zertifikatvorlage und der vom Remotehost verwendet registrierungsstellenzertifikats ausstellen Access-Server und alle DirectAccess-Client OTP zertifikatsanforderungen anmelden. Diese Zertifikate werden wie folgt verwendet:  
  
1.  Der DirectAccess-Client fordert ein OTP-Zertifikat aus, und der RAS-Server empfängt die Anforderung.  
  
2.  RAS-Servers wird überprüft, ob der OTP-Anmeldeinformationen, und wenn sie gültig sind, der Server fungiert als eine Autorisierungsstelle für die Registrierung, und der OTP-zertifikatregistrierungsanforderung mithilfe eines kurzlebigen Signaturzertifikats signiert.  
  
3.  RAS-Server sendet die signierte zertifikatanforderung für die Registrierung mit dem DirectAccess-client  
  
4.  Der Client wird dann das OTP-Zertifikat von der Zertifizierungsstelle, die mit der vom Server signierten zertifikatregistrierungsanforderungen registriert.  
  
5.  Die CA überprüft die Anmeldeinformationen und die Anforderung.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[3.1 Planen der OTP-Zertifizierungsstellen](#bkmk_3_1_CA)|Planen Sie die Zertifizierungsstelle (CA) zum Ausstellen von Zertifikaten für DirectAccess-Clients für die OTP-Authentifizierung verwenden.|  
|[3.2 Planung der OTP-Zertifikatvorlage](#bkmk_3_2_OTP_Cert)|Planen Sie die OTP-Zertifikatvorlage.|
|[3.3 Planen der registrierungsstellenzertifikats](#bkmk_33RACert)|Planen Sie die Registrierung-Zertifikat zum Signieren alle zertifikatsanforderungen der OTP-Authentifizierung.|

## <a name="bkmk_3_1_CA"></a>3.1 Planen der OTP-Zertifizierungsstellen  
Um DirectAccess mithilfe der Einmalkennwort-Authentifizierung (OTP) bereitstellen, müssen Sie eine interne Zertifizierungsstelle zum Ausstellen von der OTP-Authentifizierung-Zertifikate für DirectAccess-Clientcomputer. Zu diesem Zweck können Sie die gleiche interne Zertifizierungsstelle, die Sie verwenden, um die Ausstellung der Zertifikate, die für die reguläre IPsec-Computerauthentifizierung verwendet werden.  
  
## <a name="bkmk_3_2_OTP_Cert"></a>3.2 Planung der OTP-Zertifikatvorlage  
Jedes DirectAccess-Client erforderlich, dass ein OTP-Authentifizierungszertifikat auf dem internen Netzwerk zugreifen. Sie müssen eine Vorlage für Ihre interne Zertifizierungsstelle für das OTP-Zertifikat konfigurieren. Beachten Sie Folgendes ein, wenn Sie die OTP-Zertifikatvorlage zu konfigurieren:  
  
-   Es müssen alle Benutzer, die OTP-Authentifizierung ausführen, um müssen Lese- und Registrierungsberechtigungen für diese Vorlage.  
  
-   Der Name des Antragstellers sollten erstellt werden, aus Active Directory-Informationen, um sicherzustellen, dass der Name des Antragstellers findet die Einmalkennwort-Benutzernamen und nicht den Namen des RAS-Servers, der die Anforderung ausführt. Der Name des Antragstellers muss im Format Vollständiger definierter Name sein, und der alternative Antragstellername muss im UPN-Format sein. Dadurch wird sichergestellt, dass das angemeldete OTP-Zertifikat für die Smartcard-Kerberos-Authentifizierung gültig ist.  
  
-   Der Zweck des Zertifikats muss die Smartcard-Anmeldung sein.  
  
-   Ausstellung ist eine autorisierte Signatur erforderlich. Die Signatur muss mit der vordefinierten DirectAccess OTP Anwendung richtlinieneinstellung in der Registrierung Zertifizierungsstelle Signieren Zertifikatvorlage konfiguriert werden.  
  
-   Die Gültigkeitsdauer sollte auf eine Stunde festgelegt werden.  
  
    > [!NOTE]  
    > In Situationen, in dem der CA-Server ist ein Windows Server 2003-Computer, und klicken Sie dann die Vorlage muss auf einem anderen Computer konfiguriert werden. Dies ist darauf zurückzuführen, dass Festlegen der **Gültigkeitsdauer** in Stunden ist nicht möglich, wenn Windows-Versionen vor 2008/Vista ausgeführt wird. Wenn der Computer, mit denen Sie die Vorlage zu konfigurieren, verfügt nicht über die Zertifizierungsdienst-Rolle installiert sein, oder es ein Clientcomputer ist, dann müssen Sie möglicherweise das Zertifikatvorlagen-Snap-in zu installieren. Weitere Informationen zu diesem Thema finden Sie [hier](https://technet.microsoft.com/library/cc732445.aspx).  
  
-   Der Erneuerungszeitraum muss auf 0 festgelegt werden.  
  
-   (Optional) Zertifikate und Anforderungen sollten nicht in der Datenbank der Zertifizierungsstelle gespeichert werden.  
  
-   Das Certificate-Parameter, erweiterte Schlüsselverwendung muss festgelegt werden, korrekt, wie folgt:  
  
    -   Verwenden Sie den Schlüssel 1.3.6.1.4.1.311.81.1.1, für die Zertifikatvorlage der DirectAccess-Registrierung für das Signieren.  
  
    -   Verwenden Sie für die OTP-Zertifikatvorlage für Serverauthentifizierung den 1.3.6.1.4.1.311.20.2.2 Schlüssel.  
  
## <a name="bkmk_33RACert"></a>3.3 Planen der registrierungsstellenzertifikats  
Wenn DirectAccess-Clients ein OTP-Zertifikat anfordern, empfängt der RAS-Server die Anforderung vom Client an. RAS-Server signiert alle OTP zertifikatsanforderungen von Clients, die registrierungsstellenzertifikats verwenden. Die Zertifizierungsstelle stellt Zertifikate nur dann, wenn die Anforderung von der Registrierung auf dem RAS-Server das Zertifikat signiert ist. Das Zertifikat muss von einer internen Zertifizierungsstelle ausgestellt werden, das Zertifikat kann nicht selbst signiert werden. Es muss nicht von der Zertifizierungsstelle ausgestellt werden, die die OTP-Zertifikate ausgestellt, aber die Zertifizierungsstelle, die die OTP-Zertifikate ausstellt, muss die Zertifizierungsstelle, die das Signaturzertifikat für die Registrierung Autorität ausgestellt vertrauen.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 4: Planen von OTP für den RAS-server](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  


