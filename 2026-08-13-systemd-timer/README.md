# Zadanie domowe 13.08 - unit systemd (timer)

Tresc zadania (Slack, Patryk Trautberg): stworzyc unit systemd ktory bedzie odpalal skrypt raportu systemowego codziennie o 06:00 i 18:00.

## Pliki

- system-report.sh - skrypt raportu (== START/FILESYSTEM/MEMORY/TOP 10 CPU/END)
- system-report.service - jednostka typu oneshot uruchamiajaca skrypt
- system-report.timer - timer z OnCalendar=*-*-* 06,18:00:00, Persistent=true

## Instalacja na docelowej maszynie

sudo cp system-report.sh /usr/local/bin/system-report.sh
sudo chmod +x /usr/local/bin/system-report.sh
sudo cp system-report.service system-report.timer /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now system-report.timer

## Weryfikacja

systemctl list-timers system-report.timer
sudo journalctl -u system-report.service
