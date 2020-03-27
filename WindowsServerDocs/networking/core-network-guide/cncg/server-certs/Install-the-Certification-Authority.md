---
title: Installieren der Zertifizierungsstelle
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fffb03a707c48c8dd485c68b5c6bf10783b0e6cf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318366"
---
# <a name="install-the-certification-authority"></a>Installieren der Zertifizierungsstelle

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mithilfe dieses Verfahrens können Sie Active Directory Zertifikat Dienste (AD CS) installieren, damit Sie ein Serverzertifikat für Server mit Netzwerk Richtlinien Server (Network Policy Server, NPS), Routing-und RAS-Dienst (RRAS) oder beides registrieren können.  
  
> [!IMPORTANT]  
> -   Bevor Sie Active Directory Zertifikat Dienste installieren, müssen Sie den Computer benennen, den Computer mit einer statischen IP-Adresse konfigurieren und den Computer der Domäne hinzufügen. Weitere Informationen zum Ausführen dieser Aufgaben finden Sie im Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide).  
> -   Um dieses Verfahren auszuführen, muss der Computer, auf dem Sie AD CS installieren, einer Domäne hinzugefügt werden, in der Active Directory Domain Services (AD DS) installiert ist.  
  
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.  
  
> [!NOTE]  
> Um dieses Verfahren mithilfe von Windows PowerShell auszuführen, öffnen Sie Windows PowerShell, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> Geben Sie nach der Installation von AD CS den folgenden Befehl ein, und drücken Sie die EINGABETASTE.  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>So installieren Sie Active Directory-Zertifikatsdienste  

> [!TIP]
> Wenn Sie Windows PowerShell zum installieren Active Directory Zertifikat Dienste verwenden möchten, finden Sie weitere Informationen unter [install-adcscertificationauthority](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcscertificationauthority?view=win10-ps) für Cmdlets und optionale Parameter.
  
1.  Melden Sie sich als Mitglied der GruppeOrganisations-Admins und der GruppeDomänen-Admins der Stammdomäne an.  
  
2.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.  
  
3.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.  
  
    > [!NOTE]  
    > Die Seite **Vorbemerkungen** im Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie bei einer früheren Ausführung des Assistenten die Option **Seite standardmäßig überspringen** ausgewählt haben.  
  
4.  Wählen Sie unter **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie dann auf **Weiter**.  
  
5.  Stellen Sie sicher, dass unter **Zielserver auswählen** die Option **Einen Server aus dem Serverpool auswählen** aktiviert ist. Wählen Sie unter **Serverpool** den lokalen Computer aus. Klicken Sie auf **Weiter**.  
  
6.  Wählen Sie unter **Server Rollen auswählen**unter **Rollen**die Option **Active Directory Zertifikat Dienste**aus. Wenn Sie aufgefordert werden, erforderliche Features hinzuzufügen, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie unter **Features auswählen**auf **weiter**.  
  
8.  Lesen Sie in **Active Directory Zertifikat Dienste**die angegebenen Informationen, und klicken Sie dann auf **weiter**.  
  
9. Klicken Sie unter **Installationsauswahl bestätigen** auf **Installieren**. Schließen Sie den Assistenten während des Installationsvorgangs nicht. Klicken Sie nach Abschluss der Installation **auf Active Directory Zertifikat Dienste auf dem Zielserver konfigurieren**. Der AD CS-Konfigurations-Assistent wird geöffnet. Lesen Sie die Informationen zu den Anmelde Informationen, und geben Sie ggf. die Anmelde Informationen für ein Konto an, das Mitglied der Gruppe Organisations-Admins ist. Klicken Sie auf **Weiter**.  
  
10. Klicken Sie unter **Rollen Dienste**auf **Zertifizierungs**Stelle, und klicken Sie dann auf **weiter**.  
  
11. Überprüfen Sie auf der Seite Setuptyp, ob **Unternehmens** Zertifizierungsstelle ausgewählt ist, und klicken Sie dann auf **weiter**. **Setup Type**  
  
12. Vergewissern Sie sich **, dass auf** der Seite **Typ der** Zertifizierungsstelle angeben die Option Stamm Zertifizierungsstelle ausgewählt ist, und klicken Sie dann auf **weiter**.  
  
13. Vergewissern Sie sich, dass auf der Seite **Geben Sie den Typ des privaten Schlüssels** an die Option **neuen privaten Schlüssel erstellen** ausgewählt ist, und klicken Sie dann auf **weiter**.  
  
14. Behalten Sie auf der Seite **Kryptografie für** Zertifizierungsstelle die Standardeinstellungen für CSP (**RSA # Microsoft-Software Schlüsselspeicher-Anbieter**) und Hash Algorithmus (**SHA2**) bei, und bestimmen Sie die beste Schlüsselzeichen Länge für die Bereitstellung. Große Schlüsselzeichen Längen bieten optimale Sicherheit. Sie können sich jedoch auf die Serverleistung auswirken und sind möglicherweise nicht mit Legacy Anwendungen kompatibel. Es wird empfohlen, dass Sie die Standardeinstellung 2048 beibehalten. Klicken Sie auf **Weiter**.  
  
15. Behalten Sie auf der Seite Zertifizierungsstellen **Name** den vorgeschlagenen allgemeinen Namen für die Zertifizierungsstelle bei, oder ändern Sie den Namen entsprechend Ihren Anforderungen. Stellen Sie sicher, dass der ZS-Name mit ihren Benennungs Konventionen und-Zwecken kompatibel ist, weil Sie den Zertifizierungsstellen Namen nach der Installation von AD CS nicht mehr ändern können. Klicken Sie auf **Weiter**.  
  
16. Geben Sie auf der Seite **Gültigkeitsdauer** in **Geben Sie den Gültigkeits Zeitraum**an die Zahl ein, und wählen Sie einen Zeitwert (Jahre, Monate, Wochen oder Tage) aus. Die Standardeinstellung für fünf Jahre wird empfohlen. Klicken Sie auf **Weiter**.  
  
17. Geben Sie auf der Seite Zertifizierungsstellen **Datenbank** unter **Geben Sie die Daten Bank Speicherorte**an den Speicherort des Ordners für die Zertifikat Datenbank und das Zertifikat Daten Bank Protokoll an. Wenn Sie andere Speicherorte als die Standard Speicherorte angeben, stellen Sie sicher, dass die Ordner durch Zugriffs Steuerungs Listen (ACLs) geschützt sind, die verhindern, dass unbefugte Benutzer oder Computer auf die Datenbank und die Protokolldateien der Zertifizierungsstelle zugreifen. Klicken Sie auf **Weiter**.  
  
18. Klicken Sie unter **Bestätigung**auf **Konfigurieren** , um die Auswahl zu übernehmen, und klicken Sie dann auf **Schließen**.  
  


