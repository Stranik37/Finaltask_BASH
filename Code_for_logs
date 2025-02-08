#!/bin/bash

cat <<EOL > access.log
192.168.1.1 - - [28/Jul/2024:12:34:56 +0000] "GET /index.html HTTP/1.1" 200 1234
192.168.1.2 - - [28/Jul/2024:12:35:56 +0000] "POST /login HTTP/1.1" 200 567
192.168.1.3 - - [28/Jul/2024:12:36:56 +0000] "GET /home HTTP/1.1" 404 890
192.168.1.1 - - [28/Jul/2024:12:37:56 +0000] "GET /index.html HTTP/1.1" 200 1234
192.168.1.4 - - [28/Jul/2024:12:38:56 +0000] "GET /about HTTP/1.1" 200 432
192.168.1.2 - - [28/Jul/2024:12:39:56 +0000] "GET /index.html HTTP/1.1" 200 1234
EOL

echo "Отчет о логе веб-сервера" | tee report.txt
echo "=========================" | tee -a report.txt

echo -e "\nОбщее количество запросов:" | tee -a report.txt
total_requests=0
for line in $(cat access.log); do
    total_requests=$((total_requests + 1))
done

total_requests=$(wc -l < access.log)
echo "$total_requests" | tee -a report.txt

echo -e "\nКоличество уникальных IP-адресов:" | tee -a report.txt
unique_ips=$(awk '{print $1}' access.log | sort | uniq | wc -l)
echo "$unique_ips" | tee -a report.txt

echo -e "\nКоличество запросов по методам:" | tee -a report.txt
awk 'BEGIN{count_post=0; count_get=0} {if ($6 == "\"GET") {count_get++;} else if ($6 == "\"POST") {count_post++;}} END {print "Количество GET:" count_get; print "Количество POST:" count_post;}' access.log | tee>
echo -e "\nСамый популярный URL:" | tee -a report.txt
awk '{start = index($0, "GET"); if (start > 0) {url_start = start + 4; url_end = index(substr($0, url_start), " "); if (url_end > 0) {url = substr($0, url_start, url_end); } else {url = substr($0, url_start);}c>

echo -e "\nОтчет сохранен в файл report.txt"
