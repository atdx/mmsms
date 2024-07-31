nano /usr/bin/mmsms.sh
[code]
#!/bin/sh

# Ambil daftar SMS
sms_list=$(mmcli -m 1 --messaging-list-sms | grep '/org/freedesktop/ModemManager1/SMS/' | awk '{print $1}')

# Loop melalui setiap SMS ID dan tampilkan isi pesan
for sms_id in $sms_list; do
    echo "SMS ID: $sms_id"
    mmcli -m 1 -s ${sms_id##*/}
    echo "-------------------------"
done
[/code]
chmod +x /usr/bin/mmsms.sh
echo 'alias mmsms="/usr/bin/mmsms.sh"' >> /etc/profile
source /etc/profile

