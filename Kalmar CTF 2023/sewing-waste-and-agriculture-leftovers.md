#C1 :
1. Follow UDP stream 
2. Dựa Theo số cột để lấy flag
3. ![image](https://user-images.githubusercontent.com/94669750/223003255-9a412f59-a002-408c-a612-316aab1cd23f.png)

#C2 :
+ Dựa vào thư viện scapy 

```from scapy.all import *

packets = rdpcap('swaal.pcap')

udp_data = b''.join(pkt.load for pkt in packets)

segments = udp_data.split(b'\n')

flag = {}

for s in segments:

    pattern = re.compile(rb'[a-z0-9}{_]')
    matches = pattern.finditer(s)

    for m in matches:
        #flag[m.start()] = m.group()

flag = dict(sorted(flag.items())).values()

print(b''.join(flag).decode())
```

![image](https://user-images.githubusercontent.com/94669750/223004427-b7cbebb5-5f4f-46c2-ac5f-b23806793fcf.png)
