---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: de0313a65234c637018b0c7b2d7a7c9212464077
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938428"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS

## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>Schritt 6: Hinzufügen eines Host \( a \) -und Alias- \( CNAME- \) Ressourceneinsatzes zum Unternehmens-DNS für die Verbunddienst und DRS
Sie müssen die folgenden Ressourcen Einträge dem Unternehmens Domain Name System \( DNS \) für den Verbund Dienst und den Geräte Registrierungsdienst hinzufügen, den Sie in den vorherigen Schritten konfiguriert haben.

|Eingabe|Typ|Adresse|
|---------|--------|-----------|
|Verbund \_ Dienst \_ Name|Host \( A\)|IP-Adresse des AD FS Servers oder die IP-Adresse des Load Balancers, der vor der AD FS Serverfarm konfiguriert ist|
|enterpriseregistration|Alias \( CNAME\)|Verbund \_ Server \_ Name.contoso.com|

Mit dem folgenden Verfahren können Sie dem Unternehmens- \( \) \( \) DNS für den Verbund Server und den Geräte Registrierungsdienst die CNAME-Ressourcen Einträge Host a und Alias hinzufügen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>So fügen Sie einen Host \( a \) -und Alias- \( CNAME- \) Ressourcen Einträge zu DNS für Ihren Verbund Server hinzu

1.  Klicken Sie auf Ihrem Domänen Controller in Server-Manager im **Menü Extras** auf **DNS** , um das DNS-Snap \- in zu öffnen.

2.  Erweitern Sie in der Konsolen Struktur den Knoten **Domänen \_ Controller \_ Name** , erweitern Sie Forward-Lookupzonen, klicken Sie mit der rechten **Forward Lookup Zones** \- Maustaste auf **Domänen \_ Name**, und klicken Sie dann auf **neuer Host \( A oder AAAA \) **.

3.  Geben Sie im Feld **Name** den Namen ein, der für Ihre AD FS Farm verwendet werden soll.

4.  Geben Sie im Feld **IP-Adresse** die IP-Adresse Ihres Verbund Servers ein. Klicken Sie auf **Host hinzufügen**.

5.  \-Klicken Sie mit der rechten Maustaste auf den Knoten **Domänen \_ Name** , und klicken Sie auf **Neuer Alias \( CNAME \) **.

6.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz****enterpriseregistration** in das Feld **Aliasname** ein.

7.  Geben Sie im Feld voll qualifizierter Domänen Name im \( \) Feld Zielhost den ** \_ Namen Federation Service \_ Farm \_ Name. Domain \_ Name.com**ein, und klicken Sie dann auf **OK**.

    > [!IMPORTANT]
    > Wenn Ihr Unternehmen in einer realen Bereitstellung über mehrere \( UPN-Suffixe für den Benutzer Prinzipal Namen verfügt \) , müssen Sie mehrere CNAME-Einträge für jedes dieser UPN-Suffixe in DNS erstellen.

## <a name="see-also"></a>Weitere Informationen

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)

[Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)


