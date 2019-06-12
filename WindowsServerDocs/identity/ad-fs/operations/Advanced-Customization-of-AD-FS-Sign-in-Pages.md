---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: Erweiterte Anpassung von AD FS-Anmeldeseiten
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ee7bef2afe61500fe75b2d3c61b92b902f9757fa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444259"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung von AD FS-Anmeldeseiten

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung von AD FS-Anmeldeseite\-auf Seiten  
AD FS unter Windows Server 2012 R2 bietet integrierten\-in der Unterstützung für die Anmeldeseite anpassen\-Erfahrung. Bei einem Großteil der obigen Szenarios sind die integrierten\-in Windows PowerShell-Cmdlets sind alles, was erforderlich ist.  Es wird empfohlen, die Verwendung der integrierten\-melden Sie sich in Windows PowerShell-Befehle, um Standardelemente für AD FS anzupassen\-in Erfahrung, wann immer möglich.  Finden Sie unter [AD-FS-Anmeldung benutzeranpassung](AD-FS-user-sign-in-customization.md) für Weitere Informationen.  
  
In einigen Fällen AD FS-Administratoren können zusätzliche anmelden bereitstellen möchten\-in Umgebungen, die nicht über die vorhandenen PowerShell-Befehle in enthaltenen\-Feld mit AD FS. In einigen Fällen ist es möglich \(in den unten stehenden Richtlinien\) für Administratoren das Anpassen der Anmeldung von\-Erfahrung weiter durch zusätzliche Logik zum **onload.js** , wird von AD FS bereitgestellt und wird auf allen AD FS-Seiten ausgeführt.  
  
## <a name="things-to-know-before-you-start"></a>Wichtige Informationen, bevor Sie beginnen  
  
-   Jede Änderung, die wirkt sich auf die Umleitung Datenflüsse oder ändert die Parameter, denen mit AD FS funktioniert, wird nicht unterstützt.
  
-   Die ursprüngliche onload.js, eines, das das standardwebdesign, Lieferumfang enthält Code, der Seitenrendering für verschiedene Formfaktoren behandelt. Es wird empfohlen, nicht, ändern Sie den Inhalt der ursprünglichen onload.js, aber fügen Sie Ihren Code nur an den vorhandenen onload.js, der benutzerdefinierten Logik behandelt werden soll.  
  
-   AD FS im Lieferumfang eines integrierten\-im Design "Web" der standardmäßige aufgerufen wird. Sie können die onload.js, der das standardwebdesign nicht ändern. Um onload.js zu aktualisieren, müssen Sie erstellen und verwenden ein benutzerdefiniertes Webdesign, für die AD FS-Anmeldung\-in Seiten.  Finden Sie unter [AD-FS-Anmeldung benutzeranpassung](AD-FS-user-sign-in-customization.md) Informationen zur Vorgehensweise: Erstellen Sie ein benutzerdefiniertes Webdesign.  
  
-   Die gleichen onload.js führt auf allen AD FS-Seiten \(ex. Formular\--basierte Anmeldeseite "," Seite zur startbereichsermittlung "und" usw.\). Sie müssen sicherstellen, dass der Code in Ihrem Skript nur ausgeführt wird, ist nicht unerwartet ausgeführt und dient.  
  
-   Wenn Sie ein HTML-Element zu verweisen, stellen Sie sicher, dass Sie immer, ob das Element vor auf das Element vorhanden ist überprüfen. Dies bietet Stabilität und stellt sicher, dass die benutzerdefinierte Logik auf Seiten, die dieses Element nicht enthalten, nicht ausgeführt werden sollen. Sie können einfach den HTML-Quellcode auf die AD FS-Anmeldeseite anzeigen\-auf Seiten, um die vorhandenen Elemente anzuzeigen.  
  
-   Es wird dringend empfohlen, um Ihre Anpassungen in einer anderen Umgebung zu überprüfen und Testen Sie sie vor dem Rollback, in der Produktion AD FS-Server. Dies reduziert die Wahrscheinlichkeit, dass Endbenutzer diese Anpassungen vor der Überprüfung verfügbar gemacht werden.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Anpassen der AD FS-Anmeldeseite\-Erfahrung mit onload.js  
Verwenden Sie die folgenden Schritte aus, bei der Anpassung der onload.js für AD FS-Diensts.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>Anpassen von onload.js für den AD FS-Dienst  
  
1.  Um die benutzerdefinierte Logik onload.js hinzuzufügen, müssen Sie zunächst ein benutzerdefiniertes Webdesign erstellen. Das Design, das versandt wird\-von\-der\-Feld standardmäßig aufgerufen wird. Sie können das Standarddesign exportieren und verwenden, um schnell anzufangen. Das folgende Cmdlet erstellt ein benutzerdefiniertes Webdesign, das das standardwebdesign dupliziert:  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  Sie können dann exportieren die benutzerdefinierte oder eine Standardinstanz Webdesigns onload.js Datei abgerufen. Um ein Webdesign zu exportieren, verwenden Sie das folgende Cmdlet aus:  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    Sehen Sie onload.js unter dem Ordner "Skripts" im Verzeichnis, dass Sie im obigen Cmdlet Export angeben, und fügen die benutzerdefinierte Logik für das Skript \(finden Sie unter Anwendungsfälle im folgenden Beispielabschnitt\).  
  
3.  Stellen Sie die erforderlichen Änderungen onload.js basierend auf Ihren Anforderungen anpassen.  
  
4.  Aktualisieren Sie das Design, mit der geänderten onload.js. Verwenden Sie das folgende Cmdlet aus, um die benutzerdefinierten Webdesigns für das Update onload.js zuweisen:  

     Für AD FS unter Windows Server 2012 R2:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}  
  
    ```  
    Für AD FS unter WindowsServer 2016:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\ADFStheme\script\onload.js"   
  
    ```  
  
5.  Verwenden Sie zum Anwenden des benutzerdefinierten Webdesigns für AD FS das folgende Cmdlet aus:  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>Beispiele für die weitere Anpassung  
Im folgenden sind die Beispiele von benutzerdefiniertem Code hinzugefügt onload.js für verschiedene Fine\-zu optimieren. Beim Hinzufügen des benutzerdefinierten Codes fügen Sie Ihren benutzerdefinierten Code immer am unteren Rand der onload.js.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>Beispiel 1: Ändern der Zeichenfolge "Mit Unternehmenskonto anmelden"  
Das Standard-AD FS-Form\-basierend anmelden\-verfügt einen Titel mit "Mit Ihrem Unternehmenskonto anmelden" über die Eingabefelder für Benutzer.  
  
Wenn Sie diese Zeichenfolge durch Ihre eigenen ersetzen möchten, können Sie den folgenden Code zum onload.js hinzufügen.  
  
```  
// Sample code to change “Sign in with organizational account” string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>Beispiel 2: akzeptieren SAM\-Kontoname als Anmeldung Format in eine AD FS-Formular\-basierend anmelden\-auf Seite  
Das Standard-AD FS-Form\-basierend anmelden\-Seite unterstützt Anmeldung Format Benutzerprinzipalnamen \(UPNs\) \(z. B. <strong>johndoe@contoso.com</strong> \) oder Domäne qualifiziert Sam\-Kontonamen \( **Contoso\\Johndoe** oder **"contoso.com"\\Johndoe**\). Falls alle Benutzer aus derselben Domäne stammen, und sie nur zu den Sam Informationen\-Kontonamen, Sie möchten das Szenario, in denen die Benutzer können sich anmelden, zu unterstützen, bei der Nutzung Sam\-Konto nur Namen. Sie können den folgenden Code hinzufügen, um onload.js unterstützen dieses Szenario, ersetzen Sie die Domäne "contoso.com" im Beispiel unten einfach mit der Domäne, die Sie verwenden möchten.  
  
```  
if (typeof Login != 'undefined'){  
    Login.submitLoginRequest = function () {   
    var u = new InputUtil();  
    var e = new LoginErrors();  
    var userName = document.getElementById(Login.userNameInput);  
    var password = document.getElementById(Login.passwordInput);  
    if (userName.value && !userName.value.match('[@\\\\]'))   
    {  
        var userNameValue = 'contoso.com\\' + userName.value;  
        document.forms['loginForm'].UserName.value = userNameValue;  
    }  
  
    if (!userName.value) {  
       u.setError(userName, e.userNameFormatError);  
       return false;  
    }  
  
    if (!password.value)   
    {  
        u.setError(password, e.passwordEmpty);  
        return false;  
    }  
    document.forms['loginForm'].submit();  
    return false;  
};  
}  
  
```  
  
## <a name="additional-references"></a>Weitere Verweise 
[AD FS-Anmeldung Benutzeranpassung](AD-FS-user-sign-in-customization.md)  
  

