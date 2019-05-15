---
title: Hinzufügen von Domänennamen der dritten Ebene
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833321"
---
# <a name="add-third-level-domain-names"></a>Hinzufügen von Domänennamen der dritten Ebene

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können es Benutzern ermöglichen, Domänennamen der dritten Ebene im Assistenten zum Einrichten von Domänennamen anzufordern. Dazu erstellen und installieren Sie eine Codeassembly, die vom Domain-Manager im Betriebssystem verwendet wird.  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>Erstellen eines Anbieters für Domänennamen der dritten Ebene  
 Sie können Domänennamen der dritten Ebene verfügbar machen, indem Sie eine Codeassembly erstellen und installieren, die dem Assistenten Domänennamen bereitstellt. Dazu führen Sie die folgenden Schritte aus:  
  
-   [Eine Implementierung der IDomainSignupProvider-Schnittstelle zur Assembly hinzufügen](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [Eine Implementierung der IDomainMaintenanceProvider-Schnittstelle zur Assembly hinzufügen](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [Signieren der Assembly mit Authenticode-Signatur](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [Installieren Sie die Assembly, auf dem Referenzcomputer](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Starten Sie den Dienst von Windows Server-Domänennamenverwaltung](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="BKMK_DomainSignup"></a> Eine Implementierung der IDomainSignupProvider-Schnittstelle zur Assembly hinzufügen  
 Die IDomainSignupProvider-Schnittstelle wird verwendet, um dem Assistenten Domänenangebote hinzufügen.  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>So fügen Sie der Assembly den Code für "IDomainSignupProvider" hinzu  
  
1.  Öffnen Sie Visual Studio 2008 als Administrator, indem Sie im Menü **Start** mit der rechten Maustaste auf das Programm klicken und **Als Administrator ausführen** auswählen.  
  
2.  Klicken Sie auf **Datei**, auf **Neu**und anschließend auf **Projekt**.  
  
3.  Klicken Sie im Dialogfeld **Neues Projekt** auf **Visual C#**, klicken Sie auf **Klassenbibliothek**, geben Sie einen Namen für die Projektmappe ein, und klicken Sie dann auf **OK**.  
  
4.  Benennen Sie die Datei "Class1.cs" um, beispielsweise in "MyDomainNameProvider.cs".  
  
5.  Fügen Sie Verweise auf die Dateien "Wssg.Web.DomainManagerObjectModel.dll", "CertManaged.dll", "WssgCertMgmt.dll" und "WssgCommon.dll" hinzu.  
  
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
  
7.  Ändern Sie den Namespace und den Klassenheader entsprechend dem folgenden Beispiel.  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  Fügen Sie der Klasse die Initialize-Methode und die erforderlichen Variablen hinzu, um die Angebote im Assistenten zu definieren.  
  
    > [!NOTE]
    >  Die Initialize-Methode definiert einen Bezeichner für den Domänenanbieter, der eindeutig sein muss. Üblicherweise wird eine GUID als Bezeichner definiert. Weitere Informationen zum Erstellen einer GUID finden Sie unter [GUID erstellen (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098).  
  
     Mit dem folgenden Codebeispiel wird die Initialize-Methode veranschaulicht.  
  
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
  
9. Fügen Sie die GetOfferings-Methode hinzu, die die Liste der Angebote zurückgibt, die im vorherigen Schritt initialisiert wurde. Mit dem folgenden Codebeispiel wird die GetOfferings-Methode veranschaulicht.  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. Fügen Sie die FindOfferingForDomain-Methode hinzu, die das Angebot aus der Liste zurückgibt. Mit dem folgenden Codebeispiel wird die FindOfferingForDomain-Methode veranschaulicht.  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. Fügen Sie die SetCredentials-Methode hinzu, mit der die Anmeldeinformationen definiert werden, die für den Zugriff auf die Angebote erforderlich sind. Mit dem folgenden Codebeispiel wird die SetCredentials-Methode veranschaulicht.  
  
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
  
12. Fügen Sie die ValidateCredentials-Methode hinzu, die die durch die SetCredentials-Methode definierten Anmeldeinformationen überprüft. Mit dem folgenden Codebeispiel wird die ValidateCredentials-Methode veranschaulicht.  
  
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
  
13. Fügen Sie die GetAvailableDomainRoots-Methode hinzu, die die Liste der Stammdomänennamen zurückgibt, die von dem in der Anforderung angegebenen Angebot unterstützt werden. Diese Liste der Stammdomänennamen darf nicht leer sein. Mit dem folgenden Codebeispiel wird die GetAvailableDomainRoots-Methode veranschaulicht.  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. Fügen Sie die GetUserDomainNames-Methode hinzu, die abhängig vom aktuellen Angebot eine Liste von Domänennamen zurückgibt, die der aktuelle Benutzer bereits besitzt. Diese Liste kann leer sein. Mit dem folgenden Codebeispiel wird die GetUserDomainNames-Methode veranschaulicht.  
  
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
  
15. Fügen Sie die GetUserDomainQuota-Methode hinzu, die die maximale Anzahl von Domänen zurückgibt, die das angegebene Angebot zulässt. Wenn kein Maximum gilt, sollte diese Methode "0" zurückgeben. Mit dem folgenden Codebeispiel wird die GetUserDomainQuota-Methode veranschaulicht.  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. Fügen Sie die CheckDomainAvailability-Methode hinzu, die die Verfügbarkeit des angegebenen Domänennamens überprüft und eine Liste mit Vorschlägen zurückgeben kann. Mit dem folgenden Codebeispiel wird die CheckDomainAvailability-Methode veranschaulicht.  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. Fügen Sie die CommitDomain-Methode hinzu, die den angeforderten Domänennamen übergibt. Der erfolgreiche Abschluss dieser Methode bedeutet, dass der Domänenname dem Benutzerkonto zugeordnet ist. Der Wartungsanbieter wird sofort aufgerufen, um das Zertifikat abzurufen, wenn der Status "FullyOperational" ist. Der Anbieter und das Angebot werden aktiviert. Mit dem folgenden Codebeispiel wird die CommitDomain-Methode veranschaulicht.  
  
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
  
18. Fügen Sie die ReleaseDomain-Methode hinzu, die den Anbieter darüber informiert, dass der Benutzer den Domänennamen freigeben möchte. Mit dem folgenden Codebeispiel wird die ReleaseDomain-Methode veranschaulicht.  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. Fügen Sie die GetProviderLandingUrl-Methode hinzu, die die URL für die Angebotsseite im Domänenanmeldeworkflow zurückgibt. Mit dem folgenden Codebeispiel wird die GetProviderLandingUrl-Methode veranschaulicht.  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. Fügen Sie die GetDomainMaintenanceProvider-Methode hinzu, die eine Instanz der IDomainMaintenanceProvider-Schnittstelle zurückgibt, die für Domänenwartungsaufgaben verwendet wird. Diese Methode wird nach erfolgreicher Ausführung der CommitDomain-Methode und beim Start des Domain-Managers aufgerufen. Mit dem folgenden Codebeispiel wird die GetDomainMaintenanceProvider-Methode veranschaulicht.  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. Speichern Sie das Projekt, aber schließen Sie es nicht, da Sie es mit dem nächsten Verfahren erweitern. Sie können das Projekt erst erstellen, wenn Sie das nächste Verfahren abgeschlossen haben.  
  
###  <a name="BKMK_DomainMaintenance"></a> Eine Implementierung der IDomainMaintenanceProvider-Schnittstelle zur Assembly hinzufügen  
 Die IDomainMaintenanceProvider-Schnittstelle wird verwendet, um die Domäne zu verwalten, nachdem sie erstellt wurde.  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>So fügen Sie der Assembly den Code für "IDomainMaintenanceProvider" hinzu  
  
1.  Fügen Sie den Klassenheader für den Domänenwartungsanbieter hinzu. Stellen Sie sicher, dass der für den Anbieter definierte Name mit dem zuvor definierten Namen in der GetDomainMaintenanceProvider-Methode übereinstimmt.  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  Fügen Sie die Activate-Methode hinzu, die den aktiven Anbieter festlegt. Mit dem folgenden Codebeispiel wird die Activate-Methode veranschaulicht.  
  
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
  
3.  Fügen Sie die Deactivate-Methode hinzu, die verwendet wird, um alle Aktionen zu deaktivieren. Mit dem folgenden Codebeispiel wird die Deactivate-Methode veranschaulicht.  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  Fügen Sie die SetCredentials-Methode hinzu, die die Anmeldeinformationen des Benutzers aktualisiert. Diese Methode kann beispielsweise aufgerufen werden, um nicht mehr gültige Anmeldeinformationen zu aktualisieren. Mit dem folgenden Codebeispiel wird die SetCredentials-Methode veranschaulicht.  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  Fügen Sie die ValidateCredentials-Methode hinzu, die die angegebenen Anmeldeinformationen überprüft. Mit dem folgenden Codebeispiel wird die ValidateCredentials-Methode veranschaulicht.  
  
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
  
6.  Fügen Sie die GetPublicAddress-Methode hinzu, die die externe IP-Adresse des Servers zurückgibt. Mit dem folgenden Codebeispiel wird die GetPublicAddress-Methode veranschaulicht.  
  
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
  
7.  Fügen Sie die SubmitCertificateRequest-Methode hinzu, die die Zertifikatanforderung für den gegenwärtig konfigurierten Domänennamen übermittelt.  
  
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
  
8.  Fügen Sie die GetCertificateResponse-Methode hinzu, die eine Zertifikatantwort zurückgibt, wenn der Domänenstatus "FullyOperational" ist. Diese Methode wird für neue Zertifikatanforderungen und für Zertifikaterneuerungsanforderungen aufgerufen. Mit dem folgenden Codebeispiel wird die GetCertificateResponse-Methode veranschaulicht.  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. Fügen Sie die SubmitRenewCertificateRequest-Methode hinzu, die die Erneuerung des Zertifikats verarbeitet. Mit dem folgenden Codebeispiel wird die SubmitRenewCertificateRequest-Methode veranschaulicht.  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. Fügen Sie die UpdateDNSRecords-Methode hinzu, die die vom Anbieter gespeicherten DNS-Einträge aktualisiert. Mit dem folgenden Codebeispiel wird die UpdateDNS-Methode veranschaulicht.  
  
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
  
11. Fügen Sie die TestConnection-Methode hinzu, die versucht, eine Verbindung mit einem Back-End-Dienst herzustellen. Wenn für diese Methode eine Authentifizierung erforderlich ist, sollte eine entsprechende Ausnahme ausgelöst werden. Mit dem folgenden Codebeispiel wird die TestConnection-Methode veranschaulicht.  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. Fügen Sie die GetDomainState-Methode hinzu, die den aktuellen Status der Domäne zurückgibt. Mit dem folgenden Codebeispiel wird die GetDomainState-Methode veranschaulicht.  
  
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
  
13. Fügen Sie die GetCertificateState-Methode hinzu, die den aktuellen Status des Zertifikats zurückgibt. Mit dem folgenden Codebeispiel wird die GetCertificateState-Methode veranschaulicht.  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. Speichern und erstellen Sie die Projektmappe.  
  
###  <a name="BKMK_SignAssembly"></a> Signieren der Assembly mit Authenticode-Signatur  
 Sie müssen die Assembly mit Authenticode signieren, damit sie im Betriebssystem verwendet werden kann. Weitere Informationen zum Signieren der Assembly finden Sie unter [Signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).  
  
###  <a name="BKMK_InstallAssembly"></a> Installieren Sie die Assembly, auf dem Referenzcomputer  
 Platzieren Sie die Assembly in einem Ordner auf dem Referenzcomputer. Notieren Sie sich den Ordnerpfad, da Sie ihn im nächsten Schritt in die Registrierung einfügen.  
  
### <a name="add-a-key-to-the-registry"></a>Hinzufügen eines Schlüssels zur Registrierung  
 Sie fügen einen Registrierungseintrag hinzu, um die Eigenschaften und den Speicherort der Assembly zu definieren.  
  
##### <a name="to-add-a-key-to-the-registry"></a>So fügen Sie einen Schlüssel zur Registrierung hinzu  
  
1.  Klicken Sie auf dem Referenzcomputer auf **Start**, geben Sie **regedit**ein, und drücken Sie die **Eingabetaste**.  
  
2.  Erweitern Sie im linken Bereich **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, dann **Domain Managers** und schließlich **Providers**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Providers**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
4.  Geben Sie den Bezeichner für den Anbieter als Namen des Schlüssels ein. Der Bezeichner ist die GUID, die Sie für den Anbieter in Schritt 8 unter [Hinzufügen einer Implementierung der IDomainSignupProvider-Schnittstelle zur Assembly](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup) definiert haben.  
  
5.  Klicken Sie mit der rechten Maustaste auf den gerade erstellten Schlüssel, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Geben Sie **Assembly** als Namen der Zeichenfolge ein, und drücken Sie die **EINGABETASTE**.  
  
7.  Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Assembly**, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie den vollständigen Pfad der Assemblydatei ein, die Sie zuvor erstellt haben, und klicken Sie dann auf **OK**.  
  
9. Klicken Sie mit der rechten Maustaste erneut auf den Schlüssel, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
10. Geben Sie **Aktiviert** als Namen der Zeichenfolge ein, und drücken Sie die **EINGABETASTE**.  
  
11. Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Aktiviert**, und klicken Sie dann auf **Ändern**.  
  
12. Geben Sie **True**ein und klicken Sie dann auf **OK**.  
  
13. Klicken Sie mit der rechten Maustaste erneut auf den Schlüssel, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
14. Geben Sie **Typ** als Namen der Zeichenfolge ein, und drücken Sie die **EINGABETASTE**.  
  
15. Klicken Sie mit der rechten Maustaste im rechten Bereich auf die neue Zeichenfolge **Typ**, und klicken Sie dann auf **Ändern**.  
  
16. Geben Sie den vollständigen Klassennamen des Anbieters ein, der in der Assembly definiert ist, und klicken Sie dann auf **OK**.  
  
###  <a name="BKMK_RestartService"></a> Starten Sie den Dienst von Windows Server-Domänennamenverwaltung  
 Sie müssen den Windows Server-Dienst für die Domänenverwaltung neu starten, damit der Anbieter dem Betriebssystem zur Verfügung steht.  
  
##### <a name="restart-the-service"></a>Neustarten des Diensts  
  
1.  Click **Start**, type **mmc**, and then press **Enter**.  
  
2.  Wenn das Snap-In "Dienste" in der Konsole nicht aufgeführt wird, fügen Sie es mit den folgenden Schritten hinzu:  
  
    1.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
    2.  Klicken Sie in der Liste **Verfügbare Snap-Ins** auf **Dienste**, und klicken Sie dann auf **Hinzufügen**.  
  
    3.  Stellen Sie im Dialogfeld **Dienste** sicher, dass **lokaler Computer** ausgewählt ist, und klicken Sie dann auf **Fertig stellen**.  
  
    4.  Klicken Sie auf **OK**, um das Dialogfeld **Snap-In hinzufügen/entfernen** zu schließen.  
  
3.  Doppelklicken Sie auf **Dienste**, führen Sie einen Bildlauf nach unten aus, und wählen Sie **Windows Server-Domänenverwaltung**aus. Klicken Sie anschließend auf **Dienst neu starten**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)