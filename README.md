# Redhat Linux 9 (Upgrade from Redhat 8)

## Agenda 

  1. appstream /flatpak 
     * [Overview / Exercise appstream](application_streams/overview.md)
     * [Overview Flatpak](flatpak/overview.md)

  1. Redhat Alternativen
     * [Überblick](distros/overview-in-comparison-to-rhel-9.md)
    
  1. Redhat 9 - New Features
     * [Redhat 9 - LivePatching Kernel - now in WebConsole](feature/live-patching-kernel-in-webconsole/overview.md)
     * [Redhat container tools - new streams](feature/redhat-container-tools/overview.md)
     * [Rootless Container, now supported](feature/redhat-container-tools/rootless-containers/overview.md)
     * [rpm - default compression zstd](feature/rpm-zstd/overview.md)

  1. Redhat 9 - Container Tools
     * [Redhat 9 - container tools ](feature/redhat-container-tools/overview.md)
  
  1. Changes Filesystem
     * [xfs - changes](feature/filesystems-xfs/bigtime-inobtcount.md)
     * [scp now uses sftp - protocol](feature/scp-over-sftp.md)
    
  1. Changes Network / Security 
     * [iptables vs. nftables - What has changed](network-security/iptables-to-nftables/overview.md)
     * [iptables vs. nftables - migrate](network-security/iptables-to-nftables/migrate.md)
     * [Network Profiles keyfile format](network/profiles/keyfile-format-overview.md)

  1. Network
     * [eBPF & tools](/network/ebpf/overview.md)
     * [MultiPath TCP](/network/mptcp/overview.md)

  1. Future / Network
     * [systemd-networkd / .network units](network/systemd-networkd/overview.md
)
  1. Security
     * [Deprecated signing with sha1](security/sha1-deprecated.md)
     * [systemweite Krypto](security/system-wide-cryptographic-policy.md)
     * [facpolicyd](security/fapolicyd/overview.md)
    
  1. Security (SELinux)
      * [Changes selinux in RHEL9](security/selinux.md)
      * [Troubleshooting Ports with selinux](security/selinux-troubleshooting-centos.md)
      * [Troubleshotting Files selinux](/security/selinux-files.md)
  
  1. Upgrade from RHEL 8 to RHEL 9
     * [in place upgrade RHEL8->9](upgrade/in-place/step-by-step.md)
     
  1. Containers / Automation
     * [Using docker-compose in RHEL 9](automation-containers/docker-compose-on-rhel9.md)
     * [Capabilities with Ansible/Podman](automation-containers/rhel-system-role/01-podman-ansible.md)
     * [Example alpine with dropped capabilities](automation-containers/rhel-system-role/02-ansible-podman-capabilities.md)
    
  1. Tipps & Tricks 
     *  [Ins System reinkommen ohne Passwort und Änderungen vornehmen](tipps-tricks/init-bash.md)
    
  1. Anbindung an AD-Server 
     * [Anbindung an AD-SErver](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/integrating_rhel_systems_directly_with_windows_active_directory/connecting-rhel-systems-directly-to-ad-using-sssd_integrating-rhel-systems-directly-with-active-directory#using-posix-attributes-defined-in-active-directory_connecting-directly-to-ad)

## Backlog 

  1. Distributionen 
     * [Überblick](overview-distros.md)
  1. Verzeichnisse und Dateitypen 
     * [Verzeichnisaufbau](verzeichnisaufbau.md)
     * [Dateitypen](dateitypen.md) 
  1. Basisbefehle
     * [In den Root-Benutzer wechseln](sudo.md)  
     * [Wo bin ich ?](pwd.md)
     * [Praktische Ausgabe von langen Seiten - less](less.md) 
     * [Datei anlegen - touch](touch.md)
     * [Autovervollständen * und tab](autocomplete.md) 
     * [Welches Programm wird verwendet](which.md)
  1. Erweiterte Befehle (Nice to have) 
     * [Alias Befehle anzeigen](alias.md)
     * [Welche Bibliotheken verwendet ein ausführbares Programm](ldd.md)
     * [Ist ein Befehl extern, alias oder intern](type.mdd) 

  1. Dateien und Verzeichnisse
     * [Mit cd im System navigieren](cd.md)
     * [Verzeichnisse in Listenansicht mit versteckten Dateien anzeigen -> ls -la](list.md)
     * [Inhalt in Datei schreiben und anhängen](file-write-append.md)
     * [Verzeichnisse anlegen](mkdir.md)
     * [Verzeichnisse und Dateien löschen](file-dir-delete.md)
     * [Kopieren/Verschieben/Umbenennen von Dateien und Files](file-rename-copy-mv.md) 
     * [Arbeiten mit vi](vi.md)
  
  1. Dateimanipulation/Unix Tools
     * [Anfang oder Ende einer Datei/Ausgabe anzeigen](head-tail.md)
     * [cat/head/tail-Beginn/Ende einer Datei anzeigen](cat-head.md)
     * [zcat - Inhalte einer mit gzip komprimierten Datei anzeigen](zcat.md)
     * [wc - Zeilen zählen](wc.md)
     * [Bestimmte Zeilen aus Datei anzeigen - grep](grep.md)
     * [Erweiterte Suche mit Grep](grep-extended.md)
     * [Finden von files nach Kriterien - find](find.md)
  
  1. Prozesse 
     * [Prozesse anzeigen - ps/pstree -p](prozesse.md)
     * [Alle Prozesse eines Dienstes anzeigen](prozesse-dienst.md)

  1. Benutzer, Gruppen und Rechte 
     * [Rechte](rechte.md) 
     * [Dateien für Benutzer und Gruppen](files-users-groups.md) 
     * [Benutzer anlegen](create-users.md) 
     * [sudo Benutzer erstellen](mod-user-sudo.md) 
  
  1. Logs/Loganalyse
     * [Logfile beobachten](tailf.md)
     * [Dienste debuggen](debug-service.md)
     * [Rsyslog](rsyslog.md)
     * [Journal analysieren](journalctl.md) 
  1. Variablen
     * [Setzen und verwenden von Variablen](variables.md) 
  1. Dienste/Runlevel(Targets verwalten) 
     * [Die wichtigsten systemctl/service](systemctl-service.md)
     * [Systemctl - timers](systemctl-timers.md)
     * [Gegenüberstellung service etc/init.d/ systemctl](service-initd-systemctl.md)
     * [Default Editor systemctl setzen](default-editor-systemctl.md) 

  1. Systemd 
     * [Die wichtigen Tools für die Kommandozeile (ctl)](systemd-cli-tools.md)

  1. Firewall
     * [Arbeiten mit firewalld](firewalld.md)

  1. Systemadministration 
     * [Hostname setzen/abfragen](hostnamectl.md) 
     * [ssh absichern](ssh-absichern.md)

  1. Partitionierung und Filesystem
     * [parted and mkfs.ext4](parted-mkfs.md)
  1. Boot-Prozess und Kernel 
     * [Grub konfigurieren](grub.md)
     * [Kernel-Version anzeigen](kernel-version.md) 
     * [Kernel-Module laden/entladen/zeigen](kernel-modules.md) 
  1. Hilfe 
     * [Hilfe zu Befehlen](help.md)
  1. Grafische Oberfläche und Installation 
     * [X-Server - Ausgabe auf Windows umleiten](xserver-windows-client.md)
     * [Installations-Images-Server](https://ubuntu.com/download/server#download) 
  1. Wartung und Aktualisierung
     * [Aktualisierung des Systems](update-upgrade.md)
     * [Paketmanager yum](yum.md)
     * [Archive runterladen und entpacken](tar-download.md)
     * [Apache installieren (firewall und )](apache-installieren--firewalld.md) 
  1. Firewall und ports
     * [firewalld](firewalld.md)
     * [Scannen und Überprüfen mit telnet/nmap](nmap-telnet.md)
  1. Netzwerk/Dienste 
     * [IP-Adresse von DHCP-Server holen (quick-and-dirty)](dhclient.md) 
     * [Auf welchen Ports lauscht mein Server](lsof.md) 
     * [Interface mit nmtu-edit verwalten - schneller Weg](nmtui-edit.md)
     * [Netzwerkinterface auf der Kommandozeile einrichten](nmcli.md) 
     * [Scannen mit nmap](nmap.md)
  1. Podman 
     * [Podman Walkthrough](podman.md) 
  1. SELinux (Linux härten)
     * [SELinux](selinux.md)
  1. Tools/Verschiedens 
     * [Remote Desktop für Linux / durch Teilnehmer getestet](https://wiki.ubuntuusers.de/Remmina/)
     * [Warum umask 002 und 0002 ? - Geschichte](umask-002-022-why.md)
     * [lokale Mails installieren](local-mail.md)
  1. Bash/Bash-Scripting 
     * [Einfaches Script zur Datumsausgabe](script-date.md) 
     * [Ausführen/Verketten von mehreren Befehlen](multiple-commands.md)
     * [Example with date and if](01-date-if.md)
     * [Example with function and return value](02-function-return-value.md)
     * [Example with test and if](03-if.md)
     * [Example log function](04-log-function.md)
     * [Example Parameter auslesen](05-parameter-auslesen.md)
  1. Timers/cronjobs 
     * [Cronjob - hourly einrichten](cronjob-hourly.md)
     * [cronjob (zentral) - crond](crond.md) 
  1. Literatur 
     * [Literatur](literatur.md) 



