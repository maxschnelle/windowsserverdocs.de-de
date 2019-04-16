---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: "Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden wir ein grundlegendes Szenario behandelt, das erläutert, wie die Anspruchstransformation zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen konfigurieren. Sie erfahren, wie Ansprüche Transformation Gruppenrichtlinienobjekte erstellt und der Vertrauensstellung der vertrauenden Gesamtstruktur und der vertrauenswürdigen Gesamtstruktur verknüpft werden können. Sie werden dann das Szenario überprüfen.  
  
## <a name="scenario-overview"></a>Beispielszenario (Übersicht)  
Adatum Corporation bietet Finanzdienstleistungen auf Contoso, Ltd. Jedes Quartal kopieren Adatum Abteilungsserver ihre Konto-Tabellen in einen Ordner auf einem Dateiserver befindet sich bei Contoso, Ltd. Es gibt eine bidirektionale Vertrauensstellung, die von Contoso Adatum eingerichtet. Contoso, Ltd. möchte die Freigabe schützen, sodass nur Adatum Mitarbeiter auf die Remotefreigabe zugreifen können.  
  
In diesem Szenario:  
  
1.  [Richten Sie die erforderlichen Komponenten und der Testumgebung](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [Einrichten der Transformation von Ansprüchen auf vertrauenswürdige Gesamtstruktur (Adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [Einrichten der Transformation von Ansprüchen in der vertrauenden Gesamtstruktur (Contoso)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [Überprüfen Sie das Szenario](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>Richten Sie die erforderlichen Komponenten und der Testumgebung  
Die Testkonfiguration umfasst das Einrichten von zwei Gesamtstrukturen: Adatum Corporation und Contoso, Ltd. und müssen eine bidirektionale Vertrauensstellung zwischen Contoso und "Adatum". "adatum.com" ist der vertrauenswürdigen Gesamtstruktur, und "contoso.com" ist die vertrauende Gesamtstruktur.  
  
Ansprüche Transformation Szenario veranschaulicht die Transformation von Ansprüchen in der vertrauenswürdigen Gesamtstruktur zum einen Anspruch in der vertrauenden Gesamtstruktur. Zu diesem Zweck müssen Sie zum Einrichten einer neuen Gesamtstruktur adatum.com bezeichnet und zum Auffüllen der Gesamtstruktur mit einem Testbenutzer mit einem Unternehmens-Wert von "Adatum". Sie müssen eine bidirektionale Vertrauensstellung zwischen contoso.com und adatum.com einrichten.  
  
> [!IMPORTANT]  
> Beim Einrichten der Contoso "und" Adatum Gesamtstrukturen müssen Sie sicherstellen, dass beide Stammdomänen unter Windows Server2012 als Domänenfunktionsebene für die Transformation von Ansprüchen funktioniert.  
  
Sie müssen die folgenden für das Labor einrichten. Diese Verfahren werden ausführlich im [AnhangB: Einstellung Einrichten der Testumgebung](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
Sie müssen die folgenden Verfahren zum Einrichten der Testumgebung für dieses Szenario implementieren:  
  
1.  [Legen Sie als vertrauenswürdigen Gesamtstruktur Contoso Adatum fest](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  [Erstellen Sie den Anspruchstyp "Unternehmen" auf Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  [Aktivieren Sie die Ressourceneigenschaft "Unternehmen" auf Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [Erstellen Sie die zentrale Zugriffsregel](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [Erstellen Sie die zentrale Zugriffsrichtlinie](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [Veröffentlichen der neuen Richtlinie mithilfe von Gruppenrichtlinien](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [Erstellen Sie den Ordner "Ergebnis" auf dem Dateiserver](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [Legen Sie die Klassifizierung, und wenden Sie die zentrale Zugriffsrichtlinie auf den neuen Ordner](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
Verwenden Sie die folgende Informationen, um dieses Szenario:  
  
|Objekte|Detail|  
|-----------|-----------|  
|Benutzer|Jeff Low, Contoso|  
|Benutzeransprüche auf Adatum und Contoso|-ID: Ad: / / Ext/Unternehmen: ContosoAdatum,<br /><br />Quellattribut: Unternehmen<br /><br />Vorgeschlagene Werte: Contoso, Adatum **wichtig:** müssen Sie die ID für die "Unternehmen" Anspruchstyp auf setzen Contoso sowohl Adatum für die Transformation von Ansprüchen gleich funktioniert.|  
|Zentrale Zugriffsregel auf Contoso|AdatumEmployeeAccessRule|  
|Zentrale Zugriffsrichtlinie auf Contoso|Nur Zugriffsrichtlinie adatum|  
|Ansprüche Transformation Richtlinien auf Adatum und Contoso|DenyAllExcept Unternehmen|  
|Dateiordner auf Contoso|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>Einrichten der Transformation von Ansprüchen auf vertrauenswürdige Gesamtstruktur (Adatum)  
In diesem Schritterstellen Sie eine Transformation-Richtlinie in der Adatum verweigern, alle Ansprüche mit Ausnahme von "Unternehmen" an Contoso übergeben.  
  
Active Directory-Modul für Windows PowerShell bietet die **DenyAllExcept** Argument, das alles außer dem angegebenen Ansprüche in der Transformation-Richtlinie fällt.  
  
Um eine Transformation von Ansprüchen einzurichten, müssen Sie eine Ansprüche Transformation-Richtlinie erstellen und verknüpfen sie den vertrauenswürdigen und vertrauenden Gesamtstrukturen.  
  
### <a name="BKMK_2.2"></a>Erstellen Sie eine Richtlinie für Ansprüche Transformation in Adatum  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>Erstellen eine Richtlinie Transformation Adatum alle Ansprüche mit Ausnahme von "Unternehmen" verweigern  
  
1.  Melden Sie sich an den Domänencontroller adatum.com als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>Legen Sie einen Ansprüche Transformation Link auf der Adatum-Gesamtstruktur-Vertrauensstellung Domänenobjekt  
In diesem Schrittwenden Sie die Richtlinie für neu erstellte Ansprüche Transformation auf der Adatum-Gesamtstruktur-Vertrauensstellung Domänenobjekt für Contoso.  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>Die Ansprüche Transformation Richtlinie anwenden  
  
1.  Melden Sie sich an den Domänencontroller adatum.com als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>Einrichten der Transformation von Ansprüchen in der vertrauenden Gesamtstruktur (Contoso)  
In diesem Schritterstellen Sie eine Ansprüche Transformation-Richtlinie in Contoso (der vertrauenden Gesamtstruktur) verweigern, alle Ansprüche mit Ausnahme von "Unternehmen". Sie müssen eine Ansprüche Transformation Richtlinie erstellen und verknüpfen Sie es mit der Gesamtstruktur-Vertrauensstellung.  
  
### <a name="BKMK_4.1"></a>Erstellen Sie eine Richtlinie für Ansprüche Transformation in Contoso  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>Erstellen eine Richtlinie Transformation Adatum verweigern, alle mit Ausnahme von "Unternehmen"  
  
1.  Melden Sie sich an den Domänencontroller contoso.com als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>Legen Sie einen Link der Ansprüche Transformation auf Contoso Domäne Vertrauensobjekt  
In diesem Schrittwenden Sie das neu erstellte Ansprüche Transformation Richtlinie auf das contoso.com Vertrauensstellung Domänenobjekt Adatum zulassen "Unternehmen" an contoso.com übergeben werden. Das Domänenobjekt Vertrauensstellung heißt adatum.com.  
  
##### <a name="to-set-the-claims-transformation-policy"></a>Ansprüche Transformation Richtlinie festlegen  
  
1.  Melden Sie sich an den Domänencontroller contoso.com als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>Überprüfen Sie das Szenario  
In diesem Schrittversuchen Sie den D:\EARNINGS Ordner zugreifen, der eingerichtet wurde auf dem Dateiserver "file1" zu überprüfen, ob der Benutzer Zugriff auf den freigegebenen Ordner hat.  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Um sicherzustellen, dass den Adatum-Benutzer kann den freigegebenen Ordner zugreifen.  
  
1.  Melden Sie sich an den Clientcomputer CLIENT1 als Jeff Low mit dem Kennwort **pass@word1**.  
  
2.  Navigieren Sie zu dem Ordner \\\FILE1.contoso.com\Earnings.  
  
3.  Jeff Low sollte auf den Ordner zugreifen können.  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>Weitere Szenarien für Ansprüche Transformation Richtlinien  
Es folgt eine Liste der zusätzliche allgemeine Fälle, in die Transformation von Ansprüchen.  
  
|Szenario|Richtlinie|  
|------------|----------|  
|Zulassen Sie alle Ansprüche, die Adatum-Gesamtstruktur auf Contoso Adatum durchlaufen stammen|Code- <br />New-ADClaimTransformPolicy \ "<br /> -Beschreibung: "Ansprüche Transformation-Richtlinie zum Zulassen von alle Ansprüche" \ "<br />-Name: "AllowAllClaimsPolicy" \ "<br />-AllowAll \ "<br />-Server: "contoso.com" \ "<br />Set-ADClaimTransformLink \ "<br />-Identity: "adatum.com" \ "<br />-Richtlinie: "AllowAllClaimsPolicy" \ "<br />-TrustRole: vertrauen \ "<br />-Server: "contoso.com" '|  
|Verweigern Sie alle Ansprüche, die Adatum-Gesamtstruktur auf Contoso Adatum durchlaufen stammen|Code- <br />New-ADClaimTransformPolicy \ "<br />-Beschreibung: "Ansprüche Transformation-Richtlinie auf alle Ansprüche verweigern" \ "<br />-Name: "DenyAllClaimsPolicy" \ "<br /> -DenyAll \ "<br />-Server: "contoso.com" \ "<br />Set-ADClaimTransformLink \ "<br />-Identity: "adatum.com" \ "<br />-Richtlinie: "DenyAllClaimsPolicy" \ "<br />-TrustRole: vertrauen \ "<br />-Server: "contoso.com" '|  
|Zulassen Sie alle Ansprüche, die mit Ausnahme von "Unternehmen" und "Department" durchlaufen bei Contoso Adatum Adatum-Gesamtstruktur stammen|Code <br />-New-ADClaimTransformationPolicy \ "<br />-Beschreibung: "Ansprüche Transformation-Richtlinie zum Zulassen von alle Ansprüche mit Ausnahme von Unternehmen" und "Department" \ "<br /> -Name: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \ "<br />-AllowAllExcept: Unternehmen, Abteilung \ "<br />-Server: "contoso.com" \ "<br />Set-ADClaimTransformLink \ "<br /> -Identity: "adatum.com" \ "<br />-Richtlinie: "AllowAllClaimsExceptCompanyAndDepartmentPolicy" \ "<br /> -TrustRole: vertrauen \ "<br />-Server: "contoso.com" '|  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   Eine Liste aller Windows PowerShell-Cmdlets, die für die Transformation von Ansprüchen verfügbar sind, finden Sie unter [Active Directory-PowerShell-Cmdlet-Referenz ](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
-   Verwenden Sie für erweiterte Aufgaben mit Export und Import von DAC-Konfigurationsinformationen zwischen zwei Gesamtstrukturen, die [Dynamic Access-Steuerelement PowerShell-Referenz](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [Bereitstellen von Ansprüchen über Gesamtstrukturen](Deploy-Claims-Across-Forests.md)  
  
-   [Ansprüche Transformation Regeln Sprache](Claims-Transformation-Rules-Language.md)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

