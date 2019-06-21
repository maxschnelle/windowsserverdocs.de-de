---
title: Erstellen Sie eine benutzerdefinierte Authentifizierungsmethode für AD FS unter WindowsServer
description: Dieses Szenario beschreibt, wie Sie eine benutzerdefinierte Authentifizierungsmethode für AD FS in Windows Server zu erstellen.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a638ec25be4fc99b4eccd1d9fa541e640ef9e15c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280652"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Erstellen Sie eine benutzerdefinierte Authentifizierungsmethode für AD FS unter WindowsServer

Diese exemplarische Vorgehensweise enthält Anweisungen zum Implementieren einer benutzerdefinierten Authentifizierungsmethode für AD FS in Windows Server 2012 R2. Weitere Informationen finden Sie unter [Additional Authentication Methods](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\)).


> [!WARNING]
> Das Beispiel, das Sie erstellen können ist&nbsp;zum besseren. &nbsp;Diese Anweisungen gelten für die einfachste und minimale Implementierung, die Möglichkeit, um die erforderlichen Elemente des Modells verfügbar zu machen.&nbsp; Es ist keine Authentifizierung-Back-End, Fehler beim Verarbeiten, oder Konfigurationsdaten. 
> <P></P>



## <a name="setting-up-the-development-box"></a>Das Feld für die Entwicklung einrichten

In dieser exemplarischen Vorgehensweise wird Visual Studio 2012 verwendet.  Das Projekt kann erstellt werden, mit jeder Entwicklungsumgebung, die eine Klasse von .NET für Windows erstellen kann. Das Projekt muss auf .NET 4.5 ausgerichtet, da die **BeginAuthentication** und **TryEndAuthentication** Methoden verwenden Sie den Typ **System.Security.Claims.Claim**, die Bestandteil von .NET Framework-Version 4.5.There ist ein Verweis für das Projekt erforderlich sind:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Verweis-dll</strong></p></td>
<td><p><strong>Wo Sie sich befindet</strong></p></td>
<td><p><strong>Erforderlich für</strong></p></td>
</tr>
<tr class="even">
<td><p>Microsoft.IdentityServer.Web.dll</p></td>
<td><p>Die Dll befindet sich im %windir%\ADFS auf einem Windows Server 2012 R2-Server, auf dem AD FS installiert wurde.</p>
<p></p>
<p>Diese Dll muss auf dem Entwicklungscomputer ausgeführt und einen expliziten Verweis im Projekt erstellt kopiert werden.</p></td>
<td><p>Schnittstellentypen einschließlich IAuthenticationContext, IProofData</p></td>
</tr>
</tbody>
</table>


## <a name="create-the-provider"></a>Erstellen des Anbieters

1.  In Visual Studio 2012: Wählen Sie Datei -\>New-\>Projekt...

2.  Wählen Sie die Klassenbibliothek, und achten Sie darauf, dass Sie .NET 4.5 ausgerichtet sind.

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "Erstellen des Anbieters")

3.  Erstellen Sie eine Kopie der **Microsoft.IdentityServer.Web.dll** % windir%\\AD FS auf dem Windows Server 2012 R2-Server, in dem AD FS installiert wurde, und fügen Sie ihn in Ihrem Projektordner auf dem Entwicklungscomputer.

4.  In **Projektmappen-Explorer**, klicken Sie mit der rechten Maustaste auf **Verweise** und **Verweis hinzufügen...**

5.  Navigieren Sie zu Ihrer lokalen Kopie des **Microsoft.IdentityServer.Web.dll** und **hinzufügen...**

6.  Klicken Sie auf **OK** , den neuen Verweis zu bestätigen:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "Erstellen des Anbieters")

    Sie sollten jetzt eingerichtet werden, beheben alle Typen, die für den Anbieter erforderlich. 

7.  Fügen Sie eine neue Klasse zu Ihrem Projekt (klicken Sie mit der rechten Maustaste auf Ihr Projekt **hinzufügen... Klasse...** ), und geben sie einen Namen wie **MyAdapter**, wie unten gezeigt:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "Erstellen des Anbieters")

8.  Ersetzen Sie in der neuen Datei MyAdapter.cs den vorhandenen Code durch Folgendes:

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

    Nachdem Sie F12 können (Rechtsklick: Gehe zu Definition) auf IAuthenticationAdapter, um die erforderliche Schnittstellenmember anzuzeigen. 

    Als Nächstes können Sie eine einfache Implementierung dieser durchführen.

9.  Ersetzen Sie den gesamten Inhalt der Klasse, durch Folgendes:

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

10. Wir sind nicht bereit für die noch erstellen... Es gibt zwei weitere Schnittstellen zu.

    Fügen Sie zwei weitere Klassen zu Ihrem Projekt: einer ist für die Metadaten und die andere für das Formular für die Präsentation.  Sie können diese in derselben Datei wie die oben gezeigte Klasse hinzufügen.

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. Als Nächstes können Sie die erforderlichen Member für die einzelnen hinzufügen. Erstens werden die Metadaten (mit Kommentaren der hilfreich Inline)

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

    Als Nächstes das Presentation-Formular:

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

12. Beachten Sie den "Todo" für die **Resources.FormPageHtml** Element oben. 

   Sie können dies beheben, in einer Minute, aber zunächst sehen wir die letzten erforderlichen return-Anweisungen, basierend auf die neu implementierten Typen, auf die erste MyAdapter-Klasse hinzufügen.  Zu diesem Zweck fügen Sie die Elemente in *Kursiv* unter Ihrer vorhandenen IAuthenticationAdapter-Implementierung:

       MyAdapter-Klasse: IAuthenticationAdapter     {     public IAuthenticationAdapterMetadata Metadata     {     //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }     get { return new MyMetadata(); }     }

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

13. Für die Ressourcendatei, enthält jetzt das HTML-Fragment. Erstellen Sie eine neue Textdatei in Ihrem Projektordner mit dem folgenden Inhalt:

       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">Dieser Inhalt wird vom beispieladapter MFA bereitgestellt. Herausforderung Eingaben sollte unten angezeigt werden.</p>
        <label for="challengeQuestionInput" class="block">Fragetext</label>
        <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
        <div id="submissionArea" class="submitMargin">
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

14. Wählen Sie dann **Projekt -\>Komponente hinzufügen... Ressourcen** Datei, und nennen Sie die Datei **Ressourcen**, und klicken Sie auf **hinzufügen:**

   ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "Erstellen des Anbieters")

15. Klicken Sie dann in der **"Resources.resx"** Datei, wählen Sie **Ressource hinzufügen... Vorhandene Datei hinzufügen**.  Navigieren Sie zu der Textdatei (mit der html-Fragment), die Sie über gespeichert.

   Stellen Sie sicher, dass Ihr Code GetFormHtml-der Name der neuen Ressource ordnungsgemäß durch das Namenspräfix der Ressourcen-Datei (.resx) gefolgt vom Namen der Ressource selbst aufgelöst wird:

       public string GetFormHtml(int lcid)    {     string htmlTemplate = Resources.MfaFormHtml; //Resxfilename.resourcename     return htmlTemplate;    }

   Sie sollten jetzt erstellen können.

## <a name="build-the-adapter"></a>Entwickeln Sie den adapter

Der Adapter sollte in einer Assembly mit starkem Namen .NET erstellt werden, die im globalen Assemblycache in Windows installiert werden kann.  Führen Sie hierzu in Visual Studio-Projekt die folgenden Schritte aus:

1.  Klicken Sie mit der rechten Maustaste auf den Projektnamen im Projektmappen-Explorer, und klicken Sie auf **Eigenschaften**.

2.  Auf der **Signierung** Registerkarte **Assembly signieren** , und wählen Sie **\<neu... \>** unter **Schlüsseldatei mit starkem Namen auswählen:**  Geben Sie einen Schlüsseldateinamen und ein Kennwort ein, und klicken Sie auf **OK**.  Stellen Sie sicher **Assembly signieren** aktiviert ist und **nur verzögerte Signierung** deaktiviert ist.  Die Eigenschaften **Signierung** Seite sollte wie folgt aussehen:

    ![Erstellen des Anbieters](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "Erstellen des Anbieters")

3.  Erstellen Sie die Projektmappe.

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>Bereitstellen Sie den Adapter auf der AD FS-Test-Computer

Bevor Sie ein externer Anbieter von AD FS aufgerufen werden kann, muss es im System registriert werden.  Adapter-Anbieter müssen ein Installationsprogramm die erforderlichen Installationsaktionen einschließlich der Installation im GAC ausführt, sowie vom Installer muss Registrierung in AD FS unterstützt.  Wenn dies nicht erfolgt ist, muss der Administrator die folgenden Windows PowerShell-Schritte ausführen.  Diese Schritte können im Lab verwendet werden, um zu testen und Debuggen zu aktivieren.

### <a name="prepare-the-test-ad-fs-machine"></a>Vorbereiten der AD FS-Test-VM

Kopieren von Dateien und fügen Sie im GAC.

1.  Stellen Sie sicher, dass Sie einen Windows Server 2012 R2-Computer oder virtuellen Computer verfügen.

2.  Installieren Sie des AD FS-Rollendiensts und konfigurieren Sie eine Farm mit mindestens einem Knoten.

    Ausführliche Schritte zum Einrichten eines Verbundservers in einer Lab-Umgebung finden Sie unter den [Windows Server 2012 R2 AD FS-Bereitstellungshandbuch](https://msdn.microsoft.com/library/dn486820\(v=msdn.10\)).

3.  Kopieren Sie die Gacutil.exe-Tools, mit dem Server.

    Gacutil.exe finden Sie im **%HOMEDRIVE%\\Programmdateien (x86)\\Microsoft SDKs\\Windows\\v8.0A\\Bin\\NETFX 4.0 Tools\\** auf einem Windows 8-Computer.  Müssen Sie die **gacutil.exe** Datei selbst als auch die **1033**, **En-US**, und die andere lokalisierte Ressourcen-Ordner aus der **NETFX4.0-Tools** Speicherort.

4.  Kopieren Sie Ihre Anbieter-Dateien (ein oder mehrere starken Namen signiert DLL-Dateien) in den gleichen Ordner wie **gacutil.exe** (der Speicherort ist nur zur Vereinfachung)

5.  Fügen Sie Ihre DLL-Dateien im globalen Assemblycache auf jedem AD FS-Verbundserver in der Farm hinzu:

    Beispiel: Verwenden von Befehlszeilentools GACutil.exe eine Dll im globalen Assemblycache hinzufügen: `C:\>.\gacutil.exe /if .\<yourdllname>.dll`

    So zeigen Sie die resultierende Eintrag im globalen Assemblycache an:`C:\>.\gacutil.exe /l <yourassemblyname>`

6.  

### <a name="register-your-provider-in-ad-fs"></a>Registrieren Sie Ihren Anbieter in AD FS

Wenn die oben genannten Voraussetzungen erfüllt sind, öffnen Sie auf Ihrem Verbundserver ein Windows PowerShell-Befehlsfenster, und geben Sie die folgenden Befehle aus (Beachten Sie, dass wenn Sie Verbundserverfarm, die Windows Internal Database verwendet verwenden, müssen Sie diese Befehle für Ausführen der Primärer Verbundserver der Farm):

1.  `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    YourTypeName ist, in denen Ihre .NET Typ mit starkem Namen: "YourDefaultNamespace.YourIAuthenticationAdapterImplementationClassName, YourAssemblyName, Version = YourAssemblyVersion, Culture = Neutral, PublicKeyToken = YourPublicKeyTokenValue, ProcessorArchitecture = MSIL"

    Dadurch wird Ihren externen Anbieter in AD FS mit dem Namen registriert, die Sie als AnyNameYouWish oben bereitgestellt.

2.  Starten Sie den AD FS-Dienst (z. B. die Windows-Dienste-Snap-in mit) neu.

3.  Führen Sie den folgenden Befehl: `Get-AdfsAuthenticationProvider`.

    Zeigt den Anbieter als einen der Anbieter im System.

    Beispiel:

        PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
        PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
        PS C:\>net stop adfssrv
        PS C:\>net start adfssrv

    Wenn Sie den geräteregistrierungsdienst in Ihrer AD FS-Umgebung aktiviert haben, führen Sie außerdem Folgendes:  `PS C:\>net start drs`

    Um die registrierten Anbieter überprüfen möchten, verwenden Sie den folgenden Befehl:`PS C:\>Get-AdfsAuthenticationProvider`.

    Zeigt den Anbieter als einen der Anbieter im System.

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>Erstellen Sie die AD FS-Authentifizierungsrichtlinie, die den Adapter aufruft.

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Erstellen der Authentifizierungsrichtlinie, die mit der AD FS-Verwaltungs-Snap-in

1.  Öffnen Sie das AD FS-Verwaltungs-Snap-in (im Server-Manager **Tools** Menü).

2.  Klicken Sie auf **Authentifizierungsrichtlinien**.

3.  Klicken Sie im mittleren Bereich unter **Multi-Factor Authentication**, klicken Sie auf die **bearbeiten** Verknüpfung mit der rechten Seite des **globale Einstellungen**.

4.  Klicken Sie unter **wählen Sie zusätzliche Authentifizierungsmethoden** am unteren Rand der Seite, aktivieren Sie das Kontrollkästchen für Ihres Anbieters AdminName. Klicken Sie auf **Übernehmen**.

5.  Eine "Trigger" zum Aufrufen von MFA unter Verwendung von des Adapters zu **Speicherorte** aktivieren Sie beide **Extranet** und **Intranet**, z. B. Klicken Sie auf **OK**. (So konfigurieren Sie Trigger pro vertrauender Seite Partei, finden Sie unten unter "Erstellen die Authentifizierungsrichtlinie, die mithilfe von Windows PowerShell".)

6.  Überprüfen Sie die Ergebnisse mithilfe der folgenden Befehle ein:

    Verwenden Sie zunächst `Get-AdfsGlobalAuthenticationPolicy`. Ihr Anbieter Name sollte als einer der Werte AdditionalAuthenticationProvider angezeigt werden.

    Verwenden Sie dann `Get-AdfsAdditionalAuthenticationRule`. Die Regeln sollte für das Extranet und Intranet konfiguriert, durch die Richtlinienauswahl in der Benutzeroberfläche für Administratoren angezeigt werden.

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Erstellen der Authentifizierungsrichtlinie, die mithilfe von Windows PowerShell

1.  Aktivieren Sie zunächst den Anbieter in der globalen Richtlinie:

    `PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`


~~~
> [!NOTE]
> Note that the value provided for the AdditionalAuthenticationProvider parameter corresponds to the value you provided for the “Name” parameter in the Register-AdfsAuthenticationProvider cmdlet above and to the “Name” property from Get-AdfsAuthenticationProvider cmdlet output. 
> <P></P>


Example:`PS C:\>Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
~~~

2. Als Nächstes konfigurieren Sie globale oder der vertrauenden Seite für Partei die spezifischen Regeln an MFA-Trigger:

   Beispiel 1: Erstellen Sie globale Regel, um MFA anzufordern, für externe Anforderungen:`PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'`

   Beispiel 2: Klicken Sie zum Erstellen von MFA Partei Regeln, um MFA für externe Anforderungen an eine bestimmte der vertrauenden Seite erforderlich ist.  (Beachten Sie, dass die einzelnen Anbieter die einzelne vertrauende Seite in AD FS unter Windows Server 2012 R2 verbunden werden können.)

       PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
       PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'

### <a name="authenticate-with-mfa-using-your-adapter"></a>Authentifizierung mit MFA mit Ihren adapter

Abschließend führen Sie die Schritte unten aus, um den Adapter zu testen:

1.  Stellen Sie sicher, der Typ der AD FS-globale primäre Authentifizierung als die Formularauthentifizierung konfiguriert ist, für Extranet und Intranet (Dies erleichtert die Demo als ein bestimmter Benutzer zu authentifizieren.)

    1.  In der AD FS-Snap-in unter **Authentifizierungsrichtlinien**in die **primäre Authentifizierung** Bereich, klicken Sie auf **bearbeiten** neben **globale Einstellungen**.

        1.  Oder klicken Sie einfach auf die **primären** Registerkarte die **Mehrstufen-Richtlinie** Benutzeroberfläche.

2.  Stellen Sie sicher **Formularauthentifizierung** ist die einzige Option für das Extranet und Intranet-Authentifizierungsmethode aktiviert.  Klicken Sie auf **OK**.

3.  Öffnen der IDP-initiierten anmelden html-Seite (https://\<Fsname\>/adfs/ls/idpinitiatedsignon.htm), und melden Sie sich als ein gültiger AD-Benutzer in Ihrer testumgebung.

4.  Geben Sie Anmeldeinformationen zur primären Authentifizierung ein.

5.  Sie sollten sehen, dass die MFA-Formulare, die Seite mit Beispiel Herausforderung Fragen angezeigt. 

    Wenn Sie mehrere Adapter konfiguriert haben, sehen Sie die MFA-Auswahl-Seite mit Ihrem Anzeigenamen von oben.

    ![mit Adapter authentifizieren](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "mit Adapter authentifizieren")

    ![mit Adapter authentifizieren](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "mit Adapter authentifizieren")

Sie verfügen nun über eine funktionsfähige Implementierung der Schnittstelle, und Sie verfügen über die Kenntnisse der Funktionsweise des Modells. Sie können Trym als zusätzliches Beispiel zum Festlegen von Breakpoints in den BeginAuthentication als auch die TryEndAuthentication.  Beachten Sie, wie BeginAuthentication ausgeführt wird, wenn der Benutzer zuerst im Formular MFA eingibt während TryEndAuthentication an jeden Senden des Formulars ausgelöst wird.

## <a name="update-the-adapter-for-successful-authentication"></a>Aktualisieren Sie den Adapter für eine erfolgreiche Authentifizierung

Aber warten – der Beispiel-Adapter wird nie erfolgreich authentifiziert.\!  Dies ist, da es sich bei "nothing" in Ihrem Code für TryEndAuthentication gibt null zurück.

Indem Sie die oben beschriebenen Schritte abschließen, müssen Sie eine grundlegende adapterimplementierung erstellt und AD FS-Server hinzugefügt.  Erhalten Sie die MFA-Forms-Seite, aber Sie können nicht noch authentifiziert werden, da Sie noch nicht die richtige Logik in Ihrer Implementierung der TryEndAuthentication gespeichert haben.  Lassen Sie uns hinzufügen, die aus.

Beachten Sie die TryEndAuthentication-Implementierung:

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     //return new instance of IAdapterPresentationForm derived class
     outgoingClaims = new Claim[0];
     return new MyPresentationForm();

     }

Wir aktualisieren sie daher immer MyPresentationForm() zurückgegeben wird nicht.  Hierfür können Sie eine einfache Hilfsmethode in Ihrer Klasse erstellen:

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

Aktualisieren Sie dann TryEndAuthentication wie unten gezeigt ein:

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

Jetzt müssen Sie den Adapter auf das Testfeld zu aktualisieren.  Sie müssen zunächst rückgängig machen die AD FS-Richtlinie, klicken Sie dann die Registrierung von AD FS und Neustart der AD FS und dann entfernen die DLL-Datei aus dem GAC, und klicken Sie dann die neue DLL-Datei im globalen Assemblycache hinzufügen und dann in AD FS registrieren, Neustarten AD FS und rekonfigurieren Sie die AD FS-Richtlinie.

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>Bereitstellen Sie und konfigurieren Sie die aktualisierten Adapters auf den Test AD FS-Computer

### <a name="clear-ad-fs-policy"></a>Deaktivieren Sie für AD FS

Löschen aller MFA bezogenen Kontrollkästchen in den MFA-UI, wie unten beschrieben, anschließend auf OK.

![Richtlinie löschen](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "Richtlinie löschen")

### <a name="unregister-provider-windows-powershell"></a>Aufheben der Registrierung Anbieters (Windows PowerShell)

`PS C:\> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

Beispiel:`PS C:\> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

Beachten Sie, dass der Wert, den für "Name" den gleichen Wert wie "Name" ist, übergeben Sie Sie an das Cmdlet "Register-AdfsAuthenticationProvider" angegeben.  Es ist auch die Eigenschaft "Name", die von Get-AdfsAuthenticationProvider ausgegeben wird.

Beachten Sie, dass vor der Registrierung ein Anbieters aufgehoben wurde, Sie entfernen müssen den Anbieter aus der AdfsGlobalAuthenticationPolicy (entweder durch das entsprechende Kontrollkästchen, die Sie im AD FS-Snap-in aktiviert. deaktivieren oder mithilfe von Windows PowerShell.)

Beachten Sie, dass der AD FS-Dienst nach diesem Vorgang neu gestartet werden muss.

### <a name="remove-assembly-from-gac"></a>Entfernen Sie die Assembly aus dem GAC

1.  Verwenden Sie zunächst den folgenden Befehl aus, um den vollqualifizierten starken Namen des Eintrags zu suchen:`C:\>.\gacutil.exe /l <yourAdapterAssemblyName>`

    Beispiel:`C:\>.\gacutil.exe /l mfaadapter`

2.  Klicken Sie dann verwenden Sie den folgenden Befehl aus, um es aus dem GAC entfernen:`.\gacutil /u “<output from the above command>”`

    Beispiel:`C:\>.\gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>Fügen Sie die aktualisierte Assembly im GAC

Stellen Sie sicher, dass Sie zuerst die aktualisierten DLL-Datei lokal einfügen. `C:\>.\gacutil.exe /if .\MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>Ansichtsassembly im GAC (Befehlszeile)

`C:\> .\gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>Registrieren Sie Ihren Anbieter in AD FS

1.  `PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2.  `PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3.  Starten Sie den AD FS-Dienst neu.

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>Erstellen der Authentifizierungsrichtlinie, die mit der AD FS-Verwaltungs-Snap-in

1.  Öffnen Sie das AD FS-Verwaltungs-Snap-in (im Server-Manager **Tools** Menü).

2.  Klicken Sie auf **Authentifizierungsrichtlinien**.

3.  Klicken Sie unter **Multi-Factor Authentication**, klicken Sie auf die **bearbeiten** Verknüpfung mit der rechten Seite des **globale Einstellungen**.

4.  Klicken Sie unter **wählen Sie zusätzliche Authentifizierungsmethoden**, aktivieren Sie das Kontrollkästchen für Ihres Anbieters AdminName. Klicken Sie auf **Übernehmen**.

5.  Um eine "Trigger" zum Aufrufen von MFA mit Ihren Adapter bereitzustellen, unter Speicherorte aktivieren Sie beide **Extranet** und **Intranet**, z. B. Klicken Sie auf **OK**.

### <a name="authenticate-with-mfa-using-your-adapter"></a>Authentifizierung mit MFA mit Ihren adapter

Abschließend führen Sie die Schritte unten aus, um den Adapter zu testen:

1.  Stellen Sie sicher, der Typ der AD FS-globale primäre Authentifizierung als konfiguriert ist, **Formularauthentifizierung** für Extranet und Intranet (Dadurch wird es einfacher, als ein bestimmter Benutzer authentifiziert).

    1.  Im AD FS-Verwaltungs-Snap-in unter **Authentifizierungsrichtlinien**in die **primäre Authentifizierung** Bereich, klicken Sie auf **bearbeiten** neben **globale Einstellungen**.

        1.  Oder klicken Sie einfach auf die **primären** Registerkarte aus der Benutzeroberfläche des Multi-Factor-Richtlinie.

2.  Stellen Sie sicher **Formularauthentifizierung** ist die einzige Möglichkeit, die für beide überprüft die **Extranet** und **Intranet** Authentifizierungsmethode.  Klicken Sie auf **OK**.

3.  Öffnen der IDP-initiierten anmelden html-Seite (https://\<Fsname\>/adfs/ls/idpinitiatedsignon.htm), und melden Sie sich als ein gültiger AD-Benutzer in Ihrer testumgebung.

4.  Geben Sie die Anmeldeinformationen zur primären Authentifizierung ein.

5.  Daraufhin sollte die MFA-Formulare, die Seite mit einem Probetext Beispiel angezeigt.

    1.  Wenn Sie mehrere Adapter konfiguriert haben, sehen Sie die MFA-Auswahl-Seite mit Ihrem Anzeigenamen.

Eine erfolgreiche Anmeldung sollte bei der Eingabe von "Adfabric" auf der Seite des MFA-Authentifizierung.

![Melden Sie sich Adapter](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "Anmeldung mit Adapter")

![Melden Sie sich Adapter](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "Anmeldung mit Adapter")

## <a name="see-also"></a>Siehe auch

#### <a name="other-resources"></a>Weitere Ressourcen

[Zusätzliche Authentifizierungsmethoden](https://msdn.microsoft.com/library/dn758113\(v=msdn.10\))  
[Verwalten von Risiken mit zusätzlicher Mehrstufiger Authentifizierung für sensible Anwendungen](https://msdn.microsoft.com/library/dn280949\(v=msdn.10\))

