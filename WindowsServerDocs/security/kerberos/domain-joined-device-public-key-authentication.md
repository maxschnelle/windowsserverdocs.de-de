---
title: Public Key Authentication für Geräte in einer Domäne
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 80906e7cfe3740200938704a4b4eaf0759af303a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885031"
---
# <a name="domain-joined-device-public-key-authentication"></a>Public Key Authentication für Geräte in einer Domäne

>Gilt für: WindowsServer 2016, Windows 10

Kerberos-Unterstützung für die Domäne eingebundene Geräte für die Anmeldung mit einem Zertifikat Anfang mit Windows Server 2012 und Windows 8. Diese Änderung ermöglicht 3. Anbietern zum Erstellen von Lösungen für das Bereitstellen und initialisieren Zertifikate für die Domäne eingebundene Geräte für die Domänenauthentifizierung verwenden. 

## <a name="automatic-public-key-provisioning"></a>Automatische public Key-Bereitstellung

Ab Windows 10 Version 1507 und Windows Server 2016 können bereitstellen Domäne eingebundene Geräte automatisch einen gebundenen öffentlichen Schlüssel zu einem Windows Server 2016-Domänencontroller (DC). Nachdem ein Schlüssel, bereitgestellt wurde und klicken Sie dann Windows Authentifizierung mit öffentlichem Schlüssel mit der Domäne verwenden können.

### <a name="public-key-generation"></a>Erstellung von öffentlichen Schlüsseln
Wenn das Gerät Credential Guard ausgeführt wird, wird ein öffentlicher Schlüssel erstellt durch Credential Guard geschützt sind. 

Wenn Sie Credential Guard ist nicht verfügbar, und ein TPM ist, und klicken Sie dann ein öffentlicher Schlüssel geschützten, durch das TPM erstellt wird. 

Wenn keiner verfügbar ist, klicken Sie dann ein Schlüssel wird nicht generiert, und Authentifizieren des Geräts kann nur mit Kennwort.

### <a name="provisioning-computer-account-public-key"></a>Bereitstellen von öffentlichen Computer-kontoschlüssel
Wenn Windows wird gestartet, überprüft, ob Sie ein öffentlicher Schlüssel für das Computerkonto bereitgestellt wird. Wenn dies nicht der Fall, klicken Sie dann einen gebundenen öffentlichen Schlüssel generiert und in Active Directory mit einem Windows Server 2016 oder höher Domänencontroller für sein Konto konfiguriert. Wenn allen DC abwärtskompatible sind, ist kein Schlüssel bereitgestellt.

### <a name="configuring-device-to-only-use-public-key"></a>Konfigurieren des Geräts nur die öffentlichen Schlüssel verwenden
Wenn die gruppenrichtlinieneinstellung **Unterstützung für die Geräteauthentifizierung mit Zertifikat** nastaven NA hodnotu **erzwingen**, und klicken Sie dann das Gerät muss einen Domänencontroller zu suchen, die die Ausführung von Windows Server 2016 oder höher zu authentifizieren. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

### <a name="configuring-device-to-only-use-password"></a>Gerät nur das Kennwort konfigurieren
Wenn die gruppenrichtlinieneinstellung **Unterstützung für die Geräteauthentifizierung mit Zertifikat** deaktiviert ist, und klicken Sie dann das Kennwort immer verwendet wird. Die Einstellung befindet sich unter Administrative Vorlagen > System > Kerberos.

## <a name="domain-joined-device-authentication-using-public-key"></a>Zur Domäne gehörenden Geräteauthentifizierung mit öffentlichen Schlüssel
Wenn Windows ein Zertifikat für die Domäne eingebundenes Gerät besitzt, mit dem Zertifikat zuerst Kerberos authentifiziert und auf Fehler bei Wiederholungen mit dem Kennwort. Dadurch wird das Gerät älteren DCs zu authentifizieren.

Da der automatisch bereitgestellten öffentlichen Schlüssel ein selbstsigniertes Zertifikats verfügen, bei der zertifikatsvalidierung auf Domänencontrollern, die kontozuordnung Schlüsselbasierte Vertrauensstellung nicht unterstützen. Standardmäßig startet Windows-Authentifizierung mithilfe des Geräts Domänenkennwort.


