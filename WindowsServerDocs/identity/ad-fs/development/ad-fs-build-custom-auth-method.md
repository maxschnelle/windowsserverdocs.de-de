---
title: Erstellen einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server
description: In diesem Szenario wird beschrieben, wie eine benutzerdefinierte Authentifizierungsmethode für AD FS in Windows Server erstellt wird.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2ef16ddeb241d55b61b484805ff91cb247985d8d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358885"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Erstellen einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server

Diese exemplarische Vorgehensweise enthält Anweisungen zum Implementieren einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2. Weitere Informationen finden Sie unter [zusätzliche Authentifizierungsmethoden](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\)).


> [!WARNING]
> Das Beispiel, das Sie hier erstellen können&nbsp;, dient nur zu Schulungszwecken. &nbsp;Diese Anweisungen gelten für die einfachste, kleinste Implementierung, die die erforderlichen Elemente des Modells verfügbar machen kann.&nbsp; Es gibt keine Authentifizierungs-Back-End-, Fehler-oder Konfigurationsdaten. 
> <P></P>



## <a name="setting-up-the-development-box"></a>Einrichten der Entwicklungs Box

In dieser exemplarischen Vorgehensweise wird Visual Studio 2012 verwendet.  Das Projekt kann mit einer beliebigen Entwicklungsumgebung erstellt werden, die eine .NET-Klasse für Windows erstellen kann. Das Projekt muss .NET 4,5 als Ziel verwenden, da die **beginauthentication** -Methode und die **tryendauthentication** -Methode den Typ **System. Security. Claims. Claim**verwenden, der Teil von .NET Framework Version 4.5 ist. für das Projekt ist ein Verweis erforderlich:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Verweis-dll</strong></p></td>
<td><p><strong>Speicherort für die Suche</strong></p></td>
<td><p><strong>Erforderlich für</strong></p></td>
</tr>
<tr class="even">
<td><p>Microsoft. identityserver. Web. dll</p></td>
<td><p>Die dll befindet sich in%windir%\adfs auf einem Windows Server 2012 R2-Server, auf dem AD FS installiert wurde.</p>
<p></p>
<p>Diese DLL muss auf den Entwicklungs Computer kopiert werden, und es muss ein expliziter Verweis im Projekt erstellt werden.</p></td>
<td><p>Schnittstellentypen, einschließlich iauthenticationcontext, iproosdata</p></td>
</tr>
</tbody>
</table>


## <a name="create-the-provider"></a>Erstellen des Anbieters

1.  In Visual Studio 2012: Wählen Sie Datei\>-neu\>-Projekt... aus.

2.  Wählen Sie Klassenbibliothek aus, und stellen Sie sicher, dass Sie auf .NET 4,5 abzielen.

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "Erstellen des Anbieters")

3.  Erstellen Sie eine Kopie von **Microsoft. identityserver. Web. dll** aus% windir% \\adfs auf dem Windows Server 2012 R2-Server, auf dem AD FS installiert wurde, und fügen Sie ihn in Ihren Projektordner auf dem Entwicklungs Computer ein.

4.  Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf **Verweise** , und **fügen Sie einen Verweis hinzu.**

5.  Navigieren Sie zu Ihrer lokalen Kopie von **Microsoft. identityserver. Web. dll** , und **fügen Sie hinzu...**

6.  Klicken Sie auf **OK** , um den neuen Verweis zu bestätigen:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "Erstellen des Anbieters")

    Nun sollten Sie so eingerichtet sein, dass alle für den Anbieter erforderlichen Typen aufgelöst werden. 

7.  Fügen Sie dem Projekt eine neue Klasse hinzu (Klicken Sie mit der rechten Maustaste auf das Projekt, und **fügen Sie hinzu. Klasse...** ) und weisen Sie ihm einen Namen wie **myAdapter**zu, wie unten dargestellt:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "Erstellen des Anbieters")

8.  Ersetzen Sie den vorhandenen Code in der neuen Datei MyAdapter.cs durch den folgenden Code:

        using System;
         using System.Collections.Generic;
         using System.Linq;
         using System.Text;
         using System.Threading.Tasks;
         using System.Globalization;
         using System.IO;
         using System.Net;
         using System.Xml.Serialization;
         using Microsoft.IdentityServer.Web.Authentication.External;
         using Claim = System.Security.Claims.Claim;

         namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {

         }
         }

    Jetzt sollten Sie F12 (mit der rechten Maustaste auf – Gehe zu Definition) auf iauthenticationadapter anzeigen können, um den Satz erforderlicher Schnittstellenmember anzuzeigen. 

    Als nächstes können Sie eine einfache Implementierung dieser Aktionen ausführen.

9.  Ersetzen Sie den gesamten Inhalt der Klasse durch Folgendes:

        namespace MFAadapter
         {
         class MyAdapter : IAuthenticationAdapter
         {
         public IAuthenticationAdapterMetadata Metadata
         {
         //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
         }

         public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
         {
         return true; //its all available for now

         }

         public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
         {
         //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

         }

         public void OnAuthenticationPipelineUnload()
         {

         }

         public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
         {
         //return new instance of IAdapterPresentationForm derived class

         }

         }
         }

10. Wir sind noch nicht bereit, zu erstellen... Es gibt zwei weitere Schnittstellen.

    Fügen Sie dem Projekt zwei weitere Klassen hinzu: eine für die Metadaten und die andere für das Präsentations Formular.  Sie können diese innerhalb derselben Datei wie die oben genannte Klasse hinzufügen.

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. Als nächstes können Sie die erforderlichen Elemente für jede hinzufügen. Zuerst die Metadaten (mit hilfreichen Inline Kommentaren)

        class MyMetadata : IAuthenticationAdapterMetadata
         {
         //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
         public string AdminName
         {
         get { return "My Example MFA Adapter"; }
         }

         //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter 
         /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
         /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
         /// one of the methods listed in this property, the authentication attempt will fail.
         public virtual string[] AuthenticationMethods 
         {
         get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
         }

         /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
         /// to determine the best language\locale to display to the user.
         public int[] AvailableLcids
         {
         get
         {
         return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
         }
         }

         /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid. 
         /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than 
         /// one secondary authentication provider available.
         public Dictionary<int, string> FriendlyNames
         {
         get
         {
         Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
         _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
         _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
         return _friendlyNames;
         }
         }

         /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid. 
         /// These descriptions are displayed in the "choice page" offered to the user when there is more than one 
         /// secondary authentication provider available.
         public Dictionary<int, string> Descriptions
         {
         get 
         {
         Dictionary<int, string> _descriptions = new Dictionary<int, string>();
         _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
         _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
         return _descriptions; 
         }
         }

         /// Returns an array indicating the type of claim that the adapter uses to identify the user being authenticated.
         /// Note that although the property is an array, only the first element is currently used.
         /// MUST BE ONE OF THE FOLLOWING
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
         public string[] IdentityClaims
         {
         get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
         }

         //All external providers must return a value of "true" for this property.
         public bool RequiresIdentity
         {
         get { return true; }
         }
        }

    Im nächsten Schritt wird das Präsentations Formular angezeigt:

        class MyPresentationForm : IAdapterPresentationForm
         {
         /// Returns the HTML Form fragment that contains the adapter user interface. This data will be included in the web page that is presented
         /// to the cient.
         public string GetFormHtml(int lcid)
         {
         string htmlTemplate = Resources.FormPageHtml; //todo we will implement this
         return htmlTemplate;
         }

         /// Return any external resources, ie references to libraries etc., that should be included in 
         /// the HEAD section of the presentation form html. 
         public string GetFormPreRenderHtml(int lcid)
         {
         return null;
         }

         //returns the title string for the web page which presents the HTML form content to the end user
         public string GetPageTitle(int lcid)
         {
         return "MFA Adapter";
         }


~~~
     }
~~~

12. Beachten Sie das "ToDo"-Element für das **Resources. formpgehtml** -Element oben. 

   Sie können Sie in einer Minute korrigieren, aber zuerst fügen wir die letzten erforderlichen Return-Anweisungen, die auf den neu implementierten Typen basieren, zu Ihrer anfänglichen myAdapter-Klasse hinzu.  Fügen Sie hierzu die folgenden Elemente in *kursiv* Schrift der vorhandenen iauthenticationadapter-Implementierung hinzu:

       Class myAdapter: Iauthenticationadapter {Public iauthenticationadaptermetadata-Metadaten {//get {return <instance of IAuthenticationAdapterMetadata derived class>New;}     get {return new MyMetadata ();}     }

        public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
        {
        return true; //its all available for now
        }

        public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
        {
        //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

        }

        public void OnAuthenticationPipelineUnload()
        {

        }

        public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
        {
        //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
        }

        public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
        {
        //return new instance of IAdapterPresentationForm derived class
        outgoingClaims = new Claim[0];
        return new MyPresentationForm();
        }

        }

13. Jetzt für die Ressourcen Datei, die das HTML-Fragment enthält. Erstellen Sie eine neue Textdatei in Ihrem Projektordner mit folgendem Inhalt:

       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">Dieser Inhalt wird vom MFA-Beispieladapter bereitgestellt. Die Abfrage Eingaben sollten unten dargestellt werden.</p>
        <label for="challengeQuestionInput" class="block">question Text @ no__t-1 @ no__t-2 @ no__t-3<div id="submissionArea" class="submitMargin">
        <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
        </div>
        </form>
        <div id="intro" class="groupMargin">
        <p id="supportEmail">Supportinformationen</p>
        </div>
        <script type="text/javascript" language="JavaScript">
        //<![CDATA[
        function AuthPage() { }
        AuthPage.submitAnswer = function () { return true; };
        //]]>
        </script></div>

14. Wählen Sie **dann Projekt-\>Komponente hinzufügen aus. Ressourcen** Datei, benennen Sie die Datei **Ressourcen**, und klicken Sie auf **hinzufügen:**

   ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "Erstellen des Anbieters")

15. Wählen Sie dann in der Datei **Resources. resx** die Option **Ressource hinzufügen... aus. Fügen Sie eine vorhandene Datei hinzu**.  Navigieren Sie zu der Textdatei (die das HTML-Fragment enthält), die Sie zuvor gespeichert haben.

   Stellen Sie sicher, dass Ihr getformhtml-Code den Namen der neuen Ressource ordnungsgemäß durch das namens Präfix der Ressourcen Datei (RESX-Datei), gefolgt vom Namen der Ressource selbst auflöst:

       öffentliche Zeichenfolge getformhtml (int LCID) {String HTMLTemplate = Resources. mfaformhtml;//Resxfilename.resourceName Return HTMLTemplate;    }

   Sie sollten jetzt in der Lage sein, zu erstellen.

## <a name="build-the-adapter"></a>Erstellen des Adapters

Der Adapter sollte in eine stark benannte .NET-Assembly integriert werden, die im GAC in Windows installiert werden kann.  Um dies in einem Visual Studio-Projekt zu erreichen, führen Sie die folgenden Schritte aus:

1.  Klicken Sie mit der rechten Maustaste Projektmappen-Explorer auf den Projektnamen, und klicken Sie auf **Eigenschaften**

2.  Aktivieren Sie auf der Registerkarte **Signierung** **die Option Assembly signieren** , und wählen Sie **\<neu... wählen\>** **Sie Unterschlüssel Datei mit starkem Namen auswählen:**  Geben Sie einen Schlüssel Dateinamen und ein Kennwort ein, **und klicken Sie**  Vergewissern Sie sich dann, dass **das Signieren der Assembly** aktiviert ist und **nur Verzögertes Signieren**  Die Seite "Eigenschaften **Signierung** " sollte wie folgt aussehen:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "Erstellen des Anbieters")

3.  Erstellen Sie dann die Projekt Mappe.

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>Bereitstellen des Adapters auf dem AD FS Testcomputer

Bevor ein externer Anbieter von AD FS aufgerufen werden kann, muss er im System registriert werden.  Adapter Anbieter müssen ein Installationsprogramm bereitstellen, das die erforderlichen Installations Aktionen einschließlich der Installation im GAC ausführt, und das Installationsprogramm muss die Registrierung in AD FS unterstützen.  Wenn dies nicht der Fall ist, muss der Administrator die folgenden Windows PowerShell-Schritte ausführen.  Diese Schritte können im Lab zum Aktivieren von Tests und Debuggen verwendet werden.

### <a name="prepare-the-test-ad-fs-machine"></a>Bereiten Sie den Test AD FS Computer vor.

Kopieren Sie Dateien, und fügen Sie Sie GAC hinzu.

1.  Stellen Sie sicher, dass Sie einen Computer mit Windows Server 2012 R2 oder einen virtuellen Computer haben.

2.  Installieren Sie den AD FS-Rollen Dienst, und konfigurieren Sie eine Farm mit mindestens einem Knoten.

    Ausführliche Schritte zum Einrichten eines Verbund Servers in einer Lab-Umgebung finden Sie im [Windows Server 2012 R2-AD FS Bereitstellungs Handbuch](https://msdn.microsoft.com/library/dn486820\(v=msdn.10\)).

3.  Kopieren Sie die Tools "Gacutil. exe" auf den Server.

    Gacutil. exe befindet sich in **% HOMEDRIVE% \\program Files (x86) \\microsoft sdgs @ no__t-3Windows @ no__t-4V 8.0 a @ no__t-5bin @ no__t-6netfx 4,0 Tools @ no__t-7** auf einem Computer mit Windows 8.  Sie benötigen die Datei " **Gacutil. exe** " und die Datei " **1033**", " **en-US**" und den anderen lokalisierten Ressourcen Ordner unter dem Speicherort der **Netfx 4,0-Tools** .

4.  Kopieren Sie die Anbieter Dateien (eine oder mehrere signierte dll-Dateien mit starkem Namen) in den gleichen Ordner Speicherort wie " **Gacutil. exe** " (der Speicherort ist nur aus Gründen der Benutzer Nähe).

5.  Fügen Sie die DLL-Datei (en) auf jedem AD FS Verbund Server in der Farm dem GAC hinzu:

    Beispiel: Verwenden des Befehlszeilen Tools "Gacutil. exe" zum Hinzufügen einer DLL zum GAC:`C:\>.\gacutil.exe /if .\<yourdllname>.dll`

    So zeigen Sie den resultierenden Eintrag im GAC an`C:\>.\gacutil.exe /l <yourassemblyname>`

6.  

### <a name="register-your-provider-in-ad-fs"></a>Registrieren Sie Ihren Anbieter in AD FS

Nachdem Sie die oben genannten Voraussetzungen erfüllt haben, öffnen Sie auf dem Verbund Server ein Windows PowerShell-Befehlsfenster, und geben Sie die folgenden Befehle ein (Beachten Sie, dass Sie die folgenden Befehle ausführen müssen, wenn Sie eine Verbund Serverfarm verwenden, die die interne Windows-Datenbank verwendet.) primärer Verbund Server der Farm):

1.  `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    Dabei ist yourtykame der Name Ihres starken .net-Typs: "Yourdefaultnamespace. youriauthenticationadapterimplemenationclassname, yourassemblyname, Version = yourassemblyversion, Culture = neutral, PublicKeyToken = yourpublickeytokenvalue, ProcessorArchitecture = msil"

    Dadurch wird der externe Anbieter in AD FS registriert, wobei der von Ihnen als anynameyouwish angegebene Name angegeben wird.

2.  Starten Sie den AD FS-Dienst neu (z. b. über das Snap-in "Windows-Dienste").

3.  Führen Sie den folgenden Befehl `Get-AdfsAuthenticationProvider`aus:.

    Dadurch wird der Anbieter als einer der Anbieter im System angezeigt.

    Beispiel:

        PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
        PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
        PS C:\>net stop adfssrv
        PS C:\>net start adfssrv

    Wenn Sie den Geräte Registrierungsdienst in Ihrer AD FS Umgebung aktiviert haben, führen Sie auch Folgendes aus:`PS C:\>net start drs`

    Verwenden Sie den folgenden Befehl, um den registrierten Anbieter zu`PS C:\>Get-AdfsAuthenticationProvider`überprüfen:.

    Dadurch wird der Anbieter als einer der Anbieter im System angezeigt.

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>Erstellen Sie die AD FS Authentifizierungs Richtlinie, die Ihren Adapter aufruft.

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Erstellen der Authentifizierungs Richtlinie mit dem Snap-in "AD FS-Verwaltung"

1.  Öffnen Sie das Snap-in "AD FS-Verwaltung" (über das Menü "Server-Manager **Tools** ").

2.  Klicken Sie auf **Authentifizierungs Richtlinien**.

3.  Klicken Sie im mittleren Bereich unter **Multi-Factor Authentication**auf den Link **Bearbeiten** rechts neben **globale Einstellungen**.

4.  Aktivieren Sie im unteren Bereich der Seite **zusätzliche Authentifizierungsmethoden auswählen** das Kontrollkästchen für den Adminname Ihres Anbieters. Klicken Sie auf **Übernehmen**.

5.  Um einen "auslösen" zum Aufrufen von MFA mit Ihrem Adapter bereitzustellen, überprüfen Sie unter Speicher **Orte** sowohl das **Extranet** als auch das **Intranet**. Klicken Sie auf **OK**. (Informationen zum Konfigurieren von Triggern pro Vertrauender Seite finden Sie unten unter "Erstellen der Authentifizierungs Richtlinie mithilfe von Windows PowerShell").

6.  Überprüfen Sie die Ergebnisse mit den folgenden Befehlen:

    Erste Verwendung `Get-AdfsGlobalAuthenticationPolicy`. Der Anbieter Name sollte als einer der additionalauthenticationprovider-Werte angezeigt werden.

    Verwenden `Get-AdfsAdditionalAuthenticationRule`Sie dann. Die Regeln für das Extranet und das Intranet sollten als Ergebnis Ihrer Richtlinien Auswahl in der Administrator Benutzeroberfläche konfiguriert werden.

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Erstellen der Authentifizierungs Richtlinie mithilfe von Windows PowerShell

1.  Aktivieren Sie zunächst den Anbieter in der globalen Richtlinie:

    `PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`


~~~
> [!NOTE]
> Note that the value provided for the AdditionalAuthenticationProvider parameter corresponds to the value you provided for the “Name” parameter in the Register-AdfsAuthenticationProvider cmdlet above and to the “Name” property from Get-AdfsAuthenticationProvider cmdlet output. 
> <P></P>


Example:`PS C:\>Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
~~~

2. Konfigurieren Sie als nächstes globale oder Regeln der vertrauenden Seite, um MFA zu aktivieren:

   Beispiel 1: zum Erstellen einer globalen Regel, um MFA für externe Anforderungen anzufordern:`PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'`

   Beispiel 2: Erstellen von MFA-Regeln, um eine MFA für externe Anforderungen an eine bestimmte vertrauende Seite zu erfordern.  (Beachten Sie, dass einzelne Anbieter in AD FS in Windows Server 2012 R2) nicht mit einzelnen vertrauenden Seiten verbunden werden können.

       PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
       PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'

### <a name="authenticate-with-mfa-using-your-adapter"></a>Authentifizieren mit MFA mithilfe Ihres Adapters

Führen Sie abschließend die folgenden Schritte aus, um den Adapter zu testen:

1.  Stellen Sie sicher, dass der AD FS globalen primären Authentifizierungstyp sowohl für das Extranet als auch für das Intranet als Formular Authentifizierung konfiguriert ist (Dadurch wird das Authentifizieren der Demo als bestimmter Benutzer vereinfacht).

    1.  Klicken Sie im AD FS-Snap-in unter **Authentifizierungs Richtlinien**im Bereich **primäre Authentifizierung** neben **globale Einstellungen**auf **Bearbeiten** .

        1.  Oder klicken Sie einfach auf der Benutzeroberfläche der **Multi-Factor Policy** auf die Registerkarte **primär** .

2.  Stellen Sie sicher, dass die **Formular Authentifizierung** die einzige Option ist, die sowohl für die Extranet-als auch die Intranet-Authentifizierungsmethode  Klicken Sie auf **OK**.

3.  Öffnen Sie die IDP-initiierte Anmelde-HTML-Seite\<(https://\>FSName/adfs/ls/idpinitiatedsignon.htm), und melden Sie sich als gültiger AD-Benutzer in Ihrer Testumgebung an.

4.  Geben Sie Anmelde Informationen für die primäre Authentifizierung ein.

5.  Die Seite mit den MFA-Formularen sollte angezeigt werden. 

    Wenn Sie mehr als einen Adapter konfiguriert haben, wird die MFA-Auswahl Seite mit dem anzeigen Amen von oben angezeigt.

    ![Authentifizieren mit Adapter](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "Authentifizieren mit Adapter")

    ![Authentifizieren mit Adapter](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "Authentifizieren mit Adapter")

Sie verfügen nun über eine funktionierende Implementierung der-Schnittstelle, und Sie wissen, wie das Modell funktioniert. Sie können auch ein zusätzliches Beispiel für das Festlegen von Breakpoints in der beginauthentication und tryendauthentication.  Beachten Sie, dass beginauthentication ausgeführt wird, wenn der Benutzer zum ersten Mal das MFA-Formular eingibt, während tryendauthentication bei jeder Übermittlung des Formulars ausgelöst wird.

## <a name="update-the-adapter-for-successful-authentication"></a>Aktualisieren des Adapters für die erfolgreiche Authentifizierung

Aber warten Sie – Ihr Beispieladapter wird nie erfolgreich authentifiziert.\!  Dies liegt daran, dass Nothing in Ihrem Code für tryendauthentication NULL zurückgibt.

Nachdem Sie die oben beschriebenen Verfahren abgeschlossen haben, haben Sie eine grundlegende Adapter Implementierung erstellt und einem AD FS Server hinzugefügt.  Sie können die MFA-Formularseite erhalten, aber Sie können sich noch nicht authentifizieren, da Sie noch nicht die richtige Logik in die tryendauthentication-Implementierung eingefügt haben.  Fügen wir das nun hinzu.

Erinnern Sie sich an Ihre tryendauthentication-Implementierung:

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     //return new instance of IAdapterPresentationForm derived class
     outgoingClaims = new Claim[0];
     return new MyPresentationForm();

     }

Wir aktualisieren es, damit es nicht immer mypresentationform () zurückgibt.  Hierfür können Sie eine einfache hilfsprogrammmethode in ihrer Klasse erstellen:

    static bool ValidateProofData(IProofData proofData, IAuthenticationContext authContext)
     {
     if (proofData == null || proofData.Properties == null || !proofData.Properties.ContainsKey("ChallengeQuestionAnswer"))
     {
     throw new ExternalAuthenticationException("Error - no answer found", authContext);
     }

     if ((string)proofData.Properties["ChallengeQuestionAnswer"] == "adfabric")
     {
     return true;
     }
     else
     {
     return false;
     }
     }

Aktualisieren Sie dann tryendauthentication wie folgt:

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     outgoingClaims = new Claim[0];
     if (ValidateProofData(proofData, authContext))
     {
     //authn complete - return authn method
     outgoingClaims = new[] 
     {
     // Return the required authentication method claim, indicating the particulate authentication method used.
     new Claim( "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", 
     "http://example.com/myauthenticationmethod1" )
     };
     return null;
     }
     else
     {
     //authentication not complete - return new instance of IAdapterPresentationForm derived class
     return new MyPresentationForm();
     }
     }

Nun müssen Sie den Adapter im Testfeld aktualisieren.  Sie müssen zunächst die AD FS Richtlinie rückgängig machen, die Registrierung bei AD FS aufheben und AD FS neu starten, dann die DLL-Datei aus dem GAC entfernen, dann die neue dll-Datei dem GAC hinzufügen, Sie dann in AD FS registrieren, AD FS neu starten und AD FS Richtlinie neu konfigurieren.

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>Bereitstellen und Konfigurieren des aktualisierten Adapters auf dem Test AD FS Computer

### <a name="clear-ad-fs-policy"></a>AD FS Richtlinie löschen

Deaktivieren Sie alle auf MFA bezogenen Kontrollkästchen in der MFA-Benutzeroberfläche, und klicken Sie dann auf OK.

![Richtlinie löschen](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "Richtlinie löschen")

### <a name="unregister-provider-windows-powershell"></a>Aufheben der Registrierung des Anbieters (Windows PowerShell)

`PS C:\> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

Beispiel`PS C:\> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

Beachten Sie, dass der Wert, den Sie für "Name" übergeben, der gleiche Wert wie "Name" ist, den Sie dem Cmdlet "Register-adfsauthenticationprovider" bereitgestellt haben.  Dabei handelt es sich auch um die "Name"-Eigenschaft, die von Get-adfsauthenticationprovider ausgegeben wird.

Beachten Sie, dass Sie vor der Aufhebung der Registrierung eines Anbieters den Anbieter aus adfsglobalauthenticationpolicy entfernen müssen (entweder durch Deaktivieren der Kontrollkästchen, die Sie in AD FS-Verwaltungs-Snap-in oder mithilfe von Windows PowerShell aktiviert haben.)

Beachten Sie, dass der AD FS-Dienst nach diesem Vorgang neu gestartet werden muss.

### <a name="remove-assembly-from-gac"></a>Assembly aus GAC entfernen

1.  Verwenden Sie zuerst den folgenden Befehl, um den voll qualifizierten starken Namen des Eintrags zu ermitteln:`C:\>.\gacutil.exe /l <yourAdapterAssemblyName>`

    Beispiel`C:\>.\gacutil.exe /l mfaadapter`

2.  Verwenden Sie dann den folgenden Befehl, um ihn aus dem GAC zu entfernen:`.\gacutil /u “<output from the above command>”`

    Beispiel`C:\>.\gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>Die aktualisierte Assembly dem GAC hinzufügen

Stellen Sie sicher, dass Sie die aktualisierte dll zuerst lokal einfügen. `C:\>.\gacutil.exe /if .\MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>Anzeigen der Assembly im GAC (cmd-Zeile)

`C:\> .\gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>Registrieren Sie Ihren Anbieter in AD FS

1.  `PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2.  `PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3.  Starten Sie den AD FS-Dienst neu.

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Erstellen der Authentifizierungs Richtlinie mit dem Snap-in "AD FS-Verwaltung"

1.  Öffnen Sie das Snap-in "AD FS-Verwaltung" (über das Menü "Server-Manager **Tools** ").

2.  Klicken Sie auf **Authentifizierungs Richtlinien**.

3.  Klicken Sie unter **Multi-Factor Authentication**auf den Link **Bearbeiten** rechts neben **globale Einstellungen**.

4.  Aktivieren Sie unter **zusätzliche Authentifizierungsmethoden auswählen**das Kontrollkästchen für den Adminname Ihres Anbieters. Klicken Sie auf **Übernehmen**.

5.  Um einen "auslösen" zum Aufrufen von MFA mit Ihrem Adapter bereitzustellen, überprüfen Sie unter Speicherorte sowohl das **Extranet** als auch das **Intranet**. Klicken Sie auf **OK**.

### <a name="authenticate-with-mfa-using-your-adapter"></a>Authentifizieren mit MFA mithilfe Ihres Adapters

Führen Sie abschließend die folgenden Schritte aus, um den Adapter zu testen:

1.  Stellen Sie sicher, dass der AD FS globalen primären Authentifizierungstyp sowohl für das Extranet als auch für das Intranet als **Formular Authentifizierung** konfiguriert ist (dadurch ist es einfacher, sich als bestimmter Benutzer zu authentifizieren).

    1.  Klicken Sie im AD FS-Verwaltungs-Snap-in unter **Authentifizierungs Richtlinien**im Bereich **primäre Authentifizierung** neben **globale Einstellungen**auf **Bearbeiten** .

        1.  Oder klicken Sie einfach auf der Benutzeroberfläche der Multi-Factor Policy auf die Registerkarte **primär** .

2.  Stellen Sie sicher, dass die **Formular Authentifizierung** die einzige Option ist, die sowohl für die **Extranet** -als auch die **Intranet** -Authentifizierungsmethode  Klicken Sie auf **OK**.

3.  Öffnen Sie die IDP-initiierte Anmelde-HTML-Seite\<(https://\>FSName/adfs/ls/idpinitiatedsignon.htm), und melden Sie sich als gültiger AD-Benutzer in Ihrer Testumgebung an.

4.  Geben Sie die Anmelde Informationen für die primäre Authentifizierung ein.

5.  Die Seite MFA Forms mit Beispiel Text für die Abfrage wird angezeigt.

    1.  Wenn Sie mehr als einen Adapter konfiguriert haben, wird die MFA-Auswahl Seite mit dem anzeigen Amen angezeigt.

Bei der Eingabe von "adfabric" auf der Seite "MFA-Authentifizierung" sollte eine erfolgreiche Anmeldung angezeigt werden.

![mit Adapter anmelden](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "mit Adapter anmelden")

![mit Adapter anmelden](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "mit Adapter anmelden")

## <a name="see-also"></a>Siehe auch

#### <a name="other-resources"></a>Weitere Ressourcen

[Zusätzliche Authentifizierungsmethoden](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\))  
[Verwalten von Risiken mit zusätzlicher mehrstufiger Authentifizierung für sensible Anwendungen](https://msdn.microsoft.com/library/dn280949\(v=msdn.10\))

