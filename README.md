# การติดตั้ง We Mail Server Carbonio CE

## ขั้นตอนการติดตั้ง

### 1. อัปเดตระบบก่อนเริ่มการติดตั้ง
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. ติดตั้งแพ็คเกจที่จำเป็น
```bash
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release software-properties-common
```

### 3. ตั้งค่าโฮสต์เนม
ตั้งชื่อโฮสต์เป็น `[Domain].go.th`
```bash
sudo hostnamectl set-hostname [Domain].go.th
```
แก้ไขไฟล์ /etc/hosts
```bash
sudo nano /etc/hosts
```
เพิ่มบรรทัดนี้ใน /etc/hosts:
```bash
127.0.0.1       localhost
[private ip]    [Domain].go.th
```

### 4. ดาวน์โหลดและแปลง GPG Key
ดาวน์โหลดและแปลง GPG key จาก Ubuntu keyserver
```bash
wget -O- "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x5dc7680bc4378c471a7fa80f52fd40243e584a21" | gpg --dearmor | sudo tee /usr/share/keyrings/zextras.gpg > /dev/null
```

### 5. กำหนดสิทธิ์ให้กับไฟล์ GPG Key
```bash
sudo chmod 644 /usr/share/keyrings/zextras.gpg
```

### 6. เพิ่ม repository ของ Zextras
สร้างไฟล์ `/etc/apt/sources.list.d/zextras.list` และเพิ่มบรรทัดนี้ลงไป:
```text
deb [arch=amd64 signed-by=/usr/share/keyrings/zextras.gpg] https://repo.zextras.io/release/ubuntu focal main
```

### 7. อัปเดตและติดตั้ง Carbonio CE
```bash
sudo apt update
sudo apt install carbonio-ce
sudo carbonio-bootstrap
```

---

## หมายเหตุ
- คำสั่ง `sudo carbonio-bootstrap` จะเริ่มกระบวนการตั้งค่าระบบ Carbonio CE
- แนะนำให้ทำตามขั้นตอนเรียงลำดับเพื่อความถูกต้องในการติดตั้ง
