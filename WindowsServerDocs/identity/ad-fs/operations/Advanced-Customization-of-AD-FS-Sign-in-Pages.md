---
ms.assetid: 882abec8-0189-4f73-99c5-792987168080
title: Erweiterte Anpassung der AD FS Anmelde Seiten
author: billmath
ms.author: billmath
manager: femila
ms.date: 01/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ea149e6b9a5fbf5c0671991a61f9bcda35656022
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859983"
---
# <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung der AD FS Anmelde Seiten

  
## <a name="advanced-customization-of-ad-fs-sign-in-pages"></a>Erweiterte Anpassung der AD FS Sign\-in Pages  
AD FS in Windows Server 2012 R2 bietet integrierte\-zur Unterstützung der Anpassung der Anmelde\-. In den meisten Fällen sind nur die integrierten\-in den Windows PowerShell-Cmdlets erforderlich.  Es wird empfohlen, dass Sie die erstellten\-in Windows PowerShell-Befehlen verwenden, um Standardelemente für das AD FS Signieren\-in der-Funktion zu verwenden, wenn möglich.  Weitere Informationen finden Sie [unter Anpassung an die AD-FS-Benutzeranmeldung](AD-FS-user-sign-in-customization.md) .  
  
In einigen Fällen können AD FS Administratoren zusätzliche Anmelde\-in Umgebungen bereitstellen, die über die vorhandenen PowerShell-Befehle, die\-Box mit AD FS ausgeliefert werden, nicht möglich sind. In bestimmten Fällen ist es möglich, \(in den unten aufgeführten Richtlinien zu\), damit Administratoren das Anmelden\-in der Umgebung weiter anpassen können, indem Sie " **OnLoad. js** " zusätzliche Logik hinzufügen, die von AD FS bereitgestellt wird und auf allen AD FS Seiten ausgeführt wird.  
  
## <a name="things-to-know-before-you-start"></a>Dinge, die Sie kennen müssen, bevor Sie beginnen  
  
-   Jede Änderung, die Auswirkungen auf die Umleitung oder die Änderung von Protokoll Parametern hat, mit denen AD FS funktioniert, wird nicht unterstützt.
  
-   Die ursprüngliche Datei "OnLoad. js", die im Standard-Webdesign enthalten ist, enthält Code, der das Seiten Rendering für verschiedene Formfaktoren behandelt. Es wird empfohlen, den ursprünglichen OnLoad. js-Inhalt nicht zu ändern, sondern nur den Code an die vorhandene "OnLoad. js" anzufügen, die benutzerdefinierte Logik behandelt.  
  
-   AD FS wird mit einem erstellten\-im Webdesign ausgeliefert, das als Default bezeichnet wird. "OnLoad. js" kann nicht im Standard-Webdesign geändert werden. Zum Aktualisieren von "OnLoad. js" müssen Sie ein benutzerdefiniertes Webdesign erstellen und verwenden, um AD FS\-in Seiten zu signieren.  Informationen zum Erstellen eines benutzerdefinierten Webdesigns finden Sie [unter AD-FS-Benutzeranmeldung](AD-FS-user-sign-in-customization.md) .  
  
-   Dieselbe "OnLoad. js" wird auf allen ADFS-Seiten \(Ex ausgeführt. Formular\-basierten Anmeldeseite, Seite "Startbereichs Ermittlung" und "\)". Sie müssen sicherstellen, dass der Code in Ihrem Skript nur ausgeführt wird, wenn er entworfen wurde und nicht unerwartet ausgeführt wird.  
  
-   Wenn Sie auf ein beliebiges HTML-Element verweisen, stellen Sie sicher, dass Sie immer das vorhanden sein des Elements überprüfen, bevor Sie für das Element agieren. Dadurch wird die Stabilität gewährleistet, und es wird sichergestellt, dass die benutzerdefinierte Logik nicht auf Seiten ausgeführt wird, die dieses Element nicht enthalten. Sie können die HTML-Quelle einfach auf dem AD FS\-auf den Seiten anzeigen, um die vorhandenen Elemente anzuzeigen.  
  
-   Es wird dringend empfohlen, die Anpassungen in einer alternativen Umgebung zu überprüfen und zu testen, bevor Sie Sie auf Produktions AD FS Servern Rollout. Dadurch wird die Wahrscheinlichkeit verringert, dass Endbenutzer diese Anpassungen vor der Validierung ausgesetzt werden.  
  
## <a name="customizing-the-ad-fs-sign-in-experience-by-using-onloadjs"></a>Anpassen des AD FS Sign\-in der Umgebung mithilfe von "OnLoad. js"  
Führen Sie die folgenden Schritte aus, wenn Sie "OnLoad. js" für den AD FS-Dienst anpassen.  
  
#### <a name="customizing-onloadjs-for-the-ad-fs-service"></a>Anpassen von "OnLoad. js" für den AD FS-Dienst  
  
1.  Um die benutzerdefinierte Logik zu "OnLoad. js" hinzuzufügen, müssen Sie zunächst ein benutzerdefiniertes Webdesign erstellen. Das Design, das\-von\-dem\-Feld ausgeliefert wird, wird als Standard bezeichnet. Sie können das Standarddesign exportieren und verwenden, um schnell anzufangen. Mit dem folgenden Cmdlet wird ein benutzerdefiniertes Webdesign erstellt, das das Standardweb Design dupliziert:  
  
    ```  
    New-AdfsWebTheme –Name custom –SourceName default  
  
    ```  
  
2.  Sie können dann das benutzerdefinierte oder standardmäßige Webdesign exportieren, um die Datei "OnLoad. js" zu erhalten. Verwenden Sie zum Exportieren eines Webdesigns das folgende Cmdlet:  
  
    ```  
    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  
  
    ```  
  
    Sie finden "OnLoad. js" im Skript Ordner in dem Verzeichnis, das Sie im obigen Cmdlet "Export" angegeben haben, und fügen die benutzerdefinierte Logik zum Skript hinzu, \(im Beispiel Abschnitt unten\)die Anwendungsfälle anzuzeigen.  
  
3.  Nehmen Sie die notwendigen Änderungen vor, um OnLoad. js je nach Bedarf anzupassen.  
  
4.  Aktualisieren Sie das Design mit der geänderten OnLoad. js. Verwenden Sie das folgende Cmdlet, um das Update OnLoad. js auf das benutzerdefinierte Webdesign anzuwenden:  

     Für AD FS unter Windows Server 2012 R2:  

    ```  
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}  
  
    ```  
    Für AD FS unter Windows Server 2016:

     ```  
    Set-AdfsWebTheme -TargetName custom -OnLoadScriptPath "c:\ADFStheme\script\onload.js"   
  
    ```  
  
5.  Verwenden Sie das folgende Cmdlet, um das benutzerdefinierte Webdesign auf AD FS anzuwenden:  
  
    ```  
    Set-AdfsWebConfig -ActiveThemeName custom  
    ```  
  
## <a name="additional-customization-examples"></a>Weitere Anpassungs Beispiele  
Im folgenden finden Sie die Beispiele für benutzerdefinierten Code, der "OnLoad. js" für verschiedene fein\-optimiert wurde. Wenn Sie den benutzerdefinierten Code hinzufügen, fügen Sie Ihren benutzerdefinierten Code immer am Ende der Datei "OnLoad. js" an.  
  
### <a name="example-1-change-sign-in-with-organizational-account-string"></a>Beispiel 1: Ändern der Zeichenfolge "Anmelden mit dem Organisations Konto"  
Die Standard AD FS Formular\-basierte Anmelde\-auf der Seite hat den Titel "Anmelden mit Ihrem Organisations Konto" oberhalb der Benutzereingabe Felder.  
  
Wenn Sie diese Zeichenfolge durch ihre eigene Zeichenfolge ersetzen möchten, können Sie "OnLoad. js" den folgenden Code hinzufügen.  
  
```  
// Sample code to change "Sign in with organizational account" string.  
  
// Check whether the loginMessage element is present on this page.  
var loginMessage = document.getElementById('loginMessage');  
if (loginMessage)  
{  
       // loginMessage element is present, modify its properties.  
       loginMessage.innerHTML = 'Your company description text';  
}  
  
```  
  
### <a name="example-2-accept-sam-account-name-as-a-login-format-on-an-ad-fs-form-based-sign-in-page"></a>Beispiel 2: akzeptieren Sie Sam\-Account Name als Anmelde Format auf einem AD FS Formular\-basierten Anmelde\-auf der Seite.  
Die standardmäßige AD FS Formular\-basierte Anmelde\-auf der Seite unterstützt das Anmelde Format von Benutzer Prinzipal Namen \(UPNs <strong>\) \(z</strong> . b.johndoe@contoso.com\) oder Domänen qualifizierte Sam\--Kontonamen **contoso.com\\johndoe** **\(** von von.\\\) Wenn alle Benutzer von derselben Domäne stammen und Sie nur über Sam\-Kontonamen wissen, können Sie das Szenario unterstützen, in dem sich die Benutzer mit Ihnen anmelden können, wenn Sie nur die Kontonamen von Sam\-. Sie können den folgenden Code zu "OnLoad. js" hinzufügen, um dieses Szenario zu unterstützen. ersetzen Sie einfach die Domäne "contoso.com" im folgenden Beispiel durch die Domäne, die Sie verwenden möchten.  
  
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
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
  

