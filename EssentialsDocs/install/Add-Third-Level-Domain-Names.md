---
title: "Hinzufügen von Domänennamen der dritten Ebene"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 64bf24e45155fdd981e2061b3de7ebce1c53b36c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-third-level-domain-names"></a>Hinzufügen von Domänennamen der dritten Ebene

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können die Möglichkeit für Benutzer Domänennamen der dritten Ebene in den Domain Name-Assistenten anzufordern hinzufügen. Dazu erstellen und installieren Sie eine Codeassembly, die vom Domain-Manager im Betriebssystem verwendet wird.  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>Erstellen Sie einen Anbieter von Domänennamen der dritten Ebene  
 Sie können Domänennamen der dritten Ebene verfügbar machen, erstellen und installieren eine Codeassembly, die der Assistent den Domänennamen bereitstellt. Zu diesem Zweck müssen Sie die folgenden Aufgaben ausführen:  
  
-   [Hinzufügen einer Implementierung der IDomainSignupProvider-Schnittstelle zur assembly](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [Hinzufügen einer Implementierung der IDomainMaintenanceProvider-Schnittstelle zur assembly](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [Signieren der Assembly mit Authenticode-Signatur](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [Installieren Sie die Assembly auf dem Referenzcomputer](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Starten Sie den Dienst Windows Server-Domänennamenverwaltung](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="BKMK_DomainSignup"></a>Hinzufügen einer Implementierung der IDomainSignupProvider-Schnittstelle zur assembly  
 Die IDomainSignupProvider-Schnittstelle wird verwendet, um dem Assistenten domänenangebote hinzufügen.  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>Die IDomainSignupProvider-Code auf die Assembly hinzufügen  
  
1.  Öffnen Sie Visual Studio2008 als Administrator mit der rechten Maustaste in das Programm in die **starten** Menü und Auswählen von **als Administrator ausführen**.  
  
2.  Klicken Sie auf **Datei**, klicken Sie auf **neu**, und klicken Sie dann auf **Projekt**.  
  
3.  In der **neues Projekt** Dialogfeld, klicken Sie auf **Visual C#-**, klicken Sie auf **Klassenbibliothek**, geben Sie einen Namen für die Projektmappe, und klicken Sie dann auf **OK**.  
  
4.  Benennen Sie die Datei Class1.cs. Beispielsweise MyDomainNameProvider.cs  
  
5.  Fügen Sie Verweise auf die Dateien Wssg.Web.DomainManagerObjectModel.dll "," CertManaged.dll "," WssgCertMgmt.dll "und" WssgCommon.dll.  
  
6.  Fügen Sie die folgenden using-Anweisungen hinzu.  
  
    ```c#  
  
    using System.Collections.ObjectModel;  
    using System.Net;  
    using System.Net.Sockets;  
    using Microsoft.WindowsServerSolutions.Certificates;  
    using Microsoft.WindowsServerSolutions.CertificateManagement;  
    using Microsoft.WindowsServerSolutions.Common;  
    using Microsoft.Win32;  
    ```  
  
7.  Ändern Sie den Namespace und den klassenheader entsprechend dem folgenden Beispiel.  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  Fügen Sie der Klasse, die definiert die Angebote im Assistenten die Initialize-Methode und die erforderlichen Variablen hinzu.  
  
    > [!NOTE]
    >  Die Initialize-Methode definiert einen Bezeichner für den domänenanbieter, der eindeutig sein muss. Eine typische Möglichkeit hierzu ist eine GUID als Bezeichner definiert. Weitere Informationen zum Erstellen einer GUID finden Sie unter [GUID erstellen (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098).  
  
     Das folgende Codebeispiel zeigt die Initialize-Methode.  
  
    ```c#  
  
    static readonly Guid MyID = new Guid("8C999DF5-696A-47af-822D-94F1673D3397");  
    public Guid ID { get { return MyID; } }  
    public string Name { get { return "My Provider"; } }  
    List<Offering> offerings = new List<Offering>();  
  
    public void Initialize(DomainProviderSettings config)  
    {  
       var offer1 = new Offering()  
       {  
          Description = "My Domain Provider",  
          Name = "Offering 1",  
          ProviderID = ID,  
          MoreInfoUrl = new Uri("http://www.contoso.com"),  
          MembershipServiceName = "My Membership",  
          EulaUrl = new Uri("http://www.contoso.com"),  
       };  
  
       this.offerings.Add(offer1);  
       RegistryKey key =   
          Registry.LocalMachine.CreateSubKey(@"Software\Microsoft\Windows Server\Domain Manager\Settings");  
       key.Close();  
    }  
    ```  
  
9. Fügen Sie die GetOfferings-Methode, die die Liste der Angebote, die initialisiert wurde im vorherigen Schrittzurückgibt. Das folgende Codebeispiel zeigt die GetOfferings-Methode.  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. Fügen Sie die FindOfferingForDomain-Methode, die das Angebot aus der Liste zurückgibt. Das folgende Codebeispiel zeigt die FindOfferingForDomain-Methode.  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. Fügen Sie die SetCredentials-Methode, die die Anmeldeinformationen definiert, die zum Zugriff auf die Angebote erforderlich sind. Das folgende Codebeispiel zeigt die SetCredentials-Methode.  
  
    ```c#  
  
    private string currentUser { get; set; }  
    private string currentPassword { get; set; }  
  
    public bool SetCredentials(DomainNameRequest request,   
       DomainProviderCredentials credentials, bool validate)  
    {  
       currentUser = credentials.UserName;  
       currentPassword = credentials.Password;  
       if (validate)  
       {  
          return ValidateCredentials();  
       }  
  
       return true;  
    }  
    ```  
  
12. Fügen Sie die ValidateCredentials-Methode, die die durch die SetCredentials definierten Anmeldeinformationen überprüft. Das folgende Codebeispiel zeigt die ValidateCredentials-Methode.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (IsUser())  
          return string.Equals(currentPassword, offerPassword);  
       else  
          return false;  
    }   
  
    private bool IsUser()  
    {  
       return string.Equals(currentUser, offerUser, StringComparison.OrdinalIgnoreCase);  
    }  
    ```  
  
13. Fügen Sie die GetAvailableDomainRoots-Methode, die die Liste der Stammdomänennamen zurückgibt, die von den in der Anforderung angegebenen Angebot unterstützt werden. Diese Liste der Stammdomänennamen darf nicht leer sein. Das folgende Codebeispiel zeigt die GetAvailableDomainRoots-Methode.  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. Fügen Sie die GetUserDomainNames-Methode, die eine Liste von Domänennamen, die der aktuelle Benutzer bereits besitzt zurückgibt, vom aktuellen Angebot. Diese Liste kann leer sein. Das folgende Codebeispiel zeigt die GetUserDomainNames-Methode.  
  
    ```c#  
  
    public static readonly string AvailableDomain1 = "available.domain1.com",  
       AvailableDomain2 = "available.domain2.com";  
    public static readonly string OccupiedDomain1 = "occupied.domain1.com",  
       OccupiedDomain2 = "occupied.domain2.com";  
  
    public ReadOnlyCollection<string> GetUserDomainNames(DomainNameRequest request)  
    {  
       var userDomains = new List<string>();  
       userDomains.Add(OccupiedDomain1);  
       userDomains.Add(AvailableDomain1);  
  
       return userDomains.AsReadOnly();  
    }  
    ```  
  
15. Fügen Sie die GetUserDomainQuota-Methode, die die maximale Anzahl von Domänen zurückgibt, die die angegebene Angebot ermöglicht. Wenn ein Maximum nicht anwendbar ist, sollte diese Methode 0 zurück. Das folgende Beispiel zeigt die GetUserDomainQuota-Methode.  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. Fügen Sie die CheckDomainAvailability-Methode, die für die Verfügbarkeit des Domänennamens überprüft und können eine Liste mit Vorschlägen zurückgeben. Das folgende Codebeispiel zeigt die CheckDomainAvailability-Methode.  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. Fügen Sie die CommitDomain-Methode, die den angeforderten Domänennamen übergibt. Erfolgreiche Abschluss dieser Methode bedeutet, dass der Domänenname dem Benutzerkonto zugeordnet ist, der Wartungsanbieter wird sofort aufgerufen, um das Zertifikat abzurufen, wenn der Status "fullyoperational" ist und der Anbieter und das Angebot aktiviert werden. Das folgende Codebeispiel zeigt die CommitDomain-Methode.  
  
    ```c#  
  
    public DomainStatus CommitDomain(DomainNameRequest request)  
    {              
       ReadOnlyCollection<string> suggestions;  
       if (!CheckDomainAvailability(request, out suggestions))  
       {  
          throw new DomainException(FailureReason.InvalidDomainName, null, null);  
       }  
  
       return DomainStatus.Ready;  
    }  
    ```  
  
18. Fügen Sie die ReleaseDomain-Methode, die den Anbieter darüber informiert, den der Benutzer den Domänennamen freigeben möchte. Das folgende Codebeispiel zeigt die ReleaseDomain-Methode.  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. Fügen Sie die GetProviderLandingUrl-Methode, die die URL für die Angebotsseite im domänenanmeldeworkflow zurückgibt. Das folgende Codebeispiel zeigt die GetProviderLandingUrl-Methode.  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. Fügen Sie die GetDomainMaintenanceProvider-Methode, die eine Instanz der idomainmaintenanceprovider-Schnittstelle zurückgibt, die für domänenwartungsaufgaben verwendet wird. Diese Methode wird aufgerufen, nachdem die CommitDomain-Methode erfolgreich ist, und wenn Domain-Manager gestartet wird. Das folgende Codebeispiel zeigt die GetDomainMaintenanceProvider-Methode.  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. Speichern Sie das Projekt, und schließen Sie es nicht, da Sie es mit dem nächsten Verfahren hinzufügen möchten. Sie werden nicht zum Erstellen des Projekts, bis Sie das nächste Verfahren ausführen können.  
  
###  <a name="BKMK_DomainMaintenance"></a>Hinzufügen einer Implementierung der IDomainMaintenanceProvider-Schnittstelle zur assembly  
 Der idomainmaintenanceprovider-Schnittstelle wird verwendet, um die Domäne zu verwalten, nachdem dieser erstellt wurde.  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>Der Assembly den Code für "idomainmaintenanceprovider" hinzu  
  
1.  Fügen Sie den klassenheader für den domänenwartungsanbieter hinzu. Stellen Sie sicher, dass der Name, den Sie für den Anbieter definiert den Namen in der GetDomainMaintenanceProvider-Methode übereinstimmt, die Sie zuvor definiert.  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  Fügen Sie die Activate-Methode, die den aktiven Anbieter festlegt. Das folgende Codebeispiel zeigt die Activate-Methode.  
  
    ```c#  
  
    string DomainName { get; set; }  
    protected DomainProviderSettings Settings { get; set; }  
  
    public void Activate(DomainProviderSettings settings,   
       DomainNameConfiguration config, DomainProviderCredentials credentials)  
    {  
       Settings = settings;  
       SetCredentials(credentials);  
       DomainName = config.AutoConfiguredAnywhereAccessFullName.Punycode;  
    }  
    ```  
  
3.  Fügen Sie die Deactivate-Methode, die verwendet wird, um alle Aktionen zu deaktivieren. Das folgende Codebeispiel zeigt die Deactivate-Methode.  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  Fügen Sie die SetCredentials-Methode, die Anmeldeinformationen des Benutzers aktualisiert. Diese Methode kann beispielsweise aufgerufen werden, um Anmeldeinformationen zu aktualisieren, die nicht mehr gültig sind. Das folgende Codebeispiel zeigt die SetCredentials-Methode.  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  Fügen Sie die ValidateCredentials-Methode, die die angegebenen Anmeldeinformationen überprüft. Das folgende Codebeispiel zeigt die ValidateCredentials-Methode.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (string.Equals(this.Credentials.UserName,   
          offerUser,   
          StringComparison.OrdinalIgnoreCase) &&   
             string.Equals(this.Credentials.Password, offerPassword))  
          return true;  
  
       return false;  
    }  
    ```  
  
6.  Fügen Sie die GetPublicAddress-Methode, die externe IP-Adresse des Servers zurückgibt. Das folgende Codebeispiel zeigt die GetPublicAddress-Methode.  
  
    ```c#  
  
    public IPAddress GetPublicIPAddress()  
    {  
       string PublicIP = "0.0.0.0";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          PublicIP = (key == null) ? "0.0.0.0" : key.GetValue("PublicIP", "0.0.0.0").ToString();  
       }  
       IPAddress ip = IPAddress.Parse(PublicIP);  
  
       if (PublicIP == "0.0.0.0")  
       {  
          string strHostName = Dns.GetHostName();  
          IPHostEntry ipEntry = Dns.GetHostEntry(strHostName);  
  
          IPAddress[] addr = ipEntry.AddressList;  
          foreach (IPAddress add in addr)  
          {  
             if (add.AddressFamily == AddressFamily.InterNetwork)  
             {  
                return add;  
             }  
          }  
       }  
       else  
       {  
          return IPAddress.Parse(PublicIP);  
       }  
  
       return null;    
    }  
    ```  
  
7.  Fügen Sie die SubmitCertificateRequest-Methode, die die Zertifikatanforderung für den gegenwärtig konfigurierten Domänennamen übermittelt.  
  
    ```c#  
  
    string cert=null;  
  
    public void SubmitCertificateRequest(string certificateRequest)  
    {  
       cert = CertManaged.SubmitRequest(certificateRequest, CertCommon.CAServerFQDN + "\\" +      
          CertCommon.CAName,   
          Microsoft.WindowsServerSolutions.CertificateManagement.CRFlags.Base64Header,   
          CertCommon.CATemplate,   
          EncodingFlags.Base64);  
    }  
    ```  
  
8.  Fügen Sie die GetCertificateResponse-Methode, die der Zertifikatantwort zurückgibt, wenn der Domänenstatus "fullyoperational" ist. Diese Methode wird für neue Zertifikatanforderungen und für zertifikaterneuerungsanforderungen aufgerufen. Das folgende Codebeispiel zeigt die GetCertificateResponse-Methode.  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. Fügen Sie die SubmitRenewCertificateRequest-Methode, die die Erneuerung des Zertifikats verarbeitet. Das folgende Codebeispiel zeigt die SubmitRenewCertificateRequest-Methode.  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. Fügen Sie die UpdateDNSRecords-Methode, die vom Anbieter gespeicherten DNS-Einträge aktualisiert. Das folgende Codebeispiel zeigt die UpdateDNS-Methode.  
  
    ```c#  
  
    public bool UpdateDnsRecords(IList<DnsRecord> records)  
    {  
       string UpdateDNS = "true";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          UpdateDNS = (key == null) ? "true" : key.GetValue("UpdateDNS", "true").ToString();  
       }  
  
       return UpdateDNS == "true";  
    }  
  
    ```  
  
11. Fügen Sie die TestConnection-Methode, die versucht, eine Verbindung zu Back-End-Dienst hinzu. Wenn diese Methode eine Authentifizierung erforderlich ist, sollte eine entsprechende Ausnahme ausgelöst. Das folgende Codebeispiel zeigt die TestConnection-Methode.  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. Fügen Sie die GetDomainState-Methode, die den aktuellen Zustand der Domäne zurückgibt. Das folgende Codebeispiel zeigt die GetDomainState-Methode.  
  
    ```c#  
  
    public DomainState GetDomainState()  
    {  
       string domainstatus = "FullyOperational";  
       long expirationDate = 365;  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          domainstatus = (key == null) ? "Ready" : key.GetValue("DomainStatus", "Ready").ToString();  
          expirationDate = Int64.Parse(key.GetValue("ExpirationDate", "365").ToString());  
       }  
  
       switch (domainstatus)  
       {  
          case "Failed":  
             return new DomainState(DomainStatus.Failed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Ready":  
             return new DomainState(DomainStatus.Ready,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewal":  
             return new DomainState(DomainStatus.InRenewal,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewalCustomerInterventionRequired":  
             return new DomainState(DomainStatus.InRenewalCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Pending":  
             return new DomainState(DomainStatus.Pending,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "PendingCustomerInterventionRequired":  
             return new DomainState(DomainStatus.PendingCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "RenewalFailed":  
             return new DomainState(DomainStatus.RenewalFailed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          default:  
             return new DomainState(DomainStatus.Unknown,   
                null,   
                DateTime.Now.AddDays(expirationDate));                   
          }  
    }  
    ```  
  
13. Fügen Sie die GetCertificateState-Methode, die den aktuellen Status des Zertifikats zurückgibt. Das folgende Codebeispiel zeigt die GetCertificateState-Methode.  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. Speichern Sie und erstellen Sie die Projektmappe.  
  
###  <a name="BKMK_SignAssembly"></a>Signieren der Assembly mit Authenticode-Signatur  
 Sie müssen mit Authenticode Signieren der Assembly für sie in das Betriebssystem verwendet werden. Weitere Informationen zum Signieren der Assembly finden Sie unter [signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).  
  
###  <a name="BKMK_InstallAssembly"></a>Installieren Sie die Assembly auf dem Referenzcomputer  
 Fügen Sie der Assembly in einem Ordner auf dem Referenzcomputer. Notieren Sie sich den Ordnerpfad, da Sie ihn in der Registrierung im nächsten Schritteingeben werden.  
  
### <a name="add-a-key-to-the-registry"></a>Fügen Sie einen Schlüssel zur Registrierung hinzu  
 Sie fügen einen Registrierungseintrag, um die Eigenschaften und den Speicherort der Assembly zu definieren.  
  
##### <a name="to-add-a-key-to-the-registry"></a>Hinzufügen eines Schlüssels zur Registrierung  
  
1.  Klicken Sie auf dem Referenzcomputer auf **starten**, geben Sie **Regedit**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**, erweitern Sie **Manager**, und erweitern Sie dann **Anbieter**.  
  
3.  Mit der rechten Maustaste **Anbieter**, zeigen Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Geben Sie den Bezeichner für den Anbieter als Namen für den Schlüssel. Der Bezeichner ist die GUID, die Sie für den Anbieter in Schritt8 von definiert [Hinzufügen einer Implementierung der IDomainSignupProvider-Schnittstelle zur Assembly](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup).  
  
5.  Maustaste, die Sie gerade erstellt haben, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Typ **Assembly** für den Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  
  
7.  Mit der rechten Maustaste die neue **Assembly** im rechten Bereich eine Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
8.  Geben Sie den vollständigen Pfad zur Assemblydatei, die Sie zuvor erstellt haben, und klicken Sie dann auf **OK**.  
  
9. Mit der rechten Maustaste erneut auf des Schlüssels, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
10. Typ **aktiviert** für den Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  
  
11. Mit der rechten Maustaste die neue **aktiviert** im rechten Bereich eine Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
12. Typ **True**, und klicken Sie dann auf **OK**.  
  
13. Mit der rechten Maustaste erneut auf des Schlüssels, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
14. Typ **Typ** für den Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  
  
15. Mit der rechten Maustaste die neue **Typ** im rechten Bereich eine Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
16. Geben Sie den vollständigen Klassennamen des Anbieters in der Assembly definiert, und klicken Sie dann auf **OK**.  
  
###  <a name="BKMK_RestartService"></a>Starten Sie den Dienst Windows Server-Domänennamenverwaltung  
 Sie müssen neu starten, die Windows Server-Dienst für den Anbieter, um das Betriebssystem zur Verfügung gestellt.  
  
##### <a name="restart-the-service"></a>Starten Sie den Dienst neu.  
  
1.  Klicken Sie auf **starten**, Typ **Mmc**, und drücken Sie dann die **EINGABETASTE**.  
  
2.  Wenn das Dienste-Snap-In in der Konsole nicht aufgeführt ist, fügen Sie es mithilfe des folgenden Verfahrens:  
  
    1.  Klicken Sie auf **Datei**, und klicken Sie dann auf **Snap-In hinzufügen/entfernen**.  
  
    2.  In der **Verfügbare Snap-Ins** auf **Dienste**, und klicken Sie dann auf **hinzufügen**.  
  
    3.  In der **Dienste** Dialogfeld sicher, dass **lokalen Computer** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    4.  Klicken Sie auf **OK** zum Schließen der **-Snap-Ins hinzufügen/entfernen** Dialogfeld.  
  
3.  Doppelklicken Sie auf **Dienste**, scrollen Sie nach unten, und wählen Sie **Windows Server-Domänenverwaltung**, und klicken Sie dann auf **starten Sie den Dienst**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)