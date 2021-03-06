---
title: Problembehandlung der Windows-Volumenaktivierung
description: Listet Ressourcen auf, die Informationen zu bewährten Methoden für die Volumenaktivierung sowie Informationen zur Problembehandlung bei Aktivierungsproblemen enthalten.
ms.topic: troubleshooting
ms.date: 09/24/2019
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: ce6c2e830e7c30e24112854b54e12909c43fa6f7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972327"
---
# <a name="troubleshooting-windows-volume-activation"></a>Problembehandlung der Windows-Volumenaktivierung

Produktaktivierung ist der Prozess der Softwareüberprüfung nach der Installation auf einem bestimmten Computer. Bei der Aktivierung wird die Echtheit des Produkts bestätigt (dass es keine illegale Kopie ist), und dass der Product Key oder die Seriennummer gültig und nicht beschädigt bzw. gesperrt sind. Bei der Aktivierung wird außerdem eine Verknüpfung oder eine Beziehung zwischen dem Product Key und der Installation erstellt.

Die Volumenaktivierung ist der Prozess des Aktivierens von volumenlizenzierten Produkten. Eine Organisation, die Volumenlizenzierungskunde werden möchte, muss einen Volumenlizenzvertrag mit Microsoft abschließen. Microsoft bietet angepasste Volumenlizenzierungsprogramme, die die Größe und Einkaufspräferenzen der Organisation berücksichtigen. Weitere Informationen findest du im [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).

Das [Windows Server 2016-Aktivierungshandbuch](server-2016-activation.md) konzentriert sich auf die KMS-Aktivierungstechnologie (Key Management Service, Schlüsselverwaltungsdienst). In diesem Abschnitt werden häufige Probleme behandelt und Richtlinien zur Problembehandlung für KMS und verschiedene andere Volumenaktivierungstechnologien bereitgestellt.

## <a name="best-practices-for-volume-activation"></a>Bewährte Methoden für die Volumenaktivierung

Die folgenden Artikel bieten technische Informationen und bewährte Methoden für die Volumenaktivierungstechnologien von Microsoft.

### <a name="key-management-service-kms"></a>Schlüsselverwaltungsdienst (Key Management Service, KMS)

- [Planen für die Volumenaktivierung](/windows/deployment/volume-activation/plan-for-volume-activation-client)
- [Grundlegendes zu KMS](/previous-versions/tn-archive/ff793434(v=technet.10))
- [Bereitstellen der KMS-Aktivierung](/previous-versions/tn-archive/ff793409%28v=technet.10%29)
- [Konfigurieren von KMS-Hosts](/previous-versions/tn-archive/ff793407%28v%3dtechnet.10%29)
- [Konfigurieren des DNS](/previous-versions/tn-archive/ff793405%28v%3dtechnet.10%29)
- [Aktivierung mittels Schlüsselverwaltungsdienst](/windows/deployment/volume-activation/activate-using-key-management-service-vamt)

### <a name="active-directory-based-activation-adba"></a>Active Directory-basierte Aktivierung (ADBA)

- [Bereitstellen der Active Directory-basierte Aktivierung](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn502534%28v%3dws.11%29)
- [Aktivierung mittels Active Directory-basierter Aktivierung](/windows/deployment/volume-activation/activate-using-active-directory-based-activation-client)
- [Übersicht über die Active Directory-basierte Aktivierung](/windows/deployment/volume-activation/active-directory-based-activation-overview)

### <a name="multiple-activation-key-mak-activation"></a>MAK-Aktivierung (Multiple Activation Key, Mehrfachaktivierungsschlüssel)

- [Verwenden der MAK-Aktivierung](/previous-versions/tn-archive/ff793438%28v=technet.10%29)
- [Grundlegendes zur MAK-Aktivierung](/previous-versions/tn-archive/ff793435%28v%3dtechnet.10%29)
- [Aktivieren von MAK-Clients](/previous-versions/tn-archive/ff793398%28v%3dtechnet.10%29)

### <a name="subscription-activation"></a>Abonnementaktivierung

- [Windows 10-Abonnementaktivierung](/windows/deployment/windows-10-subscription-activation)
- [Bereitstellen von Windows 10 Enterprise-Lizenzen](/windows/deployment/deploy-enterprise-licenses)
- [Windows 10 Enterprise E3 in CSP](/windows/deployment/windows-10-enterprise-e3-overview)

## <a name="resources-for-troubleshooting-activation-issues"></a>Ressourcen zur Problembehandlung von Aktivierungsproblemen

Die folgenden Artikel enthalten Richtlinien und Informationen zu Tools für die Behandlung von Problemen mit der Volumenaktivierung:

- [Richtlinien für die Problembehandlung des Schlüsselverwaltungsdiensts (KMS)](activation-troubleshoot-kms-general.md)
- [„Slmgr.vbs“-Optionen für das Abrufen von Informationen zur Volumenaktivierung](activation-slmgr-vbs-options.md)
- [Beispiel: Problembehandlung von ADBA-Clients, die sich nicht aktivieren lassen](activation-troubleshoot-adba-clients.md)

In den folgenden Artikeln findest du Anleitungen zur Behebung spezifischerer Aktivierungsprobleme:

- [Auflösen von gängigen Aktivierungsfehlercodes](activation-error-codes.md)
- [KMS-Aktivierung: bekannte Probleme](activation-troubleshoot-KMS-issues.md)
- [MAK-Aktivierung: bekannte Probleme](activation-troubleshoot-MAK-issues.md)
- [Richtlinien für die Problembehandlung von Aktivierungsproblemen im Zusammenhang mit DNS](common-troubleshooting-procedures-kms-dns.md)
- [Neuerstellen der Datei „Tokens.dat“](activation-rebuild-tokens-dat-file.md)
