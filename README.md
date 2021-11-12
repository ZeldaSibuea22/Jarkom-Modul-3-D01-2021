# Jarkom-Modul-3-D01-2021-
Soal : https://docs.google.com/document/d/1hwuI5YpxiP-aboS7wGWPbaQeSOQl0HHVHLT3ws2BPUk/edit

<img src="img/Topologi.PNG">

Prefix kelompok D01: `192.192`

Untuk menyambungkan ke internet, jangan lupa:
- Lakukan perintah berikut di router (Foosha)
  ```
  iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.192.0.0/16
  ```
- Samakan nameserver router (Foosha) ke node yang ingin disambungkan dengan internet
  ```
  echo nameserver 192.168.122.1 > /etc/resolv.conf
  ```

### Konfigurasi Network


## Soal 1
Konfigurasi EniesLobby sebagai DNS Server, Jipangu sebagai DHCP Server, Water7 sebagai Proxy Server

### EniesLobby sebagai DNS Server
Dengan melakukan instalasi berikut yang akan digunakan sebagai DNS Server
```Shell
apt-get update
apt-get install bind9 -y
apt-get install dnsutils -y
```

### Jipangu sebagai DHCP Server
Lakukan instalasi berikut yang akan digunakan sebagai DHCP Server
```Shell
apt-get update
apt-get install isc-dhcp-server -y
```
Menentukan interface di file `/etc/default/isc-dhcp-server`. Pada bagian `INTERFACES=` isi dengan interface yang akan diberi layanan DHCP (sebagai klien DHCP).
Pada kasus ini, yang menjadi klien DHCP adalah Switch1 dan Switch3 melalui eth0 milik Jipangu.
```
INTERFACES="eth0"
```
<img src="img/soal1_testing.PNG">

**Konfigurasi selanjutnya merupakan bagian jawaban soal selanjutnya**

### Water7 sebagai Proxy Server
Lakukan instalasi berikut yang dibutuhkan oleh Proxy Server
```
apt-get update
apt-get install squid -y
apt-get install apache2-utils -y
```
Cek status squid apakah berjalan dengan baik menggunakan command `service squid status`.

Lakukan konfigurasi squid dengan melakukan back-up file konfigurasi default squid.
```
mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
```
Buat konfigurasi squid pada file `/etc/squid/squid.conf` dengan menambahkan script:
```
http_port 8080
visible_hostname Water7
```
<img src="img/soal1_testing1.PNG">

Kemudian restart squid dengan perintah `service squid restart`.
