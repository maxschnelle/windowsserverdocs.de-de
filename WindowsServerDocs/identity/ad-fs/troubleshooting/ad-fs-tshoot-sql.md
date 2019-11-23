---
title: 'AD FS Problembehandlung: SQL-Konnektivität'
description: In diesem Dokument wird beschrieben, wie verschiedene Aspekte von AD FS behandelt werden.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 09d61292b91c83466f9770184d431b3e6d627dca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385438"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS Problembehandlung: SQL-Konnektivität
AD FS bietet die Möglichkeit, Remote SQL Server für die AD FS Farm Daten zu verwenden.  Es werden Probleme angezeigt, wenn die AD FS Server in der Farm nicht mit den SQL Server-Back-Ends kommunizieren können.  Im folgenden Dokument werden einige grundlegende Schritte zum Testen der Kommunikation mit den Back-End-Servern bereitgestellt.

## <a name="acquire-the-sql-database-connection-string"></a>Abrufen der Verbindungs Zeichenfolge für SQL-Datenbank
Beim Überprüfen der SQL-Konnektivität ist das erste zu testende, wenn AD FS über die richtigen SQL-Verbindungsinformationen verfügt.  Dies kann mithilfe von PowerShell erfolgen.

### <a name="to-acquire-the-sql-connection-string"></a>So erhalten Sie die SQL-Verbindungs Zeichenfolge
1.  Öffnen von Windows PowerShell
2. Geben Sie Folgendes ein: `$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService` und drücken Sie die EINGABETASTE
3. Geben Sie Folgendes ein: `$adfs.ConfigurationDatabaseConnectionString` und drücken Sie die EINGABETASTE.
4. Die Informationen zur Verbindungs Zeichenfolge sollten angezeigt werden.
![](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>Erstellen Sie eine Universal Data Link Datei (UDL), um die Konnektivität zu testen.
Eine Universal Data Link Datei oder eine UDL-Datei ist im Grunde eine Textdatei, die eine Daten bankverbindungs Zeichenfolge enthält.  Mithilfe der Informationen, die wir oben abgerufen haben, können wir testen, ob der SQL Server auf Verbindungen antwortet.

### <a name="to-create-a-udl-file-to-test-connectivity"></a>So erstellen Sie eine UDL-Datei zum Testen der Konnektivität

1. Öffnen Sie Editor, und speichern Sie die Datei als Test. udl.  Stellen Sie sicher, dass **alle Dateien** in der Dropdown-Datei für den **Dateityp "Speichern**unter" ausgewählt sind.
2. Doppelklicken Sie auf "Test. udl".
3. Geben Sie die folgenden Informationen ein: a. **Servernamen auswählen oder eingeben:**  Verwenden Sie die Datenquelle aus der Verbindungs Zeichenfolge oberhalb von b. **Geben Sie Informationen zum Anmelden am Server ein:**  Verwenden Sie das AD FS-Dienst Konto oder ein Konto, das über Berechtigungen zum Remote anmelden verfügt.  Wenn es sich bei dem Konto um ein Windows-Konto handelt, verwenden Sie die integrierte Authentifizierung.
    c. **Wählen Sie die Datenbank auf dem Server aus:** Verwenden Sie den Anfangs Katalog aus der obigen Zeichenfolge.  Beispiel: AdfsConfigurationV3.
   ![Verbindung testen](media/ad-fs-tshoot-sql/sql4.png)
1. Klicken Sie auf **Verbindung testen**.</br>
![Erfolg](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>Verwenden von SQL Server Management Studio zum Testen der Konnektivität
Sie können SSMS auch [herunterladen](https://go.microsoft.com/fwlink/?linkid=864329) und installieren, um die Datenbankkonnektivität zu testen.

### <a name="to-test-connectivity-with-ssms"></a>So testen Sie die Konnektivität mit SSMS
1. SQL Server Management Studio herunterladen und installieren.
![Installieren](media/ad-fs-tshoot-sql/sql5.png)
1. Öffnen Sie SSMS, und geben Sie den Server Namen ein.  Die oben angegebene Datenquelle.
2. Verwenden Sie das AD FS-Dienst Konto oder ein Konto, das über Berechtigungen zum Remote anmelden verfügt.  Wenn es sich bei dem Konto um ein Windows-Konto handelt, verwenden Sie die integrierte Authentifizierung.
![Connect](media/ad-fs-tshoot-sql/sql6.png)
1. Es sollte angezeigt werden, dass die linke Seite aufgefüllt ist.  Erweitern Sie Datenbanken, und vergewissern Sie sich, dass die AD FS Datenbanken angezeigt werden
![AD FS-Datenbanken](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)