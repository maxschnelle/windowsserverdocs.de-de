---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3bab7a396061ecae8a187cc6986d6d026a9e4b32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830351"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird ein grundlegendes Szenario behandelt, das erklärt, wie Sie Transformationen von Ansprüchen zwischen vertrauenden und vertrauenswürdigen Gesamtstrukturen konfigurieren. Sie lernen, wie Ansprüche Transformation Gruppenrichtlinienobjekte erstellt und verknüpft die Vertrauensstellung der vertrauenden Gesamtstruktur und der vertrauenswürdigen Gesamtstruktur werden können. Sie werden dann das Szenario überprüfen.  
  
## <a name="scenario-overview"></a>Szenarioübersicht  
Adatum Corporation stellt Finanzdienstleistungen an Contoso, Ltd. In jedem Quartal kopieren Adatum Accountants ihre Konto-Tabellen in einen Ordner auf einem Dateiserver befindet sich bei Contoso, Ltd. Es gibt eine bidirektionale Vertrauensstellung, die von Contoso auf Adatum einrichten. Contoso, Ltd. möchte die Freigabe schützen, sodass nur Adatum Mitarbeitern Freigabe auf den Remotecomputer zugreifen können.  
  
In diesem Szenario:  
  
1.  [Richten Sie die Voraussetzungen und die testumgebung](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  
  
2.  [Einrichten der Transformation von Ansprüchen auf vertrauenswürdige Gesamtstruktur (Adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  
  
3.  [Einrichten der Transformation von Ansprüchen in der vertrauenden Gesamtstruktur (Contoso)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  
  
4.  [Überprüfen Sie das Szenario](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  
  
## <a name="BKMK_1.1"></a>Richten Sie die Voraussetzungen und die testumgebung  
Die Testkonfiguration umfasst das Einrichten von zwei Gesamtstrukturen: Adatum Corporation und Contoso, Ltd lautet, und dass eine bidirektionale Vertrauensstellung zwischen Contoso und Adatum. "adatum.com" ist der vertrauenswürdigen Gesamtstruktur aus, und "contoso.com" lautet die vertrauende Gesamtstruktur.  
  
Ansprüche Transformation Szenario veranschaulicht Transformation eines Anspruchs in der vertrauenswürdigen Gesamtstruktur einem Anspruch in der vertrauenden Gesamtstruktur. Zu diesem Zweck müssen Sie zum Einrichten einer neuen Gesamtstruktur "adatum.com" aufgerufen, und füllen Sie die Gesamtstruktur mit einem Testbenutzer mit einem Unternehmens-Wert von "Adatum". Sie müssen eine bidirektionale Vertrauensstellung zwischen "contoso.com" und "adatum.com" einrichten.  
  
> [!IMPORTANT]  
> Beim Einrichten der Contoso und Adatum Gesamtstrukturen müssen Sie sicherstellen, dass der Root-Domänen unter Windows Server 2012 Funktionsebene der Domäne für die Anspruchstransformation arbeiten werden.  
  
Sie müssen die folgenden für die laborumgebung einrichten. Diese Verfahren werden ausführlich im [Anhang B: Einrichten der Testumgebung](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
Sie müssen die folgenden Verfahren zum Einrichten der testumgebung für dieses Szenario zu implementieren:  
  
1.  [Legen Sie Adatum als vertrauenswürdigen Gesamtstruktur Contoso](Appendix-B--Setting-Up-the-Test-Environment.md)  
  
2.  [Erstellen Sie den Anspruchstyp "Unternehmen" für Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  
  
3.  [Aktivieren der Ressourceneigenschaft "Company" auf Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  
  
4.  [Erstellen Sie die zentrale Zugriffsregel](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  
  
5.  [Erstellen Sie die zentrale Zugriffsrichtlinie](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  
  
6.  [Veröffentlichen der neuen Richtlinie über Gruppenrichtlinien](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  
  
7.  [Erstellen Sie den Ordner "Ergebnis" auf dem Dateiserver](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  
  
8.  [Festlegen von Klassifizierung, und wenden Sie die zentrale Zugriffsrichtlinie auf den neuen Ordner](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  
  
Verwenden Sie die folgende Informationen, um dieses Szenario zu vervollständigen:  
  
|Objekte|Details|  
|-----------|-----------|  
|Benutzer|Jeff Low, Contoso|  
|Benutzeransprüche auf Adatum "und" Contoso|ID: Ad: / / Ext/Unternehmen: ContosoAdatum,<br /><br />Quellattribut: Unternehmen<br /><br />Vorgeschlagene Werte: Contoso, Adatum **wichtig:** Sie müssen die ID für die "Unternehmen" Typ des Anspruchs auf Contoso und Adatum identisch für die Anspruchstransformation funktioniert festlegen.|  
|Zentrale Zugriffsregel für Contoso|AdatumEmployeeAccessRule|  
|Zentrale Zugriffsrichtlinie auf Contoso|Nur Adatum-Zugriffsrichtlinie|  
|Transformationsrichtlinien auf Adatum "und" Contoso-Ansprüche|DenyAllExcept Unternehmen|  
|Ordner für Contoso|D:\EARNINGS|  
  
## <a name="BKMK_3"></a>Einrichten der Transformation von Ansprüchen auf vertrauenswürdige Gesamtstruktur (Adatum)  
In diesem Schritt erstellen Sie eine transformationsrichtlinie in der Adatum, alle Ansprüche mit Ausnahme von "Unternehmen" für die Übergabe an Contoso zu verweigern.  
  
Das Active Directory-Modul für Windows PowerShell bietet die **DenyAllExcept** -Argument, das alles mit Ausnahme der angegebenen Ansprüche in der transformationsrichtlinie löscht.  
  
Um eine Transformation von Ansprüchen einzurichten, müssen Sie eine Ansprüche Transformation-Richtlinie erstellen und den vertrauenswürdigen als auch vertrauenden Gesamtstrukturen zu verknüpfen.  
  
### <a name="BKMK_2.2"></a>Erstellen einer Ansprüche Transformation-Richtlinie in Adatum  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>Zum Erstellen einer transformationsrichtlinie Adatum, alle Ansprüche, mit Ausnahme von "Unternehmen" zu verweigern.  
  
1.  Melden Sie sich bei dem Domänencontroller "adatum.com" als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except Company"`  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"adatum.com" `  
  
    ```  
  
### <a name="BKMK_2.3"></a>Legen Sie einen Ansprüche Transformation-Link für Adatum-Trust-Domain-Objekt  
In diesem Schritt wenden Sie die neu erstellte Transformation anspruchsrichtlinie auf Adatum Domäne Vertrauensstellungsobjekt für Contoso.  
  
##### <a name="to-apply-the-claims-transformation-policy"></a>Um die Ansprüche transformationsrichtlinie anzuwenden  
  
1.  Melden Sie sich bei dem Domänencontroller "adatum.com" als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  
  
    ```  
  
      Set-ADClaimTransformLink `  
    -Identity:"contoso.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    '"TrustRole:Trusted `  
  
    ```  
  
## <a name="BKMK_4"></a>Einrichten der Transformation von Ansprüchen in der vertrauenden Gesamtstruktur (Contoso)  
In diesem Schritt erstellen Sie eine Transformation anspruchsrichtlinie Contoso (der vertrauenden Gesamtstruktur), verweigern alle Ansprüche, mit Ausnahme von "Unternehmen". Sie müssen eine Ansprüche Transformation-Richtlinie erstellen und verknüpfen Sie sie mit der Gesamtstruktur-Vertrauensstellung.  
  
### <a name="BKMK_4.1"></a>Erstellen einer Ansprüche Transformation-Richtlinie in Contoso  
  
##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>Zum Erstellen einer transformationsrichtlinie Adatum, verweigern alle bis auf "Unternehmen"  
  
1.  Melden Sie sich an den Domänencontroller, "contoso.com" als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes:  
  
    ```  
    New-ADClaimTransformPolicy `  
    -Description:"Claims transformation policy to deny all claims except company" `  
    -Name:"DenyAllClaimsExceptCompanyPolicy" `  
    -DenyAllExcept:company `  
    -Server:"contoso.com" `  
  
    ```  
  
### <a name="BKMK_4.2"></a>Legen Sie einen Link der Ansprüche Transformation auf Contoso Domäne Vertrauensstellungsobjekt  
In diesem Schritt wenden Sie an die neu erstellte anspruchsrichtlinie der Transformation für das Domänencontrollerobjekt für "contoso.com" Vertrauensstellung für Adatum "Company" zu "contoso.com" übergeben werden. Das Domänenobjekt Vertrauensstellung heißt "adatum.com".  
  
##### <a name="to-set-the-claims-transformation-policy"></a>Die Ansprüche transformationsrichtlinie festlegen  
  
1.  Melden Sie sich an den Domänencontroller, "contoso.com" als Administrator mit dem Kennwort **pass@word1**.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes:  
  
    ```  
  
      Set-ADClaimTransformLink   
    -Identity:"adatum.com" `  
    -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
    -TrustRole:Trusting `  
  
    ```  
  
## <a name="BKMK_5"></a>Überprüfen Sie das Szenario  
In diesem Schritt versuchen Sie auf den D:\EARNINGS-Ordner zugegriffen, der eingerichtet wurde, auf dem Dateiserver "file1" zu überprüfen, ob der Benutzer Zugriff auf den freigegebenen Ordner hat.  
  
#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Um sicherzustellen, dass den Adatum-Benutzer kann den freigegebenen Ordner zuzugreifen.  
  
1.  Melden Sie sich an den Client Computer CLIENT1 als Jeff Low mit dem Kennwort **pass@word1**.  
  
2.  Navigieren Sie zum Ordner \\\FILE1.contoso.com\Earnings.  
  
3.  Jeff Low sollte auf den Ordner zugreifen können.  
  
## <a name="additional-scenarios-for-claims-transformation-policies"></a>Zusätzliche Szenarien für die Richtlinien für die Transformation von Ansprüchen  
Es folgt eine Liste der zusätzliche allgemeine Fälle, in der Transformation von Ansprüchen.  
  
|Szenario|Richtlinie|  
|------------|----------|  
|Können Sie alle Ansprüche, die Adatum-Gesamtstruktur auf Contoso-Adatum durchlaufen werden|Code: <br />New-ADClaimTransformPolicy \`<br /> -Description: "Ansprüche transformationsrichtlinie, damit alle Ansprüche" \`<br />-Name:"AllowAllClaimsPolicy" \`<br />-AllowAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsPolicy" \`<br />-TrustRole: Gewähren von vertrauen \`<br />-Server:"contoso.com" `|  
|Verweigern Sie alle Ansprüche, die von Adatum auf Contoso-Adatum durchlaufen stammen|Code: <br />New-ADClaimTransformPolicy \`<br />-Description: "Ansprüche transformationsrichtlinie für alle Ansprüche verweigern" \`<br />-Name:"DenyAllClaimsPolicy" \`<br /> -DenyAll \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br />-Identity:"adatum.com" \`<br />-Policy:"DenyAllClaimsPolicy" \`<br />-TrustRole: Gewähren von vertrauen \`<br />-Server:"contoso.com"`|  
|Können Sie alle Ansprüche, die Adatum-Gesamtstruktur mit Ausnahme von "Company" und "Department", um Contoso Adatum durchlaufen werden|Code <br />- New-ADClaimTransformationPolicy \`<br />-Description: "Ansprüche transformationsrichtlinie, damit alle Ansprüche, mit Ausnahme von Unternehmen" und "Department" \`<br /> -Name:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br />-AllowAllExcept: Unternehmen, die Abteilung \`<br />-Server:"contoso.com" \`<br />Set-ADClaimTransformLink \`<br /> -Identity:"adatum.com" \`<br />-Policy:"AllowAllClaimsExceptCompanyAndDepartmentPolicy" \`<br /> -TrustRole: Gewähren von vertrauen \`<br />-Server:"contoso.com" `|  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   Eine Liste aller Windows PowerShell-Cmdlets, die für die Transformation von Ansprüchen verfügbar sind, finden Sie unter [Active Directory-PowerShell-Cmdlet-Referenz](https://go.microsoft.com/fwlink/?LinkId=243150).  
  
-   Verwenden Sie für erweiterte Aufgaben, bei denen exportieren und Importieren der DAC-Konfigurationsinformationen zwischen zwei Gesamtstrukturen, die [Dynamic Access Control-PowerShell-Referenz](https://go.microsoft.com/fwlink/?LinkId=243150)  
  
-   [Bereitstellen von Ansprüchen über Gesamtstrukturen](Deploy-Claims-Across-Forests.md)  
  
-   [Ansprüche Transformation Regeln Sprache](Claims-Transformation-Rules-Language.md)  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  

