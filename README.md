# 🐧 Rocky Linux 기반 엔터프라이즈 서버 인프라 구축 프로젝트

> **Rocky Linux 환경에서 볼륨 관리, 디스크 쿼터 정책 수립 및 다양한 엔터프라이즈 필수 네트워크 서버들을 직접 구축하고 검증한 팀 프로젝트입니다.**

<br>

## 👥 Team Information (4rsenal)
- **팀장:** 신재성
- **팀원:** 정태환, 전병욱, 권승빈

<br>

## 🛠️ Tech Stack & Environment
- **OS:** `Rocky Linux 9.x`
- **Virtualization:** `VMware Workstation`
- **Languages & Tools:** `Shell CLI`, `MariaDB`, `Apache(httpd)`, `NFS`, `SAMBA`, `Sendmail`, `Dovecot`

---

## 📌 주요 수행 내용 (Key Features)

### 1️⃣ 서버 환경 세팅 및 네트워크 수동 설정
* 초기 가상머신(server1, server2, server3) 인프라 구성
* `ifconfig` 및 터미널 텍스트 인터페이스를 이용한 고정 IPv4 주소 수동 변경 및 네트워크 환경 최적화
* 외부 통신 안정성을 위한 전용 DNS 서버 매핑

### 2️⃣ Linux 디스크 및 사용자 관리 (LVM & Quota)
* **LVM(Logical Volume Manager) 구성:**
  * 물리 디스크들을 추가하여 하나의 대용량 가상 디스크 그룹(`DATA`)으로 통합
  * 이를 `VIDEO(40GB)`, `AUDIO(60GB)` 논리 볼륨으로 효율적으로 분할 및 자동 마운트(`fstab`) 처리
* **디스크 쿼터(Quota) 제한 정책 수립:**
  * 전용 스토리지 파티션을 디렉토리에 마운트 후
  * 사용자(`aespa`, `ive`, `newjeans`)를 생성하여 **Soft Limit(700MB 경고) 및 Hard Limit(1GB 저장 차단)** 일괄 쿼터 정책 적용

### 3️⃣ 엔터프라이즈 핵심 6대 서버 구축 및 연동
프로젝트의 최종 목적을 위해 다양한 네트워크 및 시스템 서비스를 패키지 설치부터 방화벽 설정까지 올인원으로 구축했습니다.

| 서버 종류 | 역할 및 주요 설정 내용 | 관련 기술 |
| :--- | :--- | :--- |
| **DNS 서버** | 모든 IP의 53번 포트 접속 허용, 마스터 서버(`4rsenal.msft`) 선언 및 CNAME 매핑 | `bind`, `bind-chroot`, `nslookup` |
| **WEB 서버** | Apache 가동, `index.html` 커스텀 웹 페이지 생성 및 80번 포트 외부 통신 확인 | `httpd`, `firewall-cmd` |
| **FTP 서버** | 익명 로그인 활성화, 외부 클라이언트 파일 송수신 검증 | `vsftpd` |
| **DB 서버** | MariaDB 서버 가동, 외부 원격 접속 권한 및 패스워드 정책 설정 | `mariadb-server` |
| **NFS 서버** | 서버간 리소스 공유를 위한 디렉토리 권한 설정 및 마운트 연동 | `nfs-utils`, `exportfs` |
| **SAMBA 서버** | Linux-Windows 이기종 간 파일 공유 인프라 구축, SELinux 보안 문맥 적용을 통한 접근 제어 | `samba`, `smb.conf`, `testparm` |

### 4️⃣ 인프라 네트워크 자동화 & 메일 시스템 구축
* **DHCP 서버:** VMware 가상 네트워크 기본 DHCP를 중지하고, 내부 주소 범위를 직접 설계하여 클라이언트에 IP 자동 할당 검증
* **MAIL 서버:** `sendmail` 및 `dovecot` 패키지를 연동하여 SMTP/POP3/IMAP 통신 인프라를 구축하고, 외부 메일 서비스로의 메일 발송 정상 작동 확인

---

## 📈 배운 점 및 성과 (Retrospective)
- **종합적인 인프라 설계 능력 배양:** 각기 분리된 서버(DNS, Web, DB 등)를 하나의 유기적인 네트워크 대역 안에서 통신하도록 연동하며 인프라 시스템의 전체 구조를 이해하게 되었습니다.
- **안정적인 스토리지 설계:** LVM과 Quota 시스템을 직접 다루며 한정된 서버 자원을 효율적으로 관리하고 인프라 장애를 방지하는 실무 중심의 능력을 키웠습니다.
