
در اینجا یک راه ساده با استفاده از یک اسکریپت bash و یک حلقه بی‌نهایت برای نظارت بر اجرای داکر آورده شده :
1:ابتدا با دستور زیر یک فایل اسکریپت bash میسازیم و اسمش رو هر چی میخواید بذارید

nano restart_docker.sh 
2:کد زیر را درون فایل قرار بدید:

#!/bin/bash

while true; do
    if ! docker ps | grep -q 'nillion/retailtoken-accuser:v1.0.1'; then
        echo "Container stopped. Restarting..."
        docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.1 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start 5664031
    fi
    sleep 100 # 
done
برای ذخیره کردن و خروج از nano، کلید‌های Ctrl + O و سپس Ctrl + X و اینتر را فشار دهید.

نکته من کد مرحله ی 7 خودم رو قرار دادم اگه کد شما فرق میکنه اون قسمت رو عوض کنید

سپس دستور زیر رو اجرا کنید


chmod +x restart_docker.sh
./restart_docker.sh
