---
title: Installieren der Zertifizierungsstelle
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17a887ab32570b739d5ca99611ee0d496a966d1b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-certification-authority"></a>Installieren der Zertifizierungsstelle

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie Active Directory-Zertifikatdienste (AD CS) installieren, damit Sie ein Serverzertifikat für Server registrieren können, auf dem Netzwerkrichtlinienserver (Network Policy Server, NPS), Routing- und RAS-Dienst (RRAS) oder beides ausgeführt werden.  
  
> [!IMPORTANT]  
> -   Vor der Installation von Active Directory Certificate Services müssen Sie Namen für den Computer, konfigurieren Sie den Computer mit einer statischen IP-Adresse und der Computer der Domäne hinzufügen. Weitere Informationen dazu, wie zum Ausführen dieser Aufgaben finden Sie unter Windows Server 2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide).  
> -   Um dieses Verfahren auszuführen, muss der Computer, auf dem Sie AD CS installieren, zu einer Domäne angehören, auf dem Active Directory-Domänendienste (AD DS) installiert ist.  
  
Mitgliedschaften in den **Organisations-Admins** und der Stammdomäne **Domänen-Admins** Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  
  
> [!NOTE]  
> Führen Sie dieses Verfahren mithilfe von Windows PowerShell, öffnen Sie Windows PowerShell und geben Sie den folgenden Befehl, und drücken dann die EINGABETASTE.   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> Nach der Installation von AD CS Geben Sie folgenden Befehl ein, und drücken Sie die EINGABETASTE.  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>So installieren Sie Active Directory-Zertifikatdienste  
  
1.  Melden Sie sich als Mitglied der Gruppe Organisations-Admins und Domänen-Admins der Stammdomäne an.  
  
2.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.  
  
3.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > Die **Vorbemerkungen** des Hinzufügen von Rollen und Features Assistenten nicht angezeigt wird, wenn Sie zuvor ausgewählt haben **diese Seite standardmäßig überspringen** beim Hinzufügen von Rollen und Features-Assistent ausgeführt wurde.  
  
4.  In **Select Installation Type**, stellen Sie sicher, dass **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
5.  In **Zielserver auswählen**, stellen Sie sicher, dass **wählen Sie einen Server aus dem Serverpool** ausgewählt ist. In **Serverpool**, stellen Sie sicher, dass der lokale Computer ausgewählt ist. Klicken Sie auf **Weiter**.  
  
6.  In **Serverrollen auswählen**im **Rollen**Option **Active Directory Certificate Services**. Wenn Sie zum Hinzufügen Erforderlicher Funktionen aufgefordert werden, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  In **Features auswählen**, klicken Sie auf **Weiter**.  
  
8.  In **Active Directory Certificate Services**, lesen Sie die bereitgestellte Informationen, und klicken Sie dann auf **Weiter**.  
  
9. In **Installationsauswahl bestätigen**, klicken Sie auf **installieren**. Schließen Sie den Assistenten nicht während der Installation. Wenn die Installation abgeschlossen ist, klicken Sie auf **konfigurieren Sie Active Directory-Zertifikatdienste auf dem Zielserver**. Der AD CS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Anmeldeinformationen, und geben Sie bei Bedarf die Anmeldeinformationen für ein Konto, das Mitglied der Gruppe Organisations-Admins ist. Klicken Sie auf **Weiter**.  
  
10. In **Rollendienste**, klicken Sie auf **Zertifizierungsstelle**, und klicken Sie dann auf **Weiter**.  
  
11. Auf der **Setuptyp** überprüfen Sie, ob Seite **Unternehmenszertifizierungsstelle** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
12. Auf der **geben den Typ der Zertifizierungsstelle** überprüfen Sie, ob Seite **Stamm-CA** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **geben den Typ des privaten Schlüssels** überprüfen Sie, ob Seite **erstellen einen neuen privaten Schlüssel** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
14. Auf der **Kryptografie für Zertifizierungsstelle** Seite, behalten Sie die Standardeinstellungen für CSP (**RSA #Microsoft Software Key Storage Provider**) und Hashalgorithmus (**SHA1**), und ermitteln Sie die beste Schlüsselzeichenlänge für die Bereitstellung. Große schlüsselzeichenlängen bieten zwar optimale Sicherheit; Allerdings kann die Leistung beeinträchtigen und möglicherweise nicht mit älteren Anwendungen kompatibel. Es wird empfohlen, dass Sie die Standardeinstellung von 2048 zu übernehmen. Klicken Sie auf **Weiter**.  
  
15. Auf der **Zertifizierungsstellennamen** Seite, halten Sie den vorgeschlagenen allgemeinen Namen für die Zertifizierungsstelle oder den Namen entsprechend Ihren Anforderungen ändern. Stellen Sie sicher, dass Sie sicher, dass der Name der Zertifizierungsstelle mit Benennungskonventionen und Zwecke kompatibel ist, da Sie den Namen der Zertifizierungsstelle nicht geändert werden können, nach der Installation von AD CS sind. Klicken Sie auf **Weiter**.  
  
16. Auf der **Gültigkeitsdauer** Seite **Geben Sie die Gültigkeitsdauer**, geben Sie die Nummer, und wählen Sie einen Zeitwert (Jahre, Monate, Wochen oder Tage). Die Standardeinstellung von fünf Jahren wird empfohlen. Klicken Sie auf **Weiter**.  
  
17. Auf der **Datenbank der Zertifizierungsstelle** Seite **geben die Datenbankspeicherorte für die**, geben Sie den Speicherort des Ordners für die Zertifikatdatenbank und Zertifikatdatenbankprotokoll. Wenn Sie nicht in die Standardspeicherorte angeben, stellen Sie sicher, dass die Ordner mit Zugriffssteuerungslisten (ACLs) geschützt sind, die verhindern, dass nicht autorisierte Benutzer oder Computer Zugriff auf die CA-Datenbank und-Protokolldateien. Klicken Sie auf **Weiter**.  
  
18. In **Bestätigung**, klicken Sie auf **konfigurieren** auf Ihre Auswahl, und klicken Sie dann auf **schließen**.  
  


