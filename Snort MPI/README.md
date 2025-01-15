## 1. Update Sistem
    sudo apt update
    sudo apt upgrade

## 2. Install Depedencies
    sudo apt install -y build-essential libpcap-dev libpcre3-dev libdumbnet-dev bison flex zlib1g-dev

## 3. Download DAQ, Ekstrak, dan Install
    wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz
    tar -xvzf daq-2.0.7.tar.gz
    cd daq-2.0.7
    ./configure
    make
    sudo make install

## 4. Download Snort (Manual)
    wget https://www.snort.org/downloads/snort/snort-2.9.20.tar.gz

## 5. Ekstrak Snort
    tar -xvzf snort-2.9.20.tar.gz

#### Tambahan Instalasi
    wget http://luajit.org/download/LuaJIT-2.0.5.tar.gz
    tar -xvzf LuaJIT-2.0.5.tar.gz
    cd LuaJIT-2.0.5
    make
    sudo make install

## 6. Install Snort
    cd snort-2.9.20
    ./configure --enable-sourcefire
    make
    sudo make install

#### Instalasi Snort (Auto)
    sudo apt-get install snort

#### Cek instalasi Snort
    snort -V

## 7. Konfigurasi Snort
    sudo nano /etc/snort/snort.conf

#### Konfigurasi yang dipakai
    var HOME_NET 192.168.1.0/24

## 8. Config Rules
    alert icmp any any -> any any (msg:"ICMP Echo Request Detected"; itype:8; sid:1000001; rev:1;)
#### Keterangan
###### msg: Pesan yang muncul di log ketika rule ini terpicu.
###### itype:8: Spesifik untuk mendeteksi ICMP Echo Request, yaitu jenis paket yang digunakan untuk ping.
###### sid: Snort ID, nomor unik untuk rule ini. Pastikan tidak bentrok dengan rule lain.

## 9. Run Program
    sudo snort -i enp0s3 -c /etc/snort/snort.conf -l /home/mpi/IDS/slave -A fast icmp
###### -i enp0s3: Interface yang akan dimonitor.
###### -c /etc/snort/snort.conf: File konfigurasi Snort yang digunakan.
###### -l /home/mpi/IDS: Direktori tempat log disimpan.
###### -A fast: Menampilkan log deteksi dengan format yang sederhana.
###### icmp: Filter untuk menangkap hanya lalu lintas ICMP.

