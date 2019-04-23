---
title: Installieren der Zertifizierungsstelle
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 84e4b2fe0b59820b9e51229335f3539bcbeeec90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860741"
---
# <a name="install-the-certification-authority"></a>Installieren der Zertifizierungsstelle

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, Active Directory-Zertifikatdienste (AD CS) installieren, damit Sie ein Serverzertifikat für den Server registrieren können, die Windows-Verwaltungsinstrumentation (Network Policy Server, NPS), Routing und RAS-Dienst (RRAS) oder beide ausgeführt werden.  
  
> [!IMPORTANT]  
> -   Vor der Installation von Active Directory Certificate Services müssen Sie den Computer benennen, konfigurieren Sie den Computer mit einer statischen IP-Adresse und fügen Sie den Computer der Domäne. Weitere Informationen zum Umsetzen dieser Aufgaben finden Sie unter Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide).  
> -   Um dieses Verfahren auszuführen, muss der Computer, auf dem Sie AD CS installieren, zu einer Domäne angehören, auf dem Active Directory Domain Services (AD DS) installiert ist.  
  
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.  
  
> [!NOTE]  
> Öffnen Sie Windows PowerShell zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell Geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> Nachdem Sie AD CS installiert ist, geben Sie den folgenden Befehl aus, und drücken Sie EINGABETASTE.  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>So installieren Sie Active Directory-Zertifikatsdienste  

>[!TIP]
>Wenn Sie Windows PowerShell zum Installieren von Active Directory-Zertifikatdienste finden verwenden möchten [Install-AdcsCertificationAuthority](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcscertificationauthority?view=win10-ps) für Cmdlets und optionale Parameter.
  
1.  Melden Sie sich als Mitglied der GruppeOrganisations-Admins und der GruppeDomänen-Admins der Stammdomäne an.  
  
2.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.  
  
3.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.  
  
    > [!NOTE]  
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.  
  
4.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.  
  
5.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.  
  
6.  In **Serverrollen auswählen**im **Rollen**Option **Active Directory Certificate Services**. Wenn Sie aufgefordert werden, die erforderlichen Features hinzuzufügen, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  In **Funktionen auswählen**, klicken Sie auf **Weiter**.  
  
8.  In **Active Directory Certificate Services**, lesen Sie die bereitgestellte Informationen, und klicken Sie dann auf **Weiter**.  
  
9. Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**. Schließen Sie den Assistenten nicht während der Installation. Wenn die Installation abgeschlossen ist, klicken Sie auf **Konfigurieren von Active Directory-Zertifikatdienste auf dem Zielserver**. Der AD CS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Anmeldeinformationen für Informationen, und geben Sie bei Bedarf die Anmeldeinformationen für ein Konto, das Mitglied der Gruppe "Organisations-Admins" ist. Klicken Sie auf **Weiter**.  
  
10. In **Rollendienste**, klicken Sie auf **Zertifizierungsstelle**, und klicken Sie dann auf **Weiter**.  
  
11. Auf der **Setuptyp** überprüfen Sie, ob Seite **Unternehmenszertifizierungsstelle** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
12. Auf der **Geben Sie den Typ der Zertifizierungsstelle** überprüfen Sie, ob Seite **Stamm-CA** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **Geben Sie den Typ des privaten Schlüssels** überprüfen Sie, ob Seite **erstellen Sie einen neuen privaten Schlüssel** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
14. Auf der **Kryptografie für Zertifizierungsstelle** Seite, behalten Sie die Standardeinstellungen für CSP (**RSA #Microsoft Software Key Storage Provider**) und Hash-Algorithmus (**SHA2**), und bestimmen die besten Schlüsselzeichenlänge für die Bereitstellung. Große schlüsselzeichenlängen bieten zwar optimale Sicherheit; Allerdings kann die serverleistung beeinträchtigen und möglicherweise nicht mit älteren Anwendungen kompatibel. Es wird empfohlen, dass Sie die Standardeinstellung von 2048 halten. Klicken Sie auf **Weiter**.  
  
15. Auf der **Zertifizierungsstellenname** Seite, behalten Sie den vorgeschlagenen allgemeinen Namen für die Zertifizierungsstelle aus, oder ändern Sie den Namen entsprechend Ihren Anforderungen. Stellen Sie sicher, dass Sie sicher, dass der Name der Zertifizierungsstelle mit Ihren Benennungskonventionen und Zwecke verwenden, kompatibel ist, da Sie den Namen der Zertifizierungsstelle ändern können, nach der Installation von AD CS sind. Klicken Sie auf **Weiter**.  
  
16. Auf der **Gültigkeitsdauer** auf der Seite **angeben die Gültigkeitsdauer**, geben Sie die Anzahl, und wählen Sie einen Zeitwert aus (Jahre, Monate, Wochen oder Tage). Die Standardeinstellung von fünf Jahren wird empfohlen. Klicken Sie auf **Weiter**.  
  
17. Auf der **Zertifizierungsstellendatenbank** auf der Seite **Geben Sie den Speicherort der Datenbank**, geben Sie den Speicherort des Ordners für die Zertifikatdatenbank und die Zertifikatdatenbankprotokoll. Wenn Sie an anderen Orten als die Standardspeicherorte angeben, stellen Sie sicher, dass die Ordner mit Zugriffssteuerungslisten (ACLs) geschützt sind, die verhindern, dass nicht autorisierte Benutzer oder Computer Zugriff auf die CA-Datenbank und-Protokolldateien. Klicken Sie auf **Weiter**.  
  
18. In **Bestätigung**, klicken Sie auf **konfigurieren** auf Ihre Auswahl, und klicken Sie dann auf **schließen**.  
  


