+++
date = "2017-08-11T22:20:25+09:00"
description = "Oracle Public Cloud에서 사용되는 Identity Domain의 의미가 무엇인지 살펴보겠습니다."
title = "Identity Domain"
thumbnailInList = "https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/logoinlist.jpg"
thumbnailInPost = "https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/logoinpost.jpg"
tags = ["Identity Domain", "Oracle Cloud"]
categories = ["Oracle Cloud"]
author = "taewan.kim"
language = ""
+++

Oracle Cloud 계정 생성, Oracle Cloud 로그인, 클라우드 서비스 활성화 과정에는 "__Identity Domain__"을 직접 설정하거나,  Identity Domain을 포함하는 정보를 입력해야만 합니다.
Identity Domain은 기존에 일반적인 IT 용어로 생각하기 쉽지만, 오라클 클라우드의 고유명사입니다.
Oracle Cloud에서 Identity Domain의 정의가 무엇이고, 어떤 의미가 있는지 알아보겠습니다.
추가로, Identity Domain에는 Cloud User 관리 기능이 포함됩니다.
이와 관련하여 Oracle Cloud에서 Identity Domain과 Cloud User의 관계를 알아보겠습니다.

## Terminology: 용어 정리

본 문서에서는 다음과 같은 용어를 사용하며, 의미는 다음과 같습니다.

| 주요 용어 | 설명 |
| --- | --- |
|Oracle Account|oracle.com에 로그인 가능한 계정.<br/> 오라클 클라우드의 사용자 계정은 oracle.com에 사전 등록이 되어 있어야 합니다. Identity Domain에는 Oracle Account만이 등록될 수 있습니다. 하나의 Oracle Account는 여러 Identity Domain에 등록될 수 있습니다.|
|Cloud User|특정 Identity domain에 등록된 Oracle Account.<br/> - 오라클 클라우드에 로그인하고 작업하는 사용자 계정을 의미합니다.|
|Oracle Cloud service account|회사나 조직에서 지명한 오라클 클라우드 관리자 계정. 슈퍼 권한이 할당된 Cloud User<br/> 주요 역할: <br /> - identity domain 생성. <br/> - 클라우드 서비스 활성화. <br/> - Oracle Account를 Cloud User로 등록. <br/> - Cloud User의 권한 관리.|

## Identity Domain이란?

오라클 클라우드 문서에서 "__Identity Domain__"을 다음과 같이 설명합니다.

> Identity domain controls the authentication and authorization of the users who can sign in to an Oracle Cloud service and what features they can access.
>
> An Oracle Cloud service must belong to an identity domain. Multiple services can be associated with a single identity domain to share user definitions and authentication. Users in an identity domain can be granted different levels of access to each service associated with the domain.

위 설명에 따르면 "__Identity Domain__"는 Cloud User의 인증과 서비스 접근 권한을 관리하는 단위입니다. 모든 오라클 클라우드 서비스가 활성화되기 위해서는 Identity Domain에 포함되어야 합니다. 하나의 Identity Domain에 여러 오라클 클라우드 서비스가 인스턴스 형태로 만들어지고 활성화될 수 있습니다. 같은 "__Identity Domain__"에 소속된 오라클 클라우드 서비스는 사용자 인증과 접근 권한 정보를 공유합니다.

오라클 문서의 Identity Domain 설명에서는 사용자 권한 관리 측면이 강조되어 있습니다. Identity Domain은 오라클 클라우드 시스템 디자인 측면과 클라우드 인프라 관점에서도 중요한 의미가 있습니다.

### 엔터프라이즈 조직을 반영한 디자인
오라클 클라우드는 "__Enterprise Cloud__"를 지향합니다. 기업의 IT 부서에서는 관련된 시스템 단위로 조직을 구성하고, 담당자 지정 및 권한을 관리됩니다. 클라우드에서도 관련 시스템을 그룹화하고 시스템 담당자 할당 및 권한을 관리하는 체계가 필요했습니다. 클라우드 디자인에 전통적인 기업 IT 조직의 개념을 반영한 결과물 중의 하나가 Identity Domain입니다. Identity Domain은 관련된 시스템의 묶음이며, 이 시스템을 관리하는 담당자들의 인증, 권한관리 및 접근 제어를 통합 관리하는 체계입니다. 오라클 클라우드를 사용하는 기업(사용자)은 동시에 여러 Identity Domain을 만들고 관리할 수 있습니다.

### 클라우드 인프라 자원 관점  

클라우드 시스템은 멀티테넌시(Multitenancy) 개념을 근간으로 발전하였습니다. 테넌트(Tenant)의 사전적 의미는 "임차인"입니다. 건물 하나를 여러 임차인이 사용하여 활용도를 극대화하는 개념이 클라우드의 멀티-테넌트 개념입니다. 클라우드는 기본적으로 테넌트끼리 논리적으로 격리하여 사생활 침해를 방지하는 기능을 포함합니다.[^2]

[^2]: 클라우드의 Multitenancy로 부터 "noisy neighbor" 문제가 발생하기도 합니다. 하나의 서버에 여러 VM(Virtual Machine, 가상머신)이 동작할 경우, 특정 VM이 과도한 자원을 사용하는 경우, 동일 서버내의 VM의 성능이 저하되는 문제입니다. Oracle Cloud는 이런 문제를 제공하기 위해서 General Purpose Compute, Dedicated Compute, Bare metal를 제공합니다. Dedicated는 특성 서버를 계정에 할당하는 고객의 VM은 지정된 서버에 전용으로 동작하는 방식입니다. Bare metal은 서버 자체를 계정에 임대하고 고객이 직접 가상화 및 모든 서버 운영 체계를 결정하는 방식입니다.

오라클 클라우드에서 Identity Domain은 테넌트와 같은 의미로 사용됩니다. Identity Domain 내에 활성화된 모든 클라우드 서비스는 하나의 네트워크에 배치됩니다. 즉 Identity domain에서 활성화되는 Compute CS의 VM, DBCS의 데이터베이스, JCS의 WAS, Container CS의 Docker 등 모든 자원은 하나의 네트워크에 배치됩니다. Identity Domain 내부에서도 네트워크 레벨의 격리가 필요할 경우 Subnet을 구성할 수 있습니다.[^3]

[^3]: 오라클 클라우드는 IP Address를 중앙에서 관리하는 Shared Network와 Identity Domain에서 IP 할당과 Subnet을 관리하는 IP Network 두 가지 방식을 제공합니다. Identity Domain이 기본적으로 하나의 네트워크에 구성된다는 것은 Shared Network을 사용합니다. Subnet을 구성하면 IP Network가 적용됩니다.

Identity Domain은 컴퓨팅 자원 측면과 네트워크 측면에서 관련 자원이 하나의 시스템 단위로 관리되고 격리되는 공간인 테넌트(Tenant)입니다.

### Identity Domain을 요약하면...

Identity Domain은 연관된 클라우드 서비스를 묶는 네트워크 및 컴퓨팅 자원관리 체계입니다. Identity Domain에는 복수의 사용자가 Cloud User로 등록됩니다. 등록된 Cloud User에는 개별적인 접근 권한과 Role이 할당됩니다. 이 정보는 Identity Domain에 활성화된 모든 서비스가 공유합니다. Identity Domain 들은 완전하게 격리된 테넌트 공간입니다. 물론 필요한 경우 추가적인 보안 설정을 통해서 Identity Domain 간의 통신이 가능합니다. Identity Domain 사이의 통신은 외부 네트워크 통신으로 분류됩니다.[^4]

[^4]: Identity Domain 간의 통신이 외부 네트워크 통신으로 분류되지만, 여전히 오라클 클라우드 내부에서 발생하는 트래픽입니다. 오라클 클라우드 내부에서 발생하는 트래픽에 대해서는 별도의 과금을 하지 않습니다.

## Cloud user 등록 및 권한 관리

"__Oracle Cloud service account__"는 Identity Domain을 생성하고 관리하는 슈퍼 유저 권한을 갖습니다. 오라클 트라이얼 계정을 신청하면 Identity Domain이 만들어지고, 계정을 신청한 Oracle Account는 "__Oracle Cloud service account__"로 등록됩니다.

"__Oracle Cloud service account__"는 동시에 여러개의 Identity Domain을 관리할 수 있습니다. "__Oracle Cloud service account__"는 Identity Domain에 Cloud User를 등록하고, Cloud User에게 서비스 별 접근 권한을 설정할 수 있습니다.

하나의 "__Cloud User__"는 동시에 여러 Identity Domain에 등록될 수 있습니다. "__Cloud User__"에 설정된 권한은 해당 Identity Domain에서만 유효합니다.

### 사용자 등록
오라클 클라우드에서 "__Oracle Cloud service account__" 계정으로 Identity Domain에 로그인하면 <그림 1>과 같은 오라클 클라우드 대시보드가 출력됩니다. 대시보드에서 __USER__ 메뉴를 클릭하여 메뉴관리 페이지로 이동할 수 있습니다.

- <그림 1> 오라클 클라우드 대시보드의 Cloud User 관리 메뉴
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt01.jpg)

Cloud User 관리 페이지에서 __Add__ 버튼을 클릭하여  현재 Identity Domain에 Cloud User를 추가할 수 있습니다. <그림 2 참조>

- <그림 2> Cloud User 관리 페이지
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt02.jpg)

<그림 3>과 같이 추가할 Cloud User의 이름, 메일, 권한을 선택하고 __Add__ 메뉴를 클릭합니다. <그림 3>에서 추가한 메일은 __Oracle Account__ 로 등록된 메일이어야 합니다. <그림 3>에서는 "__Application Container Cloud Service__"를 선택하였습니다. 현재 Identity Domain에는 활성화된 Application Container Cloud Service가 없는 상태입니다.

- <그림 3> Cloud User 설정 및 추가
  -  ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt03.jpg)

Cloud User가 정상적으로 추가되면 <그림 4>와 같이 출력됩니다.

- <그림 4> Cloud User 목록
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt04.jpg)

<그림 4>에서 추가한 Cloud User에게는 <그림 5>와 같은 메일이 발송됩니다. 이 메일에는 접속에 필요한 계정명, 임시 패스워드, 데이터 센터, Identity Domain 명과 같은 정보를 확인할 수 있습니다.

- <그림 5> Identity 도메인 접속 정보 메일
  -  ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt05.jpg)

<그림 5>의 Identity Domain 접속 정보로 오라클 클라우드에 접속하면 <그림 6>과 같은 페이지가 출력됩니다. <그림 3>에서 Cloud User에게는 __Application Container Cloud Service__ 일반 접속 관리만을 추가시켰습니다. 현재 Identity Domain에는 __Application Container Cloud Service__ 이 존재하지 않기 때문에 이용 가능한 서비스가 없다는 메시지가 출력됩니다.

- <그림 6> 오라클 클라우드 대시보드 페이지: Cloud User 권한 문제로 서비스를 출력하지 메시지 출력
  -  ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt06.jpg)

<그림 7>, <그림 8>과 같이 "__Oracle Cloud service account__"로 다시 로그인하여 현재 사용 중인 Cloud User에 Oracle BDCSCE(BigData Cloud Service - Compute Edition) 관리자 권한을 추가합니다.

- <그림 7> Cloud User 권한 수정 페이지 이동
  -   ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt07.jpg)

- <그림 8> BigData Cloud Service - Compute Edition 생성 권한 추가
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt08.jpg)

수정한 Cloud User 계정 정보로 다시 오라클 클라우드에 로그인하면 <그림 9>와 같은 대시보드를 확인할 수 있습니다. 권한이 수정된 Cloud User로 로그인한 오라클 클라우드 대시보드에는 Oracle BDCSCE 서비스 콘솔 메뉴가 추가된 것을 확인할 수 있습니다.
- <그림 9> BigData Cloud Service - Compute Edition 생성 권한 추가
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/usermgt09.jpg)

### 사용자 일괄 등록

Identity Domain에 여러 Oracle Account를 한꺼번에 Cloud User로 등록할 수있습니다.
<그림 10>과 같이 "__import__" 메뉴를 이용하여 파일을 등록하면 됩니다.

- <그림 10> Cloud User 파일업로드 등록 방식
  - ![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/batch00.jpg)

<그림 10>에 등록하는 파일 포멧은 첫 번째 줄에 헤더를 포함하는 CSV 파일 포맷입니다. 파일 구성은 다음과 같습니다.

- <그림 11> csv 파일 포멧
![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/batch01.jpg)
![](https://oracloud-kr-teamrepo.github.io/2017/08/identity_domain/batch02.jpg)

<그림 11>이 Cloud User 배치 등록을 위한 CSV 파일을 준비할 때 다음과 같은 사항을 고려해야 합니다.

1. <그림 11>과 같은 컬럼 명과 순서를 유지해야 합니다.
1. 파일은 ANSI 혹은 UTF-8으로 인코딩해야 합니다. 데이터에 한글을 포함할 경우 반드시 UTF-8으로 인코딩해야 합니다.
1. 파일 사이즈는 2MB를 넘을 수 없습니다.
1. 구분자는 반드시 "comma(,)"를 사용해야 합니다.

## 요약

Identity Domain은 오라클 클라우드 시스템에서 컴퓨팅 자원을 관리하는 독립적인 테넌트입니다. Identity Domain 사이에 컴퓨팅 자원, 네트워크 그리고 Cloud User 정보가 격리 및 관리되어 독립성이 확보됩니다.

Oracle Cloud의 Cloud User는 동시에 여러 Identity Domain에 할당될 수 있습니다. Identity Doman 관리자 계정인 "__Oracle Cloud service account__"는 Identity Domain에서 관리자 권한을 갖는 계정입니다. 모든 클라우드 서비스를 활성화 및 제거 등 라이프사이클 전체를 관장할 수 있습니다. 또한, Identity Domain에 Cloud User를 등록하고 권한을 관리 할 수 있습니다.

Identity Domain에는 복수의 여러 서비스가 활성화될 수 있고, IP Network을 이용하여 서브넷을 구성할 수 있습니다.  서브넷에 지정되는 IP는 자체적으로 관리합니다. IP Network로 구성된 서브넷들은 IP Exchange[^5]로 통신 가능합니다. 필요한 경우 Identity Domain 간의 통신도 가능합니다. 이때 Identity Domain 사이의 통신은 외부 네트워크 통신으로 간주됩니다. Identity Domain 사이의 통신은 외부 네트워크 통신으로 분류되지만, 여전히 오라클 클라우드 내부 트래픽이기 때문에 별도의 과금은 발생하지 않습니다.

[^5]: IP Exchange는 Oracle Cloud의 Route입니다.

## 참고자료
- [Getting Started with Oracle Cloud: Oracle Cloud Terminology](https://docs.oracle.com/en/cloud/get-started/subscriptions-cloud/csgsg/oracle-cloud-terminology.html)
- [Oracle Cloud Terminology ](https://docs.oracle.com/en/cloud/get-started/subscriptions-cloud/csgsg/oracle-cloud-terminology.html)
- [Using Oracle Planning and Budgeting Cloud: Identity Domain](https://docs.oracle.com/cloud/latest/pbcs_common/UPBCS/identity_domain.htm#UPBCS-cloud_user_book_29)
- [Getting Started with Oracle Cloud: Oracle Cloud Terminology ](https://docs.oracle.com/en/cloud/get-started/subscriptions-cloud/csgsg/oracle-cloud-terminology.html)
- [Oracle Cloud Identity Domain – Concepts](http://expertoracle.com/2016/12/24/oracle-cloud-concepts/)
- [Importing a Batch of User Accounts](https://docs.oracle.com/en/cloud/get-started/subscriptions-cloud/csgsg/importing-batch-user-accounts.html)
