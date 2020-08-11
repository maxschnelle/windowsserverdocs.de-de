---
title: Erstellen virtueller Computer für Remotedesktop
description: Hier erfährst du, wie du virtuelle Computer erstellst, um Remotedesktopkomponenten in der Cloud zu hosten.
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b0f62d6f-0915-44ca-afef-be44a922e20e
author: lizap
manager: dongill
ms.openlocfilehash: 864b1a0fda39570a94007108e816c7a9b2cddd51
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939691"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>Erstellen virtueller Computer für Remotedesktop

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Führe die folgenden Schritte aus, um in der Mandantenumgebung die virtuellen Computer zu erstellen, auf denen die für eine Desktophostingbereitstellung benötigten Rollen, Dienste und Features von Windows Server 2016 ausgeführt werden.

In dieser einfachen exemplarischen Bereitstellung wird die erforderliche Mindestanzahl von drei virtuellen Computern erstellt. Der erste virtuelle Computer hostet die Rollendienste „Remotedesktop-Verbindungsbroker“ und „Remotedesktop-Lizenzserver“ sowie eine Dateifreigabe für die Bereitstellung. Der zweite virtuelle Computer hostet die Rollendienste „Remotedesktop-Gateway“ und „Web Access für Remotedesktop“.  Der dritte virtuelle Computer hostet den Rollendienst „Remotedesktop-Sitzungshost“. Bei sehr kleinen Bereitstellungen kannst du zur Verringerung der VM-Kosten den AAD-App-Proxy verwenden, um alle öffentlichen Endpunkte aus der Bereitstellung zu entfernen, sowie alle Rollendienste auf einem einzelnen virtuellen Computer zusammenfassen. Bei größeren Bereitstellungen kannst du die verschiedenen Rollendienste auf einzelnen virtuellen Computern installieren, um eine bessere Skalierung zu ermöglichen.

In diesem Abschnitt werden die Schritte beschrieben, die ausgeführt werden müssen, um virtuelle Computer für die einzelnen Rollen auf der Grundlage von Windows Server-Images aus dem [Microsoft Azure Marketplace](https://azure.microsoft.com/marketplace/) bereitzustellen. Wenn du virtuelle Computer auf der Grundlage eines benutzerdefinierten Images erstellen möchtest, musst du PowerShell verwenden. Weitere Informationen hierzu findest du unter [Schnellstart: Erstellen eines virtuellen Windows-Computers in Azure mit PowerShell](/azure/virtual-machines/windows/quick-create-powershell). Kehre anschließend wieder hierher zurück, um Azure-Datenträger für die Dateifreigabe anzufügen und eine externe URL für deine Bereitstellung einzugeben.

1. [Erstelle virtuelle Windows-Computer](/azure/virtual-machines/windows/quick-create-portal), um den RD-Verbindungsbroker, den RD-Lizenzserver und den Dateiserver zu hosten.

   In unserem Beispiel haben wir folgende Benennungskonventionen verwendet:
   - RD-Verbindungsbroker, Lizenzserver und Dateiserver:
       - Virtueller Computer: Contoso-Cb1
       - Verfügbarkeitsgruppe: CbAvSet
   - Web Access für RD und RD-Gatewayserver:
       - Virtueller Computer: Contoso-WebGw1
       - Verfügbarkeitsgruppe: WebGwAvSet

   - RD-Sitzungshost:
       - Virtueller Computer: Contoso-Sh1
       - Verfügbarkeitsgruppe: ShAvSet

   Jeder virtuelle Computer verwendet die gleiche Ressourcengruppe.
2. Erstelle einen Azure-Datenträger für die UPD-Freigabe (User Profile Disk, Benutzerprofil-Datenträger):
   1.  Klicke im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicke auf die Ressourcengruppe für die Bereitstellung, und klicke anschließend auf den virtuellen Computer, der für den RD-Verbindungsbroker erstellt wurde (Beispiel: Contoso-Cb1).
   2.  Klicke auf **Einstellungen > Datenträger > Neuen anfügen**.
   3.  Übernimm die Standardwerte für Name und Typ.
   4.  Gib eine Größe (in GB) ein, die ausreicht, um Netzwerkfreigaben für die Mandantenumgebung aufzunehmen (einschließlich Benutzerprofil-Datenträger und Zertifikate). Für jeden geplanten Benutzer werden ca. 5 GB benötigt.
   5.  Übernimm die Standardwerte für Speicherort und Hostzwischenspeicherung, und klicke auf **OK**.
3. Erstelle einen externen Lastenausgleich für den externen Zugriff auf die Bereitstellung:
   1. Klicke im Azure-Portal auf **Durchsuchen > Lastenausgleichsmodule** und anschließend auf **Hinzufügen**.
   2. Gib unter **Name** einen Namen ein, wähle unter **Typ** den Lastenausgleichstyp **Öffentlich** aus, und wähle **Abonnement**,  **Ressourcengruppe** und **Standort** aus.
   3. Wähle **Öffentliche IP-Adresse auswählen** > **Neu erstellen** aus, gib einen Namen ein, und wähle **OK** aus.
   4. Wähle **Erstellen** aus, um den Lastenausgleich zu erstellen.
4. Konfigurieren des externen Lastenausgleichs für deine Bereitstellung
   1. Klicke im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicke auf die Ressourcengruppe für die Bereitstellung, und klicke anschließend auf den Lastenausgleich, den du für die Bereitstellung erstellt hast.
   2. Füge für den Lastenausgleich einen Back-End-Pool hinzu, an den Datenverkehr gesendet werden kann:
       1. Wähle **Back-End-Pool** > **Hinzufügen** aus.
       2. Gib unter **Name** einen Namen ein, und wähle **\+ Virtuellen Computer hinzufügen** aus.
       3. Wähle **Verfügbarkeitsgruppe** > **WebGwAvSet** aus.
       4. Wähle **Virtuelle Computer** > **Contoso-WebGw1** > **Auswählen** > **OK** > **OK** aus.
   3. Füge einen Test hinzu, damit der Lastenausgleich weiß, welche Computer aktiv sind:
       1. Wähle **Tests** > **Hinzufügen** aus.
       2. Gib unter **Name** einen Namen ein (beispielsweise „HTTPS“), wähle **TCP** aus, gib unter **Port** den Wert „443“ ein, und wähle anschließend **OK** aus.
   4. Gib Lastenausgleichsregeln für die Verteilung des eingehenden Datenverkehrs ein:
      1. Wähle **Lastenausgleichsregeln** > **Hinzufügen** aus.
      2. Gib unter **Name** einen Namen ein (beispielsweise „HTTPS“), wähle **TCP** aus, und gib sowohl für **Port** als auch für **Back-End-Port** den Wert „443“ ein.
          - Behalte bei einer Windows 10- oder Windows Server 2016-Bereitstellung unter **Sitzungspersistenz** den Wert **Keine** bei, oder wähle andernfalls **Client-IP** aus.
      3. Wähle **OK** aus, um die HTTPS-Regel zu akzeptieren.
      4. Wähle **Hinzufügen** aus, um eine neue Regel zu erstellen.
      5. Gib unter **Name** einen Namen ein (beispielsweise „UDP“), wähle **UDP** aus, und gib sowohl für <strong>Port</strong> als auch für **Back-End-Port** den Wert „3391“ ein.
          - Behalte bei einer Windows 10- oder Windows Server 2016-Bereitstellung unter **Sitzungspersistenz** den Wert **Keine** bei, oder wähle andernfalls **Client-IP** aus.
      6. Wähle **OK** aus, um die UDP-Regel zu akzeptieren.
   5. Gib eine NAT-Regel für eingehenden Datenverkehr ein, um eine direkte Verbindung mit „Contoso-WebGw1“ herzustellen.
       1. Wähle **NAT-Regeln für eingehenden Datenverkehr** > **Hinzufügen** aus.
       2. Gib unter **Name** einen Namen ein (beispielsweise „RDP-Contoso-WebGw1“), wähle für den Dienst die Option **Benutzerdefiniert** und für das Protokoll die Option **TCP** aus, und gib für **Port** den Wert „14000“ ein.
       3. Wähle **Virtuellen Computer auswählen** > „Contoso-WebGw1“ aus.
       4. Wähle für die Portzuordnung die Option **Benutzerdefiniert** aus, gib für **Zielport** den Wert „3389“ ein, und wähle **OK** aus.
5. Gib eine externe URL/einen DNS-Namen für deine Bereitstellung ein, um extern darauf zugreifen zu können:
   1.  Klicke im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, klicke auf die Ressourcengruppe für die Bereitstellung, und klicke anschließend auf die öffentliche IP-Adresse, die du für Web Access für RD und RD-Gateway erstellt hast.
   2.  Klicke auf **Konfiguration**, gib eine DNS-Namensbezeichnung ein (beispielsweise „contoso“), und klicke anschließend auf **Speichern**. Diese DNS-Namensbezeichnung („contoso.westus.cloudapp.azure.com“) ist der DNS-Name, der für die Verbindungsherstellung mit deinem Server für Web Access für RD und RD-Gateway verwendet wird.
