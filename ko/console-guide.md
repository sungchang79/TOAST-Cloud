## NHN Cloud > 콘솔 사용 가이드

NHN Cloud Console은 NHN Cloud 서비스를 이용하기 위한 관리 툴과 작업 창의 역할을 합니다.
여기에서는 NHN Cloud 콘솔의 기본적인 설정과 사용 방법을 안내합니다.

NHN Cloud Console은 아래와 같은 기능을 제공합니다.

- 서비스를 이용하기 위한 기본 정보 관리(조직, 프로젝트)
- 서비스 활성화/비활성화
- 서비스를 이용하는 멤버 관리
- 결제 정보 제공

## 동영상 가이드
<iframe width="560" height="315" src="https://www.youtube.com/embed/PphP9zBrHeI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 퀵 가이드
콘솔에서 제공하는 기본 기능에 대한 퀵 가이드입니다. 

![tutorial_1_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_01_202103.png)
![tutorial_2_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_02_202103.png)
![tutorial_3_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_03_202103.png)
![tutorial_4_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_04_202103.png)
![tutorial_5_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_05_202103.png)

## 조직 관리

조직은 NHN Cloud 서비스를 효율적으로 사용하고 관리하기 위해 만들어진 그룹입니다.
조직에서는 동일한 서비스 정책을, 사용자에게 공유하여 사용할 수 있습니다.

### 조직 생성

- NHN Cloud 서비스를 이용하기 위해서는 조직을 생성해야 합니다.
- 조직은 개인/사업자 회원 모두 생성할 수 있습니다.
- 조직을 생성하는 회원은 자동으로 조직의 OWNER가 됩니다.
- 조직을 생성하기 위해서는 회원의 결제 수단이 반드시 등록되어 있어야 합니다.
- 조직은 조직명/도메인 정보를 관리합니다.
- 조직의 도메인 정보는 서비스에서 사용해야 하는 정보로, 고유한 정보여야 합니다.

### 조직 서비스

조직이 생성되면, 서비스를 선택할 수 있습니다.
조직 단위로 활성화할 수 있는 서비스는 다음과 같습니다.

- Dooray!
- ERP
- Groupware
- Contact Center
- IDC
- CloudTrail

### 조직 생성 가이드

![console_guide_1_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_06_202103.png)

<center>[그림 1] 조직 생성 </center>

1. 콘솔로 이동한 뒤 상단 메뉴에서 **조직을 생성해 주세요.** 옆의 **+** 버튼을 클릭합니다.
2. **조직 생성** 창에서 조직 이름을 입력합니다. 조직 이름은 한글, 영문, 특수문자, 숫자 모두 사용 가능합니다.
3. **확인** 버튼을 클릭하면 조직 생성이 완료됩니다.
4. 콘솔 상단 메뉴에 생성된 조직 이름이 표시됩니다.
5. **설정** 버튼을 클릭하여 생성된 조직 정보를 확인합니다. 조직의 추가 정보로 도메인 정보를 입력합니다. 도메인은 NHN Cloud에서 유일한 값으로 설정해야 합니다.  

### 조직 삭제

- 조직 삭제는 조직의 OWNER만 할 수 있습니다.
- 조직을 삭제하기 위해서는 이용하고 있는 서비스를 모두 삭제해야 합니다.
- 조직 삭제 시, 조직의 모든 정보는 삭제되며 복원할 수 없습니다.

## 프로젝트 관리

프로젝트는 조직 생성 후, NHN Cloud 서비스를 이용하기 위해서 생성합니다.
프로젝트에서는 프로젝트 서비스를 활성화하여 이용할 수 있습니다.
프로젝트 서비스는 프로젝트 단위로 이용하며, 이에 따라 과금합니다.

### 프로젝트 생성

- 프로젝트 생성을 위해서는 조직을 생성해야 합니다.
- 프로젝트를 생성하는 회원은 프로젝트의 ADMIN 권한을 가집니다.
- 프로젝트 생성 시, 프로젝트 이름과 프로젝트 설명을 입력합니다.
- 프로젝트 생성 후, 프로젝트 서비스를 활성화하여 이용할 수 있습니다.
- 프로젝트 생성 후, 협업이 필요한 경우 프로젝트 멤버로 추가하여 함께 사용할 수 있습니다.

### 프로젝트 서비스

프로젝트가 생성되면, 서비스를 선택할 수 있습니다.
프로젝트 단위로 활성화할 수 있는 서비스는 다음과 같습니다.

- Compute
- Container
- Network
- Storage
- Database
- Game
- Security
- Content Delivery
- Notification
- Mobile Service
- Analytics
- Application Service
- Search
- Dev Tool
- Management
- Bill

### 프로젝트 생성 가이드

![console_guide_2_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_07_202103.png)

<center>[그림 2] 프로젝트 생성 </center>

1. 조직을 생성하면 **새 프로젝트  생성하기** 버튼이 활성화됩니다. **새 프로젝트 생성하기** 버튼을 클릭하여 프로젝트를 생성합니다.
2. **프로젝트 이름**과 **프로젝트 설명**을 입력합니다.
3. **확인** 버튼을 클릭하여 프로젝트를 생성합니다.
4. 프로젝트가 생성되면 메뉴에 프로젝트 이름이 표시됩니다.
5. **프로젝트 설정** 버튼을 클릭하여 프로젝트 정보를 확인합니다.

### 프로젝트 서비스 활성화 가이드

![console_guide_3_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_08_202103.png)

<center>[그림 3] 프로젝트 서비스 활성화 </center>

1. 프로젝트 생성 후, **서비스 선택** 버튼을 클릭하여 프로젝트에서 사용할 서비스를 선택할 수 있습니다.
2. 서비스 선택 화면에서 활성화할 서비스를 선택합니다. 서비스를 활성화할지 묻는 메시지가 나타나면 **확인**을 클릭합니다. 
3. 활성화한 서비스 목록은 콘솔 왼쪽 메뉴에서 확인할 수 있습니다. 목록에서 원하는 서비스를 클릭하면 서비스 이용 화면이 나타납니다.

### 프로젝트 삭제

프로젝트에서 이용 중인 서비스가 없을 경우에 프로젝트 삭제가 가능합니다.
프로젝트 삭제 시, 프로젝트의 모든 리소스는 삭제되며 복원가 불가능합니다.
현재까지 이용한 모든 리소스에 대한 이용 내역을 즉시 결제하고 삭제할 수 있습니다.
단, 즉시 결제하지 않고 삭제할 경우 현재까지 이용한 요금 내역은 다음 결제일에 자동 청구됩니다.

## 멤버 관리 
멤버 관리를 통해 사용자별 인증(로그인) 및 권한 부여를 통해 통제할 수 있습니다. 
프로젝트와 조직에서 멤버 관리를 별도로 할 수 있습니다. 
멤버는 NHN Cloud 회원과 IAM 회원으로 구분됩니다.

### NHN Cloud 회원과 IAM 회원 정책

| 구분           | TOAST.com 회원                                               | IAM 회원                               |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 정의           | \- 조직 관리를 위한 멤버<br>\- NHN Cloud 이용 약관에 동의한 NHN Cloud 회원으로, 서비스 이용에 대한 책임과 의무를 가지는 멤버 <br>\- NHN Cloud 서비스 전체에서 유효한 멤버로 소속된 조직이 삭제되어도 NHN Cloud 회원으로 존재 | \- 서비스 이용을 위한 멤버<br>\- NHN Cloud 이용 약관에 동의하지 않은 멤버<br>\- 조직 내에서만 유효한 멤버, 소속된 조직이 삭제되면 삭제되는 멤버 |
| 멤버 등록 방법 | \- 조직의 OWNER나 ADMIN이 NHN Cloud ID를 입력하여 등록          | \- 조직의 OWNER나 ADMIN이 조직 내 유일한 ID를 입력하여 등록<br>\- SSO 연동/API 연동 등을 통해 등록 |
| 멤버 권한      | \- 조직 관리(조직 생성/수정/조직 멤버 관리/조직 서비스 관리/결제 관리\)<br>\- 프로젝트 생성<br>\- 프로젝트 삭제 | \- 조직 서비스 이용 |
| 콘솔 접근      | \- NHN Cloud 콘솔(https://console.toast.com/) 접근 <br>\- NHN Cloud> 회원  ID/비밀번호로 로그인<br>\- (선택) 2차(이메일 또는 SMS) 인증 | \- IAM 콘솔(https://조직도메인.console.toast.com/) 접근<br> \- (Dooray!, ERP 서비스는 해당 서비스 도메인으로 접근)<br> \- 조직의 OWNER(또는 ADMIN)가 설정한 ID/PW로 로그인 \- 조직에서 설정한 로그인 보안(2차 인증, 서비스별 설정) 인증 |

### IP ACL 설정
허용한 IP(또는 IP 대역)에서만 콘솔에 접근할 수 있습니다. 
Dooray! 서비스는 해당 서비스 콘솔 화면에서 IP ACL을 설정할 수 있습니다.

- 서비스 설정 
    - 공통 설정 : 모든 서비스에 동일하게 IP ACL을 설정할 수 있습니다.
    - 서비스 별 설정 : 각 서비스(Cloud, Online Contact Workplace | Dooray! 등) 별로 IP ACL을 설정할 수 있습니다.
- IP ACL 설정 
    - 설정 안 함 : 모든 IP(또는 IP 대역)에서 콘솔에 접근할 수 있습니다. 
    - 허용한 IP(또는 IP 대역)만 콘솔 접근: 입력한 IP(또는 IP 대역)에서만 콘솔에 접근할 수 있습니다. 접근을 허용할 IP 또는 IP 대역을 입력하시면 됩니다. 

### IAM 콘솔 로그인 보안 설정
- IAM 회원의 콘솔 접속 보안을 강화하기 위해 **로그인 보안 설정** 기능을 제공합니다. 
- 모든 조직 서비스(콘솔, Online Contact, Dooray! 등)에 동일하게 설정하거나, 각 서비스별로 다르게 설정할 수 있습니다. 

![iam_console_login_security_setting_guide_1_ko.png](http://static.toastoven.net/toast/console_guide/consoleguide_09_202103.png)

1. 콘솔로 이동한 뒤 설정을 원하는 조직의 조직 설정 페이지에 접속합니다. 
2. IAM 콘솔의 **로그인 보안 설정** 버튼을 클릭합니다. 


#### 2차 인증 
2차 인증을 필수로 설정하여 사용하게 할 수 있습니다.

- 서비스 설정 
    - 공통 설정 : 모든 조직 서비스에 동일하게 2차 인증을 설정합니다. 
    - 서비스 별 설정 : 각 서비스(Cloud Console, Online Contactm Workplace | Dooray! 등) 별로 2차 인증을 다르게 설정할 수 있습니다.
- 2차 인증 설정 
    - 설정 안 함: 2차 인증을 하지 않고, 아이디와 비밀번호 입력만으로 로그인할 수 있습니다. 
    - Google OTP: 아이디와 비밀번호 입력 후, Google OTP 앱에서 제공한 One Time Password를 입력하여 인증 후 로그인할 수 있습니다.
    - 이메일: 아이디와 비밀번호를 입력한 후, 이메일 주소로 발송된 **인증** 버튼을 클릭해서 인증 후 로그인할 수 있습니다. 
- 예외 IP 설정
    - 설정 안 함 : 로그인 시 모든 IP 대역에서 2차 인증 후 로그인할 수 있습니다.
    - 설정 : 설정한 IP 또는 IP 대역에서 로그인 시 2차 인증을 하지 않고 로그인 할 수 있습니다. 

#### 로그인 실패 보안
로그인을 계속해서 실패했을 때 일정 시간이 지난 후 다시 로그인할 수 있도록 설정할 수 있습니다.

- 서비스 설정 
    - 공통 설정 : 모든 조직 서비스에 동일하게 2차 인증을 설정합니다. (서비스 별 설정 기능 미제공)
- 로그인 실패 보안 설정
    - 설정 안 함: 로그인에 실패하더라도 계속해서 로그인을 시도할 수 있습니다. 
    - 설정: 원하는 실패 횟수와 잠금 시간을 입력하면 해당 횟수만큼 로그인에 실패했을 때 해당 잠금 시간 동안 로그인을 시도할 수 없습니다. 

#### 로그인 세션
로그인 세션 설정에 따라 로그인 세션이 유지되거나 자동으로 만료됩니다.
로그인이 만료된 후에는 다시 로그인해야 콘솔에 접속할 수 있습니다.

- 서비스 설정 
    - 공통 설정 : 모든 조직 서비스에 동일하게 2차 인증을 설정합니다. (서비스 별 설정 기능 미제공)
- 로그인 세션 수 
    - 여러 기기에서 동일한 ID로 동시에 로그인할 수 있는 개수를 설정합니다. 
    - 1개 설정 시 동일한 ID로 PC, 스마트폰 등 다른 기기에서 동시에 로그인할 수 없습니다. 
      예) PC- 로그인 유지, 스마트폰 - 자동 로그아웃
- 로그인 세션 유지 시간 
    - 클릭 등의 아무런 작업이 없어도 로그인을 유지할 시간을 설정합니다. 
    - 설정한 시간 동안 클릭 등의 작업을 하지 않으면 자동으로 로그아웃됩니다. 
    - 너무 길게 설정하시면 보안상 좋지 않으니 고려하여 설정하시기 바랍니다. 


### 조직 멤버
- 조직의 OWNER는 계정의 모든 권한 부여하고 서비스를 신청할 수 있습니다. 
- OWNER는 회원을 등록하여 조직별 관리 권한을 부여할 수 있습니다.

#### NHN Cloud 회원의 조직 권한

| 작업          | 역할                                | OWNER | ADMIN | MEMBER | Billing Viewer | Log Viewer |
| ------------- | ----------------------------------- | ----- | ----- | ------ | -------------- | -------- |
| 조직 관리     | 조직 생성                           | O     |       |        |                |  |
|               | 조직 수정                           | O     | O     |        |                |  |
|               | 조직 삭제                           | O     |       |        |                |  |
| 멤버 관리     | 조직 멤버 등록                      | O     | O     |        |                |  |
|               | 조직 멤버 삭제                      | O     | O     |        |                |  |
| 서비스 관리   | 조직 서비스 활성화                  | O     | O     |        |                |  |
|               | 조직 서비스 비활성화                | O     | O     |        |                |  |
| 결제 관리     | 청구서 조회                         | O     |       |        |                |  |
|               | 이용 현황                           | O     | O     |        | O              |  |
| 프로젝트 관리 | 프로젝트 생성                       | O     | O     | O      |                |  |
|               | 프로젝트 삭제                      | O     | O     |        |                |  |
| 사용자 Action 로그 관리 | 사용자 Action 로그 조회            | O     | O     |       |                | O |

#### IAM 회원의 조직 권한 
- 조직 서비스별(Online Contact, Dooray! 등) 설정할 수 있는 권한이 다릅니다. 
- 클라우드 서비스 권한은 아래와 같습니다.
    - MEMBER 권한은 원하는 경우에만 선택적으로 부여할 수 있습니다. 
    - MEMBER 권한이 부여되면 프로젝트를 직접 생성할 수 있습니다.

| 작업          | 역할                                | MEMBER |
| ------------- | ----------------------------------- | ----- |
| 프로젝트 관리 | 프로젝트 생성             | O     |

### 프로젝트 멤버

조직의 멤버가 아니더라도 프로젝트의 멤버가 될 수 있습니다.
프로젝트 멤버에게 필요한 권한을 여러 개 부여할 수 있습니다.

#### 프로젝트 관리 권한

| 권한 | 설명 |
| --- | --- |
| ADMIN | 프로젝트 전체에 대한 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| MEMBER | 프로젝트 내 모든 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| BILLING VIEWER | 이용 현황 Read(읽기) 권한 |
| PROJECT MANAGEMENT ADMIN | 프로젝트 기본 정보 Update(갱신)<br> 프로젝트 통합 Appkey Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) <Br> 프로젝트 권한 그룹 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) <br> 프로젝트 서비스 활성화(Enable)/비활성화(Disable) <br> 프로젝트 Delete(삭제) 권한 |
| PROJECT MANAGEMENT VIEWER | 프로젝트 기본 정보 Read(읽기)<br> 프로젝트 통합 Appkey Read(읽기)<br> 프로젝트 권한 그룹 Read(읽기) 권한 |
| PROJECT MEMBER ADMIN | 프로젝트 멤버 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| PROJECT MEMBER VIEWER | 프로젝트 멤버 Read(읽기) 권한 |

#### 서비스 이용 권한

| 서비스 | 권한 | 설명 |
| --- | --- | --- |
| Infrastructure | ADMIN | Infrastructure 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Infrastructure | MEMBER | VPC, Security Group, Auto Scale, Load Balancer 서비스 Read(읽기). 이외 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Container Registry | ADMIN | Container Registry 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Container Registry | VIEWER | Container Registry 서비스 Read(읽기) |
| DNS Plus | ADMIN | DNS Plus 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Object Storage | ADMIN | Object Storage 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Backup | ADMIN | Backup 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| RDS for MySQL | ADMIN | RDS for MySQL 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| RDS for MS-SQL | ADMIN | RDS for MS-SQL 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| EasyCache | ADMIN | EasyCache 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| EasyCache | VIEWER | EasyCache 서비스 복제 그룹 메뉴 Read(읽기), 모니터링 메뉴 Read(읽기) |
| Gamebase | ADMIN | Gamebase 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | ANALYTICS VIEWER - ALL | 모든 지표 Read(읽기) |
| Gamebase | ANALYTICS VIEWER - EXCLUDING SALES | 매출을 제외한 모든 지표 Read(읽기) |
| Gamebase | ANALYTICS VIEWER - ONLY REAL-TIME | 실시간 지표 Read(읽기) |
| Gamebase | APP ADMIN | APP 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | APP VIEWER | APP 메뉴 Read(읽기) |
| Gamebase | BAN ADMIN | 이용 정지 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | BAN VIEWER | 이용 정지 메뉴 Read(읽기) |
| Gamebase | COUPON ADMIN | 쿠폰 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | COUPON VIEWER | 쿠폰 메뉴 Read(읽기) |
| Gamebase | CS ADMIN | 고객센터 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | CS INQUIRY SUPPORT | 고객센터 문의 메뉴 Read(읽기), Update(갱신) 및 멤버 메뉴 Read(읽기) |
| Gamebase | IAP ADMIN | 구매 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | IAP VIEWER | 구매 메뉴 Read(읽기) |
| Gamebase | LEADERBOARD ADMIN | 리더보드 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | LEADERBOARD VIEWER | 리더보드 메뉴 Read(읽기) |
| Gamebase | MANAGEMENT ADMIN | 관리 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | MEMBER ADMIN | 멤버 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | MEMBER VIEWER | 멤버 메뉴 Read(읽기) |
| Gamebase | MEMBER FILE DOWNLOAD | 지표, 매출, 멤버 등에 대한 메뉴 Read(읽기) 및 다운로드 |
| Gamebase | OPERATION ADMIN | 운영 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | OPERATION VIEWER | 운영 메뉴 Read(읽기) |
| Gamebase | PUSH ADMIN | 푸시 메뉴 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Gamebase | PUSH VIEWER | 푸시 메뉴 Read(읽기) |
| Leaderboard | ADMIN | Leaderboard 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Leaderboard | VIEWER | Leaderboard 서비스 Read(읽기) |
| Launching | ADMIN | Launching 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Smart Downloader | ADMIN | Smart Downloader 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| NHN AppGuard | ADMIN | AppGuard 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| App Security Check | ADMIN | Security Check 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Server Security Check | ADMIN | Server Security Check 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| Security Monitoring | ADMIN | Security Monitoring 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| CAPTCHA | ADMIN | CAPTCHA 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| OTP | ADMIN | OTP 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| WEB Firewall | ADMIN | WEB Firewall 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Vaccine | ADMIN | Vaccine 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Secure Key Manager | ADMIN | Secure Key Manager 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Secure Key Manager | VIEWER | Secure Key Manager 서비스 Read(읽기) |
| Security  Compliance | ADMIN | Security  Compliance 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제)) 권한 |
| DDoS Guard | ADMIN | DDos Guard 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| SIEM | ADMIN | SIEM 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| CDN | ADMIN | CDN 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Image | ADMIN | Image 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Push | ADMIN | Push 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| SMS | ADMIN | SMS 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Email | ADMIN | Email 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| KakaoTalk Bizmessage | ADMIN | KakaoTalk Bizmessage 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Face Recognition | ADMIN | Face Recognition 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| Maps | ADMIN | Maps 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| ROLE | ADMIN | ROLE 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| API Gateway | ADMIN | API Gateway 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| RTCS | ADMIN | RTCS 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| ShortURL | ADMIN | ShortURL 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| Cheating Detection | ADMIN | Cheating Detection 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| IAP | ADMIN | IAP 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Mobile Device Info | ADMIN | Mobile Device Info 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Cloud Search | ADMIN | Cloud Search 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Autocomplete | ADMIN | Autocomplete 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Corporation Search | ADMIN | Corporation Search 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Address Search | ADMIN | Address Search 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Log & Crash Search | ADMIN | Log & Crash Search 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Pipeline | ADMIN | Pipeline 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) 권한 |
| Deploy | ADMIN | Deploy 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Managed | ADMIN | Managed 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Service Monitoring | ADMIN | Service Monitoring 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Certificate Manager | ADMIN | Certificate Manager 서비스 Create(생성)/Read(읽기)/Update(갱신)/Delete(삭제) 권한 |
| Bill (e-Tax) | ADMIN | Bill (e-Tax) 서비스 Create(생성), Read(읽기), Update(갱신), Delete(삭제) |
| Bill (e-Tax) | VIEWER | Bill (e-Tax) 서비스 Read(읽기) |



## 결제 관리

NHN Cloud 서비스 이용 요금을 확인하고, 결제할 수 있습니다.
**내 정보 보기 > 결제 관리** 메뉴에서 결제 수단을 등록한 NHN Cloud 회원의 청구서와 결제 예정 금액, 사용량 정보를 확인할 수 있습니다.

결제 수단을 통해 해당 월에 결제되는 내역과 함께 아래의 기능을 제공합니다.

- 즉시 결제: 매월 8일 자동 결제 전에 즉시 결제 기능을 통해 결제할 수 있습니다.
- 매출 전표: 신용카드로 결제한 경우, 매출 전표를 조회할 수 있습니다.
- 세금계산서: 계좌 이체로 결제한 경우, 세금계산서를 조회할 수 있습니다.

결제 관리 청구서에 조회되는 내역은 아래와 같습니다.

- 이용 금액: 서비스 사용량과 단가를 계산한 금액
- 할인/할증 금액: 약정 할인, 관리자 할인/할증 등
- 부가세: (이용 금액 - 할인 금액 + 할증 금액)의 10%
- 연체료
    - 한국 회원: 최종 결제 금액 미납 시, 해당 금액의 2%
    - 일본 회원: 일본 소비자계약법에 의해 연체료가 발생하지 않습니다.
- 최종 결제 금액: (이용 금액 - 할인 금액 + 할증 금액) + 부가세

