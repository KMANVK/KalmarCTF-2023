+ Hiểu rõ bản chất của FTP passvie mode 
+ Follow tcp stream 
+ Dùng tshark để trích xuất dữ liệu săp xếp nó theo thứ tự CWD :

***seq 0 78 | xargs -Iz bash -c "tshark -r cards.pcap -Y 'tcp.stream==z && frame matches \"CWD|Transfer|Opening\"' -Tfields -e frame.number -e ftp.request.arg" | xargs -n4 bash -c 'echo $1; tshark -r cards.pcap -Y "frame.number in {$2..$3} and data" -Tfields -e data | head -1' | xargs -n2 | sort -n | awk '{print $2}' | xxd -r -p***

=> decode characters để nhận flag 

#kalmar{shuffle_shuff1e_can_you_k33p_tr4ck_of_where_th3_cards_are_shuffl3d_n0w}

# Lưu ý : chỉ sử dụng với phiên bản mới nhất của wireshark 
