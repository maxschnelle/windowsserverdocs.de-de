---
title: MultiPoint Services-Benutzerkonten
description: Erfahren Sie mehr über Benutzerkonten in MultiPoint Services insbesondere die Art, die für verschiedene Szenarien verwendet
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f3c6ce5-9b7c-45a0-83c5-3f9b9f5f48d4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 31279f81d5af597b0b1f1729c953fefaf24a214f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855361"
---
# <a name="example-scenarios-multipoint-services-user-accounts"></a>Beispielszenarien: MultiPoint Services-Benutzerkonten
Was möchten Sie tun, um die Benutzer-Konto-Szenario zu implementieren, das Sie für Ihr MultiPoint Services-Umgebung ausgewählt haben? Die folgenden Tabellen beschreiben die einzelnen Aufgaben zum Konfigurieren von Benutzerkonten und Vorbereiten von Stationen für gemeinsamem oder individuellem Benutzerkonten auf einem eigenständigen MultiPoint-Computer oder Netzwerk-Servern in einer Arbeitsgruppe oder einer Active Directory-Domäne ausführen. Wählen Sie das Szenario, das für Ihre Umgebung gilt. Befolgen Sie dann den Links in der Tabelle, die jede erforderliche Konfiguration für diese Aufgabe aus.  
  
> [!NOTE]  
> Wenn Sie noch nicht so richten Sie Ihre Benutzerkonten entschieden haben, finden Sie unter [Planen von Benutzerkonten für Ihr MultiPoint Services-Umgebung](Plan-user-accounts-for-your-MultiPoint-services-environment.md) für Weitere Informationen zu den Auswirkungen von Benutzern in jede gewählte Variante.  
  
## <a name="single-multipoint-services-computer-in-a-stand-alone-environment-no-network"></a>Einzelne MultiPoint Services-Computer in einer eigenständigen Umgebung (ohne Netzwerk)  
  
|||  
|-|-|  
|**Meine Benutzer müssen sich nicht anmelden.** Die Stationen können für alle Benutzer verfügbar sein, die Ihnen durchläuft. Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen einer einzelnen lokalen Benutzerkontos (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md)<br />3.  [Konfigurieren von Stationen für die automatische Anmeldung](Configure-stations-for-automatic-logon.md)|  
|**Benutzer können alle die gleiche Anmeldung des Benutzers freigeben.** Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen einer einzelnen lokalen Benutzerkontos (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md)|  
|**Benutzer müssen ihre eigenen einzelne Windows-desktop-Erlebnis.**|Erstellen Sie ein lokales Benutzerkonto für jeden Benutzer (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)|  
  
## <a name="multiple-multipoint-services-computers-on-a-network-but-with-no-domain"></a>Mehrere MultiPoint Server-Computer in einem Netzwerk, jedoch ohne Domäne  
  
|||  
|-|-|  
|**Meine Benutzer müssen sich nicht anmelden.** Die Stationen können für alle Benutzer verfügbar sein, die Ihnen durchläuft. Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen Sie ein einzelnes lokales Benutzerkonto auf jedem Server. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md) auf jedem Server<br />3.  [Konfigurieren von Stationen für die automatische Anmeldung](Configure-stations-for-automatic-logon.md) auf jedem Server|  
|**Benutzer können alle die gleiche Anmeldung des Benutzers freigeben.** Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen Sie ein einzelnes lokales Benutzerkonto auf jedem Server. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md) auf jedem Server.|  
|**Benutzer müssen ihre eigenen einzelne Windows-desktop-Erlebnis.**<br /><br />-   **Option A** -Benutzer verwenden immer lokale Stationen, die mit dem gleichen MultiPoint Services-Computer verbunden sind.<br />-   **Option B** -meine Benutzer lokale Stationen auf mehr als eine MultiPoint Services-Computer verwenden.<br />-   **Option C** -Remoteclients meine Benutzer im lokalen Netzwerk verwenden.|-   **Option A** – erstellen Sie ein einzelnes lokales Benutzerkonto auf jedem Server für die Benutzer des Servers. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />-   **Option B** -lokale Benutzerkonten für jeden Benutzer auf jedem Server zu erstellen. **Hinweis**: Dies bedeutet, dass jeder Benutzer ein Profil auf jedem Server hat. Das heißt, wenn sie eine Datei im Ordner Eigene Dateien, während Sie auf Server A-Station angemeldet speichern, wird nicht die Datei angezeigt beim Anmelden bei Server B die Station. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br />-   **Option C** -weisen Sie jedem Benutzer, die einem bestimmten MultiPoint Server-Computer. Erstellen Sie lokale Benutzerkonten für die zugewiesenen Benutzer auf jedem Server. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)|  
  
## <a name="one-or-more-multipoint-services-computers-in-a-domain-network-environment"></a>Eine oder mehrere MultiPoint Server-Computer in einer domänenumgebung-Netzwerk  
  
|||  
|-|-|  
|**Meine Benutzer müssen sich nicht anmelden.** Die Stationen können für alle Benutzer verfügbar sein, die Ihnen durchläuft. Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen Sie ein Domänenkonto ein, sich bei den Servern anzumelden.<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md) auf jedem Server.<br />3.  [Konfigurieren von Stationen für die automatische Anmeldung](Configure-stations-for-automatic-logon.md) auf jedem Server.|  
|**Benutzer können alle die gleiche Anmeldung des Benutzers freigeben.** Sie brauchen keine einzelne Windows-desktop-Erlebnis, die private Ordner zum Speichern von Daten oder personalisierte Desktops umfasst.|1.  Erstellen Sie ein Domänenkonto ein, die für eine Gruppe oder für jeden Benutzer.<br />2.  [Ermöglichen Sie ein Konto, um mehrere Sitzungen](Allow-one-account-to-have-multiple-sessions.md) auf jedem Server.|  
|**Benutzer müssen ihre eigenen einzelne Windows-desktop-Erlebnis.**<br /><br />-   **Option A** : jeder Benutzer mit einem Domänenkonto kann den MultiPoint Services-Computer verwenden.<br />-   **Option B** -beschränken möchte, welche Domänenkonten können auf den Server zugreifen.|-   **Option A** – es ist kein Setup erforderlich. Standardmäßig haben alle Domänenbenutzer Zugriff auf alle MultiPoint Services-Computer, auf das Netzwerk.<br />-   **Option B** -Einschränkung des Zugriffs Domänenbenutzerkonten in der MultiPoint Services-Computer. Anweisungen hierzu finden Sie unter [Beschränken der Benutzerzugriff auf den Server](limit-users--access-to-the-server-in-multipoint-services.md).|  
|**Ich möchte die lokale Benutzerkonten verwenden und verwalten Sie sie getrennt von meiner Domänenkonten.** Z. B. zum Verwalten von MultiPoint Services jedoch nicht der Domäne gelesen werden sollen, oder Sie keine Domänenkonten auf alle MultiPoint Services-Benutzer gewähren möchten.|Erstellen Sie eine oder mehrere lokale Benutzerkonten auf jedem Server. (Anweisungen hierzu finden Sie unter [Erstellen lokaler Benutzerkonten](Create-local-user-accounts.md).)<br /><br />**Hinweis**: Dies bedeutet, dass jedes Benutzerkonto ein Profil auf jedem Server hat. Das heißt, wenn sie eine Datei im Ordner Eigene Dateien, während Sie auf Server A-Station angemeldet speichern, wird nicht die Datei angezeigt beim Anmelden bei Server B die Station.|  