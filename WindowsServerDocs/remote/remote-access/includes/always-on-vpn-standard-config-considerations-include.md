## <a name="standard-configuration-considerations"></a>Überlegungen zur Standard Konfiguration

Always on-VPN verfügt über viele Konfigurationsoptionen. Wenn Sie jedoch Ihre VPN-Konfiguration auswählen, enthalten Sie die folgenden Informationen:

-   **Verbindungstyp.** Die Auswahl des Verbindungs Protokolls ist wichtig und wird letztendlich mit dem verwendeten Authentifizierungstyp einhergehen. Ausführliche Informationen zu den verfügbaren tunnelingprotokollen finden Sie unter [VPN-Verbindungstypen](/windows/security/identity-protection/vpn/vpn-connection-type/).

-   **Routing.** In diesem Kontext legen Routing Regeln fest, ob Benutzer während der Verbindung mit dem VPN andere Netzwerk Routen verwenden können.

    -   Das _getrennte Tunneln_ ermöglicht den gleichzeitigen Zugriff auf andere Netzwerke, z. b. das Internet.

    -   Die _Tunnel Erzwingung_ erfordert, dass der gesamte Datenverkehr ausschließlich über das VPN erfolgt und keinen gleichzeitigen Zugriff auf andere Netzwerke zulässt.

-   **Ängste.** Durch _auslösen_ wird festgelegt, wie und wann eine VPN-Verbindung initiiert wird (z. b. Wenn eine APP geöffnet wird, wenn das Gerät eingeschaltet wird, manuell durch den Benutzer). Informationen zu Triggeroptionen finden Sie in den Optionen für das [automatisch ausgelöste VPN-Profil](/windows/security/identity-protection/vpn/vpn-auto-trigger-profile/).

-   **Geräte-oder Benutzerauthentifizierung.** Always on-VPN verwendet Gerätezertifikate und eine vom Gerät initiierte Verbindung über eine Funktion mit dem Namen " [Geräte Tunnel](../vpn/vpn-device-tunnel-config.md)". Diese Verbindung kann automatisch initiiert werden und ist beständig, ähnlich wie eine DirectAccess-Infrastruktur Tunnelverbindung.

>[!TIP]
>Wenn Sie von DirectAccess zu Always on VPN migrieren möchten, sollten Sie mit den Konfigurationsoptionen beginnen, die mit ihren Funktionen vergleichbar sind, und dann von dort aus erweitern.

Durch die Verwendung von Benutzer Zertifikaten stellt der Always on VPN-Client automatisch eine Verbindung her, jedoch auf Benutzerebene (nach der Benutzeranmeldung) anstelle der Geräteebene (vor der Benutzeranmeldung). Die Benutzeroberflächen sind für den Benutzer weiterhin nahtlos, unterstützen jedoch erweiterte Authentifizierungsmechanismen wie Windows Hello for Business.
