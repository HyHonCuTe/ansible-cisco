# Võ Đào Huy Hoàng - Ansible-cisco

# Ansible Cisco Automation

Dự án này sử dụng **Ansible** để tự động hóa các tác vụ quản trị thiết bị mạng Cisco, bao gồm:
- Sao lưu cấu hình thiết bị
- Đẩy cấu hình mới lên thiết bị
- Nâng cấp hệ điều hành IOS

## 📌 Chức năng chính

### 1. Backup Config
- Tự động sao lưu cấu hình hiện tại của thiết bị Cisco.
- Lưu file cấu hình vào thư mục `backup_config/` với tên dạng `<IP>_running-config.txt`.
- Giúp dễ dàng khôi phục khi cần.

### 2. Push Config
- Đẩy cấu hình mới từ thư mục `configs/` lên thiết bị Cisco.
- Hỗ trợ cập nhật nhiều thiết bị cùng lúc dựa trên file `inventory.yaml`.

### 3. Cisco IOS Upgrade
- Tự động nâng cấp hệ điều hành IOS trên thiết bị Cisco.
- Thực hiện theo kịch bản trong `cisco-upgrade-os/upgrade_ios.yaml`.
- Đảm bảo quy trình nâng cấp an toàn và có sao lưu trước khi tiến hành.

---

## 📂 Cấu trúc thư mục

```plaintext
E:.
│   ansible.cfg               # Cấu hình Ansible chính
│   backup.yml                 # Playbook sao lưu cấu hình Cisco
│   inventory.yaml             # Danh sách thiết bị Cisco quản lý
│   push_config.yaml           # Playbook đẩy cấu hình lên thiết bị
│   README.md                  # Giới thiệu dự án
│   Ubuntu-Cisco-ssh.txt       # Hướng dẫn kết nối SSH từ Ubuntu tới Cisco
│
├───backup_config              # Nơi lưu các file cấu hình backup
│       192.168.1.20_running-config.txt
│       192.168.1.30_running-config.txt
│
├───cisco-upgrade-os           # Thư mục chứa kịch bản nâng cấp IOS
│       ansible.cfg
│       inventory.yaml
│       upgrade_ios.yaml
│
└───configs                    # Cấu hình mới cần đẩy lên thiết bị
        192.168.1.20.txt
        192.168.1.30.txt
````

---

## 🚀 Cách sử dụng

### 1. Backup cấu hình

```bash
ansible-playbook -i inventory.yaml backup.yml
```

### 2. Đẩy cấu hình mới

```bash
ansible-playbook -i inventory.yaml push_config.yaml
```

### 3. Nâng cấp IOS

```bash
cd cisco-upgrade-os
ansible-playbook -i inventory.yaml upgrade_ios.yaml
```

---

## 📄 Ghi chú

* Yêu cầu đã cấu hình SSH kết nối giữa máy điều khiển Ansible và thiết bị Cisco.
* Đảm bảo dung lượng bộ nhớ đủ trước khi nâng cấp IOS.
* Nên test cấu hình mới trên thiết bị lab trước khi áp dụng lên hệ thống thực tế.

