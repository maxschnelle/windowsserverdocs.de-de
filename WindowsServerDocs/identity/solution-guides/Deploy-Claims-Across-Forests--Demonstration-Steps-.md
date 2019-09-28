---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6045c144a0da399e8279c781273235942316e538
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407128"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>Bereitstellen von Ansprüchen über Gesamtstrukturen (Demonstrationsschritte)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird ein grundlegendes Szenario behandelt, in dem erläutert wird, wie Anspruchs Transformationen zwischen vertrauenswürdigen und vertrauenswürdigen Gesamtstrukturen konfiguriert werden. Sie erfahren, wie Anspruchs Transformations-Richtlinien Objekte erstellt und mit der Vertrauensstellung für die vertrauende Gesamtstruktur und die vertrauenswürdige Gesamtstruktur verknüpft werden können. Anschließend überprüfen Sie das Szenario.  

## <a name="scenario-overview"></a>Szenarioübersicht  
Adatum Corporation bietet Finanzdienstleistungen für Conto so, Ltd. In den einzelnen Quartalen kopiert Adatum Accountants die Konto Kalkulations Tabellen in einen Ordner auf einem Dateiserver, der sich in der Datei "CSO, Ltd." befindet. Es gibt eine bidirektionale Vertrauensstellung von "Configuration Manager" zu adatum. Die gemeinsame Nutzung von "Adatum" durch die Mitarbeiter von "Configuration Manager" möchte so geschützt werden, dass nur Administratoren auf die Remote Freigabe zugreifen können.  

In diesem Szenario:  

1.  [Einrichten der Voraussetzungen und der Testumgebung](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)  

2.  [Einrichten der Anspruchs Transformation in einer vertrauenswürdigen Gesamtstruktur (Adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)  

3.  [Einrichten der Anspruchs Transformation in der vertrauenden Gesamtstruktur ("Configuration Manager")](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)  

4.  [Überprüfen des Szenarios](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)  

## <a name="BKMK_1.1"></a>Einrichten der Voraussetzungen und der Testumgebung  
Die Testkonfiguration umfasst das Einrichten von zwei Gesamtstrukturen: Adatum Corporation und contodso, Ltd. und haben eine bidirektionale Vertrauensstellung zwischen conbeso und adatum. "adatum.com" ist die vertrauenswürdige Gesamtstruktur, und "contoso.com" ist die vertrauenswürdige Gesamtstruktur.  

Das Anspruchs Transformations Szenario veranschaulicht die Transformation eines Anspruchs in der vertrauenswürdigen Gesamtstruktur zu einem Anspruch in der vertrauenden Gesamtstruktur. Zu diesem Zweck müssen Sie eine neue Gesamtstruktur mit dem Namen Adatum.com einrichten und die Gesamtstruktur mit einem Test Benutzer mit dem Unternehmenswert "Adatum" auffüllen. Sie müssen dann eine bidirektionale Vertrauensstellung zwischen contoso.com und adatum.com einrichten.  

> [!IMPORTANT]  
> Beim Einrichten der Gesamtstrukturen von "Configuration Manager" und "Adatum" müssen Sie sicherstellen, dass sich beide Stamm Domänen auf der Domänen Funktionsebene von Windows Server 2012 befinden, damit die Transformation von Ansprüchen funktioniert.  

Sie müssen Folgendes für das Lab einrichten: Diese Prozeduren werden in [anhang B ausführlich erläutert: Einrichten der Testumgebung](Appendix-B--Setting-Up-the-Test-Environment.md)  

Sie müssen die folgenden Verfahren implementieren, um das Lab für dieses Szenario einzurichten:  

1.  [Adatum als vertrauenswürdige Gesamtstruktur auf "Configuration Manager" festlegen](Appendix-B--Setting-Up-the-Test-Environment.md)  

2.  [Erstellen Sie den Anspruchstyp "Company" in "Configuration Manager".](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)  

3.  [Aktivieren der Ressourcen Eigenschaft "Company" für "Configuration Manager"](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)  

4.  [Erstellen der zentralen Zugriffs Regel](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)  

5.  [Erstellen der zentralen Zugriffs Richtlinie](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)  

6.  [Veröffentlichen der neuen Richtlinie über Gruppenrichtlinie](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)  

7.  [Erstellen des Ordners "Ergebnis" auf dem Dateiserver](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)  

8.  [Klassifizierung festlegen und die zentrale Zugriffs Richtlinie auf den neuen Ordner anwenden](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)  

Verwenden Sie die folgenden Informationen, um dieses Szenario abzuschließen:  

|Gütern|Details|  
|-----------|-----------|  
|Benutzer|Jeff Low, Configuration Manager|  
|Benutzer Ansprüche für "Adatum" und "Configuration Manager"|ID: AD://ext/Company:ContosoAdatum,<br /><br />Quell Attribut: Company<br /><br />Vorgeschlagene Werte: "Adatum", **wichtig:** Sie müssen die ID für den Anspruchstyp "Company" sowohl für "" als auch für "Adatum" festlegen, damit die Anspruchs Transformation funktioniert.|  
|Zentrale Zugriffs Regel für "Configuration Manager"|Adatumemployeeaccessrule ein|  
|Zentrale Zugriffs Richtlinie für "Configuration Manager"|Nur adatum-Zugriffs Richtlinie|  
|Anspruchs Transformations Richtlinien für "Adatum" und "Configuration Manager"|Denyallexcept Company|  
|Datei Ordner auf "Configuration Manager"|D:\GEWINN|  

## <a name="BKMK_3"></a>Einrichten der Anspruchs Transformation in einer vertrauenswürdigen Gesamtstruktur (Adatum)  
In diesem Schritt erstellen Sie eine Transformations Richtlinie in Adatum, um alle Ansprüche außer "Company" zu verweigern, die an "Configuration Manager" übergeben werden.  

Das Active Directory-Modul für Windows PowerShell stellt das **denyallexcept** -Argument bereit, das alles außer den angegebenen Ansprüchen in der Transformations Richtlinie löscht.  

Zum Einrichten einer Anspruchs Transformation müssen Sie eine Anspruchs Transformations Richtlinie erstellen und diese zwischen den vertrauenswürdigen und vertrauenswürdigen Gesamtstrukturen verknüpfen.  

### <a name="BKMK_2.2"></a>Erstellen einer Anspruchs Transformations Richtlinie in adatum  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>So erstellen Sie eine Transformations Richtlinien-Adatum, um alle Ansprüche außer "Company" abzulehnen  

1. Melden Sie sich beim Domänen Controller adatum.com als Administrator mit dem Kennwort <strong>pass@word1</strong>an.  

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except Company"`  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"adatum.com" `  

   ```  

### <a name="BKMK_2.3"></a>Festlegen eines Anspruchs Transformations Links auf dem vertrauenswürdigen Domänen Objekt von adatum  
In diesem Schritt wenden Sie die neu erstellte Anspruchs Transformations Richtlinie auf das Vertrauensstellungs Domänen Objekt von Adatum für "Configuration Manager" an.  

##### <a name="to-apply-the-claims-transformation-policy"></a>So wenden Sie die Anspruchs Transformations Richtlinie an  

1. Melden Sie sich beim Domänen Controller adatum.com als Administrator mit dem Kennwort <strong>pass@word1</strong>an.  

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  

   ```  

     Set-ADClaimTransformLink `  
   -Identity:"contoso.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   '"TrustRole:Trusted `  

   ```  

## <a name="BKMK_4"></a>Einrichten der Anspruchs Transformation in der vertrauenden Gesamtstruktur ("Configuration Manager")  
In diesem Schritt erstellen Sie eine Anspruchs Transformations Richtlinie in "tentoso" (die vertrauende Gesamtstruktur), um alle Ansprüche außer "Company" abzulehnen. Sie müssen eine Richtlinie für die Anspruchs Transformation erstellen und Sie mit der Gesamtstruktur-Vertrauensstellung verknüpfen.  

### <a name="BKMK_4.1"></a>Erstellen einer Anspruchs Transformations Richtlinie in "Configuration Manager"  

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>So erstellen Sie eine Transformations Richtlinien-Adatum, um alle außer "Company" abzulehnen  

1. Melden Sie sich beim Domänen Controller contoso.com als Administrator mit dem Kennwort <strong>pass@word1</strong>an.  

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  

   ```  
   New-ADClaimTransformPolicy `  
   -Description:"Claims transformation policy to deny all claims except company" `  
   -Name:"DenyAllClaimsExceptCompanyPolicy" `  
   -DenyAllExcept:company `  
   -Server:"contoso.com" `  

   ```  

### <a name="BKMK_4.2"></a>Festlegen eines Anspruchs Transformations Links auf dem vertrauenswürdigen Domänen Objekt von Configuration Manager  
In diesem Schritt wenden Sie die neu erstellte Anspruchs Transformations Richtlinie auf das Domänen Objekt contoso.com Trust für Adatum an, um das Weitergeben von "Company" an contoso.com zuzulassen. Das vertrauenswürdige Domänen Objekt hat den Namen Adatum.com.  

##### <a name="to-set-the-claims-transformation-policy"></a>So legen Sie die Anspruchs Transformations Richtlinie fest  

1. Melden Sie sich beim Domänen Controller contoso.com als Administrator mit dem Kennwort <strong>pass@word1</strong>an.  

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten in Windows PowerShell, und geben Sie Folgendes ein:  

   ```  

     Set-ADClaimTransformLink   
   -Identity:"adatum.com" `  
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `  
   -TrustRole:Trusting `  

   ```  

## <a name="BKMK_5"></a>Überprüfen des Szenarios  
In diesem Schritt versuchen Sie, auf den Ordner "d:\gewinn" zuzugreifen, der auf dem Dateiserver eingerichtet wurde file1 um zu überprüfen, ob der Benutzer Zugriff auf den freigegebenen Ordner hat.  

#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>So stellen Sie sicher, dass der Adatum-Benutzer auf den freigegebenen Ordner zugreifen kann  

1. Melden Sie sich am Client Computer an, CLIENT1 als Jeff Low mit dem Kennwort <strong>pass@word1</strong>.  

2. Navigieren Sie zum Ordner \\ \ file1.................  

3. Jeff Low sollte auf den Ordner zugreifen können.  

## <a name="additional-scenarios-for-claims-transformation-policies"></a>Weitere Szenarios für Anspruchs Transformations Richtlinien  
Im folgenden finden Sie eine Liste der zusätzlichen häufigen Fälle bei der Transformation von Ansprüchen.  


|                                                 Szenario                                                 |                                                                                                                                                                                                                                           Richtlinie                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  Zulassen, dass alle Ansprüche, die von Adatum stammen, an den "Configuration Manager"-adatum weitergeleitet werden                  |                                                          Ordnung <br />New-adclaimtransformpolicy \`<br /> -Description: "Anspruchs Transformations Richtlinie, um alle Ansprüche zuzulassen" \`<br />-Name: "zuder Name der" Zuweisung "\`<br />-Zuweisung \`<br />-Server:"contoso. com" \`<br />Set-adclaimtransformlink \`<br />-Identity:"adatum. com" \`<br />-Policy: "' zuder ' zuder Wert ' zu\`<br />-Trustrole: vertrauende \`<br />-Server:"contoso. com" \`                                                          |
|                  Verweigern, dass alle Ansprüche, die von Adatum stammen, an den "Configuration Manager"-adatum weitergeleitet werden                   |                                                            Ordnung <br />New-adclaimtransformpolicy \`<br />-Description: "Anspruchs Transformations Richtlinie, um alle Ansprüche abzulehnen" \`<br />-Name: "denyallclaimspolicy" \`<br /> -Denyall \`<br />-Server:"contoso. com" \`<br />Set-adclaimtransformlink \`<br />-Identity:"adatum. com" \`<br />-Policy: "denyallclaimspolicy" \`<br />-Trustrole: vertrauende \`<br />-Server:"contoso. com" \`                                                             |
| Zulassen, dass alle Ansprüche, die von Adatum ausgenommen sind, mit Ausnahme von "Company" und "Department" zu "Adatum" von "Configuration" wechseln | Code <br />-New-adclaimtransformationpolicy \`<br />-Description: "Anspruchs Transformations Richtlinie, um alle Ansprüche außer Unternehmen und Abteilung zuzulassen" \`<br /> -Name: "Zustellungs-" Zustellungs-\`<br />-Zuweisung: Company, Department \`<br />-Server:"contoso. com" \`<br />Set-adclaimtransformlink \`<br /> -Identity:"adatum. com" \`<br />-Richtlinie: "Zustellungs-" Zustellungs-\`<br /> -Trustrole: vertrauende \`<br />-Server:"contoso. com" \` |

## <a name="BKMK_Links"></a>Siehe auch  

-   Eine Liste aller Windows PowerShell-Cmdlets, die für die Transformation von Ansprüchen verfügbar sind, finden Sie unter [Active Directory PowerShell-Cmdlet-Referenz](https://go.microsoft.com/fwlink/?LinkId=243150).  

-   Verwenden Sie für erweiterte Aufgaben, die den Export und Import von DAC-Konfigurationsinformationen zwischen zwei Gesamtstrukturen umfassen, die [dynamische Access Control PowerShell-Referenz](https://go.microsoft.com/fwlink/?LinkId=243150) .  

-   [Gesamtstrukturübergreifendes Bereitstellen von Ansprüchen](Deploy-Claims-Across-Forests.md)  

-   [Sprache zum Schreiben von Regeln für die Transformation von Ansprüchen](Claims-Transformation-Rules-Language.md)  

-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  


