---
title: Erstellen Sie mit AD FS 2019 Risk Assessment-Modell-Plug-ins
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: ''
ms.date: 04/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 80f42695af917084ee63297df052adc069340bb3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190525"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>Erstellen Sie mit AD FS 2019 Risk Assessment-Modell-Plug-ins

Sie können jetzt Ihre eigenen-Plug-ins zum Sperren oder weisen eine risikobewertung authentifizierungsanforderungen in verschiedenen Phasen – die Anforderung empfangen, Authentifizierung und nach der Authentifizierung erstellen. Dies kann erreicht werden, mit dem neuen Risk Assessment-Modell mit AD FS-2019 eingeführt wurde. 

## <a name="what-is-the-risk-assessment-model"></a>Was ist das Risiko-Bewertung-Modell?

Das Risiko-Bewertung-Modell ist ein Satz von Schnittstellen und Klassen, die es Entwicklern ermöglichen das Lesen von Anforderungsheadern für die Authentifizierung, und ihre eigene Risk Assessment Logik implementieren. Der implementierte Code (plug-in) wird mit AD FS-Authentifizierungsprozess ausgeführt. Für z.B. verwenden die Schnittstellen und Klassen, die mit dem Modell enthalten, Sie können implementieren Sie Code zum entweder blockieren oder Authentifizierungsanforderung abhängig von der Client-IP-Adresse im Header Anforderung enthalten zulassen. AD FS wird führen Sie den Code für jede Authentifizierungsanforderung und entsprechende Aktionen gemäß der implementierte Logik. 

Das Modell kann an jedem der drei Phasen des AD FS-authentifizierungspipeline wie unten gezeigt Plug-in-code

![model](media\ad-fs-risk-assessment-model\risk1.png)

1.  **Anforderung empfangen-Phase** – ermöglicht das Erstellen von-Plug-ins zum Zulassen oder blockieren Anforderung aus, wenn AD FS die Authentifizierungsanforderung z. B. empfängt, bevor der Benutzer Anmeldeinformationen eingegeben hat. Der Anforderungskontext verwendet (z. B., Client-IP, Http-Methode, die DNS-Proxy-Server usw.) können in dieser Phase können die risikobewertung zur Verfügung. Für z. B., Sie erstellen ein plug-in zum Lesen der IP-Adresse aus dem Anforderungskontext und die Authentifizierungsanforderung blockiert werden, wenn die IP-Adresse in der vordefinierten Liste von riskanten IP-Adressen befindet. 

2.  **Vorauthentifizierungsphase** – ermöglicht das Erstellen von-Plug-ins zulassen oder Blockieren von Anforderung, die zum Zeitpunkt, wenn Benutzer die Anmeldeinformationen bereitstellt, aber bevor Sie AD FS ausgewertet. In dieser Phase haben zusätzlich zu den Anforderungskontext Sie auch Informationen zu den Sicherheitskontext (z.B. Benutzertoken, Benutzer-ID, usw.) und den Protokoll-Kontext (z.B. Authentifizierungsprotokoll, "ClientID", Resourceid, usw.) in Ihre Risk Assessment Logik verwenden. Für z. B., Sie Plug-Ins zu verhindern, dass Angriffe auf Kennwörter Sprühende lesen das Kennwort des Benutzers aus dem Benutzertoken und die Authentifizierungsanforderung blockiert erstellen können, wenn das Kennwort in der vordefinierten Liste mit riskanten Kennwörter. 

3.  **Nach der Authentifizierung** – ermöglicht das Erstellen von-Plug-in zum Bewerten von Risiken, nachdem Benutzer Anmeldeinformationen angegeben hat, und AD FS hat die Authentifizierung ausgeführt. In dieser Phase wird zusätzlich zu den Anforderungskontext, Sicherheitskontext und Protokoll-Kontext müssen Sie auch Informationen über das Authentifizierungsergebnis (Erfolg oder Fehler). Das plug-in können die risikobewertung anhand der verfügbaren Informationen auswerten und übergeben Sie die risikobewertung in Anspruch nehmen und die Regeln für die weitere Auswertung. 

Zum besseren Verständnis So erstellen eine risikobewertung-Plug-in, und führen es mit AD FS-Prozess aus, erstellen Sie ein Beispiel-Plug-in, das die von bestimmten eingehenden Anforderungen blockiert **extranet** IP-Adressen identifiziert als riskante, registrieren Sie das plug-in mit AD FS und schließlich die Funktionalität testen. 

>[!NOTE]
>In dieser exemplarischen Vorgehensweise ist nur für die Sie zeigen, wie Sie ein Beispiel-Plug-Ins erstellen können. Keineswegs ist die Lösung, die wir erstellen eine unternehmenslösung bereit.  

## <a name="building-a-sample-plug-in"></a>Die Erstellung eines Plug-In-Beispiels

### <a name="pre-requisites"></a>Voraussetzungen
Es folgt die Liste der Voraussetzungen zum Erstellen dieses Beispiels-Plug-in

- AD FS-2019 installiert und konfiguriert
- .NET Framework 4.7 und höher
- Visual Studio

### <a name="build-plug-in-dll"></a>Erstellen Sie die Plug-in-dll
Das folgende Verfahren führt Sie durch die Erstellung einer Beispiel-Plug-in-Dll.

 1. Laden Sie das Beispiel-Plug-in, verwenden Sie Git Bash, und geben Sie Folgendes ein: 

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

 2. Erstellen Sie eine **CSV** Datei an einem beliebigen Speicherort auf Ihrem AD FS-Server (In meinem Fall ich erstellt habe die **authconfigdb.csv** Datei **C:\extensions**) und fügen Sie die IP-Adressen, die Sie an dieser Datei blockieren möchten. 

   Das Beispiel-Plug-in wird bei allen authentifizierungsanforderungen von blockiert die **Extranet-IP-Adressen** in dieser Datei aufgelisteten. 

   >{! Hinweis] Wenn Sie eine AD FS-Farm verfügen, können Sie die Datei auf einem oder allen AD FS-Servern erstellen. Eine der Dateien kann verwendet werden, um die riskanten IP-Adressen in AD FS zu importieren. Besprechen wir den Importvorgang zu ausführlich die [registrieren Sie die Plug-in-Dll mit AD FS](#register-the-plug-in-dll-with-ad-fs) Abschnitt weiter unten. 

 3. Öffnen Sie das Projekt `ThreatDetectionModule.sln` mithilfe von Visual Studio

 4. Entfernen Sie die `Microsoft.IdentityServer.dll` aus dem Projektmappen-Explorer wie unten dargestellt:</br>
 ![model](media\ad-fs-risk-assessment-model\risk2.png)

 5. Fügen Sie Verweis auf die `Microsoft.IdentityServer.dll` von AD FS wie unten dargestellt

   a.   Klicken Sie mit der rechten Maustaste auf **Verweise** in **Projektmappen-Explorer** , und wählen Sie **Verweis hinzufügen...**</br> 
   ![model](media\ad-fs-risk-assessment-model\risk3.png)
   
   b.   Auf der **Verweis-Manager** wählen Sie im Fenster **Durchsuchen**. In der **zu referenzierende Dateien auswählen...** Dialogfeld "," select `Microsoft.IdentityServer.dll` aus Ihrer AD FS-Installationsordner (in meinem Fall **C:\Windows\ADFS**), und klicken Sie auf **hinzufügen**.
   
   >[!NOTE]
    >In meinem Fall habe ich das plug-in auf dem AD FS-Server selbst erstellen. Wenn die Entwicklungsumgebung auf einem anderen Server befindet, kopieren die `Microsoft.IdentityServer.dll` aus Ihrer AD FS-Installationsordner auf AD FS-Server, auf dem Entwicklungscomputer.</br> 
   
   ![model](media\ad-fs-risk-assessment-model\risk4.png)
   
   c.   Klicken Sie auf **OK** auf die **Verweis-Manager** Fenster nach dem sicherstellen `Microsoft.IdentityServer.dll` aktiviert ist</br>
   ![model](media\ad-fs-risk-assessment-model\risk5.png)
 
 6. Alle Klassen und Verweise sind jetzt direkt auf eine Erstellung durchzuführen.   Da die Ausgabe des Projekts eine Dll handelt, er muss jedoch in installiert werden muss die **Global Assembly Cache**, oder der GAC, der AD FS-Server und die Dll muss zunächst signiert werden. Dies kann wie folgt durchgeführt werden:

   a.   **Mit der rechten Maustaste** auf den Namen des Projekts ThreatDetectionModule. Klicken Sie im Menü auf **Eigenschaften**.</br>
   ![model](media\ad-fs-risk-assessment-model\risk6.png)
   
   b.   Von der **Eigenschaften** auf **Signierung**, auf der linken Seite, und suchen Sie dann das Kontrollkästchen markiert **Assembly signieren**. Von der **Schlüsseldatei mit starkem Namen auswählen**: Ziehen Sie nach unten, wählen Sie im Menü **< neu... >**</br>
   ![model](media\ad-fs-risk-assessment-model\risk7.png)

   c.   In der **Schlüssel für einen starken Namen erstellen Dialogfeld**, geben Sie einen Namen (Sie können einen beliebigen Namen wählen) für den Schlüssel, deaktivieren Sie das Kontrollkästchen **Schlüsseldatei mit Kennwort schützen**. Klicken Sie dann auf **OK**.
   ![model](media\ad-fs-risk-assessment-model\risk8.png)</br>
 
   d.   Speichern Sie das Projekt aus, wie unten dargestellt.</br>
   ![model](media\ad-fs-risk-assessment-model\risk9.png)

 7. Erstellen Sie das Projekt, indem Sie auf **erstellen** und dann **Projektmappe neu erstellen** wie unten dargestellt.</br>
 ![model](media\ad-fs-risk-assessment-model\risk10.png)
 
 Überprüfen Sie die **Fenster "Ausgabe"** , am unteren Bildschirmrand, um festzustellen, ob Fehler aufgetreten sind</br>
 ![model](media\ad-fs-risk-assessment-model\risk11.png)


Die plug-in (Dll) ist nun bereit für die Verwendung und befindet sich in der **\bin\Debug** Ordner des Projektordners (In meinem Fall, dass das **C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**). 

Der nächste Schritt ist diese DLL-Datei mit AD FS registrieren, sodass sie mit AD FS-Authentifizierungsprozess ausgeführt wird. 

### <a name="register-the-plug-in-dll-with-ad-fs"></a>Registrieren Sie die Plug-in-Dll mit AD FS

Wir müssen zum Registrieren der Dll in AD FS mithilfe der `Register-AdfsThreatDetectionModule` PowerShell-Befehl auf dem AD FS-Server, jedoch bevor wir registrieren zu können, müssen wir das öffentliche Schlüsseltoken zu erhalten. Dieses Token des öffentlichen Schlüssels erstellt wurde, wenn wir den Schlüssel erstellt haben, und die Dll mit diesem Schlüssel signiert. Erfahren Sie, was das öffentliche Schlüsseltoken für die Dll ist, können Sie die **SN.exe** wie folgt

 1. Kopieren Sie die Dll-Datei aus dem **\bin\Debug** Ordner an einen anderen Speicherort (In meinem Fall, die sie zum Kopieren **C:\extensions**)

 2. Starten der **Developer-Eingabeaufforderung** für Visual Studio, und wechseln Sie zum Verzeichnis mit der **sn.exe** (das Verzeichnis ist In meinem Fall **C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A \bin\NETFX 4.7.2 Tools**) ![Modell](media\ad-fs-risk-assessment-model\risk12.png)

 3. Führen Sie die **"sn"** -Befehl mit der **-T** Parameter und den Speicherort der Datei (In meinem Fall `SN -T “C:\extensions\ThreatDetectionModule.dll”`) ![Modell](media\ad-fs-risk-assessment-model\risk13.png)</br>
 Geben Sie der Befehl Token des öffentliche Schlüssels (für den Benutzer, die **öffentlichen Schlüsseltokens ist 714697626ef96b35**)

 4. Fügen Sie die Dll der **Global Assembly Cache** des AD FS-Servers unsere bewährte Methode wäre, einen ordnungsgemäßen Installer für das Projekt zu erstellen und verwenden Sie den Installer, um die Datei im globalen Assemblycache hinzuzufügen. Eine andere Lösung ist die Verwendung **Gacutil.exe** (Weitere Informationen zu **Gacutil.exe** verfügbaren [hier](https://docs.microsoft.com/dotnet/framework/tools/gacutil-exe-gac-tool)) auf Ihrem Entwicklungscomputer.  Da ich meine visual Studio auf demselben Server wie AD FS verfügen, ich verwenden **Gacutil.exe** wie folgt

   a.   Für Entwickler-Eingabeaufforderung für Visual Studio, und wechseln Sie zum Verzeichnis mit der **Gacutil.exe** (das Verzeichnis ist In meinem Fall **c:\Programme (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**)

   b.   Führen Sie die **Gacutil** Befehl (In meinem Fall `Gacutil /IF C:\extensions\ThreatDetectionModule.dll`) ![Modell](media\ad-fs-risk-assessment-model\risk14.png)
 
 >[!NOTE]
 >Wenn Sie eine AD FS-Farm, die den oben genannten verfügen auf jedem AD FS-Server in der Farm ausgeführt werden muss. 

 5. Open **Windows PowerShell** , und führen Sie den folgenden Befehl zum Registrieren der Dll
    ```
    Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>”
    ```
    In diesem Fall lautet der Befehl: 
    ```
    Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv”
    ```
 
    >[!NOTE]
    >Sie müssen die Dll nur einmal registrieren, auch wenn Sie eine AD FS-Farm verfügen. 

 6. Starten Sie den AD FS-Dienst nach dem Registrieren der dll

Das war alles, die Dll wird jetzt mit AD FS und bereit für die Verwendung registriert!

 >[!NOTE]
 > Wenn Änderungen, um das Plug-in vorgenommen werden, und das Projekt wird neu erstellt, muss die aktualisierte Dll erneut registriert werden. Vor der Registrierung, müssen Sie beim Aufheben der Registrierung der aktuellen Dll, die mithilfe des folgenden Befehls:</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br> In diesem Fall lautet der Befehl:
 >``` 
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>Testen das plug-in

 1. Öffnen der **authconfig.csv** Datei, die wir zuvor erstellt haben (in meinem Fall am Speicherort **C:\extensions**) und fügen die **Extranet-IP-Adressen** Sie blockieren möchten. Alle IP-Adresse sollte in einer separaten Zeile sein, und am Ende sollte kein Leerzeichen sein.</br>
 ![model](media\ad-fs-risk-assessment-model\risk18.png)
 
 2. Speichern Sie und schließen Sie die Datei

 3. Importieren Sie die aktualisierte Datei in AD FS mit den folgenden PowerShell-Befehl 

  ```
  Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
  ```
 
  In diesem Fall lautet der Befehl: 
  ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
 ```
 
 4. Initiieren der Authentifizierungsanforderung von der Server mit der gleichen IP-Adresse, die Sie hinzugefügt, in haben **authconfig.csv**.

 Für diese Demo ich verwenden [AD FS-Hilfe Claims x-Ray-Tool](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) zum Initiieren einer Anforderungs. Wenn Sie das x-Ray-Tool verwenden möchten, befolgen Sie die Anweisungen 

 Geben Sie Verbund-Server-Instanz, und drücken Sie **Authentifizierung testen** Schaltfläche.</br> 
 ![model](media\ad-fs-risk-assessment-model\risk15.png) 

 5. Authentifizierung ist blockiert, wie unten dargestellt.</br>
 ![model](media\ad-fs-risk-assessment-model\risk16.png)
 
Nun, wir wissen, wie zum Erstellen und registrieren Sie das plug-in, lassen Sie uns eingeführt Exemplarische Vorgehensweise der Plug-in-Code auf die Implementierung, die über die neuen Schnittstellen und Klassen zu verstehen, mit dem Modell. 

## <a name="plug-in-code-walkthrough"></a>Exemplarische Vorgehensweise für Plug-in-code

Öffnen Sie das Projekt `ThreatDetectionModule.sln` mithilfe von Visual Studio, und öffnen Sie dann auf die Hauptdatei **UserRiskAnalyzer.cs** aus der **Projektmappen-Explorer** auf der rechten Seite des Bildschirms</br>
![model](media\ad-fs-risk-assessment-model\risk17.png)
 
Die Datei enthält die Hauptklasse UserRiskAnalyzer, die von der abstrakten Klasse implementiert [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) und Schnittstelle [IRequestReceivedThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) , lesen die IP-Adresse aus der Anforderung Kontext, vergleichen die erhaltenen IP-Adresse mit der IP-Adressen von AD FS-Datenbank geladen, und Anforderung blockieren, wenn eine IP-Übereinstimmung vorhanden ist. Gehen Sie wir diese Typen im detail

### <a name="threatdetectionmodule-abstract-class"></a>Abstrakte Klasse ThreatDetectionModule

Diese abstrakte Klasse lädt das plug-in in AD FS-Pipeline, sodass mit der Plug-in-Code mit AD FS-Prozess ausgeführt werden. 

```
public abstract class ThreatDetectionModule 
{ 
    protected ThreatDetectionModule(); 
 
    public abstract string VendorName { get; } 
    public abstract string ModuleIdentifier { get; } 
 
 public abstract void OnAuthenticationPipelineLoad(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 public abstract void OnAuthenticationPipelineUnload(ThreatDetectionLogger logger); 
  public abstract void OnConfigurationUpdate(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 }   
```
Die Klasse enthält folgende Methoden und Eigenschaften.

|Methode |Typ|Definition|
|-----|-----|-----| 
|[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |Void|Aufgerufen von AD FS beim Laden des Plug-Ins in ihrer pipeline| 
|[OnAuthenticationPipelineUnload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |Void|Wird aufgerufen, von AD FS, wenn das Plug-in aus dem die Pipeline entladen wird| 
|[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| Void|Wird aufgerufen, von AD FS beim Konfigurationsupdate |
|**Eigenschaft** |**Typ** |**Definition**|
|[VendorName](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|Zeichenfolge |Ruft den Namen des Herstellers, besitzt die-Plug-in|
|[ModuleIdentifier](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|Zeichenfolge |Ruft den Bezeichner des Plug-Ins|

In unserem Beispiel-Plug-in verwenden wir [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) und [OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) Methoden, um die vorab definierten IP-Adressen aus AD FS-Datenbank zu lesen. [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) wird aufgerufen, wenn Sie mit AD FS beim-Plug-in registriert ist [OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) wird aufgerufen, wenn das CSV importiert wird mithilfe der `Import-AdfsThreatDetectionModuleConfiguration` Cmdlet. 

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>IRequestReceivedThreatDetectionModule Interface

Dies [Schnittstelle](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019) ermöglicht es Ihnen, risikobewertung, an dem Punkt zu implementieren, AD FS die Authentifizierungsanforderung empfängt jedoch bevor der Benutzer Anmeldeinformationen z. B. in Anforderung empfangen-Phase des Authentifizierungsprozesses eingibt. 
 
```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger, 
RequestContext requestContext );
}
```

Die Schnittstelle enthält [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) Methode den Kontext der Authentifizierungsanforderung verwenden, können zu übergeben, in der RequestContext-Eingabeparameter für Ihre Risk Assessment Logik schreiben. Der RequestContext-Parameter ist vom Typ [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019). 

Der andere Eingabeparameter übergeben wird, Protokollierung, der Typ ist [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019). Der Parameter kann verwendet werden, um den Fehler zu schreiben überwachen und/oder Debugmeldungen in AD FS-Protokolle. 

Gibt die Methode zurück [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (0, wenn NotEvaluated, 1, um die Blockierung und 2, zulassen) und AD FS das dann entweder blockiert oder lässt die Anforderung.

In unserem Beispiel-Plug-in [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019) methodenimplementierung analysiert die [ClientIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses) aus der [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019) Parameter, und vergleicht ihn mit der IP-Adressen aus der AD FS-Datenbank geladen. Wenn eine Übereinstimmung gefunden wird, gibt Methode 2 für **Block**, andernfalls gibt 1 für **zulassen**. Basierend auf den zurückgegebenen Wert, AD FS entweder blockiert oder lässt die Anforderung. 

>[!NOTE]
>Das Beispiel-Plug-in erwähnte nur IRequestReceivedThreatDetectionModule-Schnittstelle implementiert. Das Risk Assessment-Modell bietet jedoch zwei zusätzliche-Schnittstellen – IPreAuthenticationThreatDetectionModule (um Risk Assessment Logik und vorauthentifizierungsphase implementiert) und IPostAuthenticationThreatDetectionModule (um das Risiko zu implementieren. Bewertung Logik Phase nach der Authentifizierung). Die Details zu den beiden Schnittstellen sind nachfolgend aufgeführt. 

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>IPreAuthenticationThreatDetectionModule-Schnittstelle 

Dies [Schnittstelle](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019) ermöglicht es Ihnen, Risk Assessment Logik an dem Punkt zu implementieren, wenn Benutzer die Anmeldeinformationen bereitstellt, aber bevor Sie AD FS z. B. vorauthentifizierungsphase ausgewertet. 

```
public interface IPreAuthenticationThreatDetectionModule
{
Task<ThrottleStatus> EvaluatePreAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
IList<Claim> additionalClams
);
}
```
Die Schnittstelle enthält [EvaluatePreAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019) Methode können Sie die Informationen zu übergeben, der [RequestContext RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext ](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [ProtocolContext ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019), und [IList<Claim> AdditionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) Eingabeparameter, die Vorauthentifizierung Risk Assessment Logik zu schreiben. 

>[!NOTE]
>Liste der Eigenschaften, die mit jeder Art von Kontext übergeben werden, finden Sie unter [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), und [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) Klassendefinitionen. 

Der andere Eingabeparameter übergeben wird, Protokollierung, der Typ ist [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019). Der Parameter kann verwendet werden, um den Fehler zu schreiben überwachen und/oder Debugmeldungen in AD FS-Protokolle.

Gibt die Methode zurück [ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (0, wenn NotEvaluated, 1, um die Blockierung und 2, zulassen) und AD FS das dann entweder blockiert oder lässt die Anforderung. 

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>IPostAuthenticationThreatDetectionModule-Schnittstelle

Dies [Schnittstelle](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019) ermöglicht es Ihnen, Risk Assessment Logik implementieren, nachdem Benutzer Anmeldeinformationen angegeben hat, und AD FS hat die Authentifizierung, d. h. die Phase nach der Authentifizierung ausgeführt. 

```
public interface IPostAuthenticationThreatDetectionModule
{
Task<RiskScore> EvaluatePostAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
AuthenticationResult authenticationResult, 
IList<Claim> additionalClams
);
}
```

Die Schnittstelle enthält [EvaluatePostAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019) Methode können Sie die Informationen zu übergeben, der [RequestContext RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext SecurityContext ](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), [ProtocolContext ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019), und [IList<Claim> AdditionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2) Eingabeparameter Ihre nachauthentifizierung Risk Assessment Logik schreiben. 

>[!NOTE]
> Vollständige Liste der Eigenschaften, die mit jeder Art von Kontext übergeben, finden Sie unter [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019), [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019), und [ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019) Klassendefinitionen. 

Der andere Eingabeparameter übergeben wird, Protokollierung, der Typ ist [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019). Der Parameter kann verwendet werden, um den Fehler zu schreiben überwachen und/oder Debugmeldungen in AD FS-Protokolle. 

Die Methode gibt die [Risk Score](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019) die in AD FS-Richtlinie verwendet werden kann und die Anspruchsregeln. 

>[!NOTE]
>Für plug-in funktioniert, muss auf die Hauptklasse (in diesem Fall UserRiskAnalyzer) ableiten [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019) abstrakte Klasse, und sollte mindestens eine der oben beschriebenen drei Schnittstellen implementieren. Nachdem die Dll registriert wurde, wird AD FS überprüft, welche Schnittstellen implementiert werden, und Sie geeigneten Zeitpunkt in der Pipeline aufgerufen werden.

### <a name="faqs"></a>Häufig gestellte Fragen

**Warum sollte ich diese Plug-Ins erstellen?**</br>
**A:** Diese Plug-Ins bieten Ihnen nicht nur zusätzliche Funktionen zum Schützen Ihrer Umgebung vor Angriffen wie z. B. Sprühende Angriffe auf Kennwörter, aber auch bieten Ihnen die Flexibilität, Ihre eigene Logik zum Risk Assessment je nach Ihren Anforderungen zu erstellen. 

**Wo sind die Protokolle erfasst?**</br>
**A:** Fehlerprotokolle können in "AD FS/Administrator"-Ereignisprotokoll mit WriteAdminLogErrorMessage-Methode geschrieben, Überwachungsprotokolle in "AD FS-Überwachung" Sicherheit, melden Sie sich mit WriteAuditMessage-Methode, und Debugprotokolle in "AD FS-Ablaufverfolgung" Debugprotokoll mit WriteDebugMessage-Methode. 

**Kann diese-Plug-ins hinzufügen prozesslatenz für AD FS-Authentifizierung erhöhen?**</br>
**A:** Auswirkungen auf die Wartezeit wird die Zeitdauer für die Logik des Risk Assessment ausgeführt, die Sie implementieren, ermittelt werden. Wir empfehlen die Latenz Auswirkungen vor der Bereitstellung das plug-in in der produktionsumgebung befinden. 

**Warum vorschlagen können nicht AD FS die Liste der riskanten IP-Adressen, Benutzer usw.?**</br>
**A:** Obwohl derzeit nicht verfügbar, arbeiten wir zum Erstellen der intelligente Funktionen, um riskante IP-Adressen, Benutzer usw., in das austauschbare Risikomodell Bewertung empfohlen. Wir geben den Start in Kürze Datumsangaben. 
