+++
date = "2018-10-25T13:58:54+09:00"
description = "오라클 블록체인 클라우드를 이용한 블록체친 네트워크 프로비전 및 관리 기능 살펴보기"
title = "Oracle Autonomous Blockchain Cloud를 이용한 블록체인 네트워크 생성 및 편리한 관리 기능 살펴보기"
thumbnailInList = "https://oracloud-kr-teamrepo.github.io/2018/11/OABCS_thumb.png"
thumbnailInPost = ""
tags = ["ORACLE", "Oracle Cloud", "블록체인", "Blockchain", "Oracle Blockchain Cloud", "OABCS", "오라클 클라우드", "HLF", "Hyperledger Fabric"]
categories = ["Oracle-Cloud"]
author = "mee-nam.lee"
language = ""  

+++

**Oracle Autonomous Blockchain Cloud Service**는 블록체인 네크워크 구성 및 관리의 편리성을 극대화한 클라우드 서비스 입니다. 복잡한 설치 및 구성 과정이 필요하지 않으며, 쉽고 편리하게 여러 참여자 조직들로 구성된 블록체인 네트워크를 쉽게 생성해 낼 수 있습니다. 솔루션에서 제공되는 편리한 관리 콘솔을 통해 네트워크의 가시성을 확보함과 동시에 네트워크를 구성하는 각 컴포넌트의 상태 및 블록의 상태까지 모니터링 할 수 있게 해 줌으로써 분산 네트워크라는 특정으로 인해 발생하는 관리의 어려움을 해소시켜 줄 수 있습니다.<br/>
![Alt text](https://monosnap.com/image/q339C1ZvLdPOLtI9chCGznCMhCckRE.png)

**Oracle Autonomous Blockchain Cloud Service**는 오픈소스인 **Hyperledger Fabric**을 기반으로 하고 있습니다. Hyperledger Fabric을 설치하고 수동으로 네트워크를 구성하고 보안 기능을 추가하려고 설정을 변경하는 작업을 해본 경험이 있다면, 이 과정이 얼마나 시간이 걸리고 error-prone한 과정인지 알고 계실 것입니다. Oracle Blockchain Cloud를 이용한다면 몇 번의 클릭만으로 쉽게 네트워크를 생성하고 구성하고 모니터링 할 수 있습니다. <br/>
이 문서에서는 블럭체인 네트워크 생성과정 (Provision)과 제공되는 관리 콘솔에서 제공하는 기능들에 대해 살펴보려고 합니다.

## 블럭체인 네트워크 생성하기
블록체인 네트워크 생성을 위해 다음과 같이 오라클 클라우드 콘솔에 접속하여 **Autonomous Blockchain Cloud Service**를 선택합니다. 여기서 **Create Instance** 버튼을 클릭하여 서비스를 생성하게 됩니다.

![Alt text](https://monosnap.com/image/Xa0L90jPUzYuNO2v4aamsrq3Pkbm51)

서비스 인스턴스 생성에 필요한 몇가지 정보만 입력하면 블록체인 네트워크가 바로 생성이 됩니다. 블록체인 네트워크에는 **Founder**와 **Participant**라는 조직의 역할이 존재하는데 **Founder** 인스턴스를 생성할 경우에만 **Create a new Network** 옵셥을 선택하여 생성합니다. **Participant**는 기존 Network에 Join하는 것이기 때문에 **Participant** 인스턴스를 생성할 때는 이 옵션을 선택하지 않습니다.

![Alt text](https://monosnap.com/image/fyRMvK7LKcGwDWCcUW56Dza6Og1K2Y.png)

인스턴스 생성 시 **Configuration** 옵션에 따라 규모가 다른 네트워크가 구성되고, 현재는 다음과 같은 옵션을 제공합니다. 이 옵션과 관계 없이 네트워크 내의 Peer 수는 추후 추가 / 삭제가 자유롭습니다. 

![Alt text](https://monosnap.com/image/fYE5kooz6q29hqSNUDrIAcZblO3SlH.png)

입력한 값을 확인하는 Confirmation 화면에서 **Create** 버튼을 클릭하면 인스턴스가 생성됩니다.

![Alt text](https://monosnap.com/image/uEmSpXHtQ9PJDazF0FjArwj5l5OCgK.png)

생성은 몇 분 정도가 소요됩니다. 완료가 되면 콘솔에 접속해 보겠습니다.

![Alt text](https://monosnap.com/image/vIN4sKVU4UhpwgtJG5aH7jdqkgfJvd.png)

## 관리 콘솔 기능 살펴보기
생성이 완료된 인스턴스의 우측 메뉴 아이콘을 선택하면 해당 인스턴스의 관리 콘솔로 이동할 수 있습니다.

![Alt text](https://monosnap.com/image/iBOSxiyEAr3kaH1sBx1kdHwp42GAqL.png)

### Dashboard
블록체인 네트워크의 전반적인 현황을 살펴볼 수 있게 구성되어 있는 화면 입니다. 네트워크에 구성된 **채널(Channel)**, **피어(Peer)**, **오더러(Orderer)**, **체인코드(Chaincode)** 배포 상태에 대한 개략 정보와 컴포넌트의 Health 및 네트워크내의 트랜잭선 액티비티들에 대해서 확인 할 수 있도록 구성되어 있습니다.

![Alt text](https://monosnap.com/image/19gBg6bfdesB7mjQH58PyMq2sozuP8.png)

### Network
블록체인 네트워크에 참여한 **Participant** 조직을 보여주는 페이지 입니다. 이 페이지를 통해 **Founder**의 Orderer 설정이나 Participant의 Certificate 정보를 Export할 수 있고, 새로운 Participant를 참여시키거나 기존 참여자의 Certificate를 Revoke하는 등의 Participant와 관련된 관리 작업을 수행할 수 있습니다.

![Alt text](https://monosnap.com/image/Ej99WcyOLw5yI0wHQtwQQYIbb2aP9U.png)

토폴로지 뷰를 통해 Participant 간의 관계를 더 가시성 있게 볼 수 있습니다.

![Alt text](https://monosnap.com/image/L2eiBmkCFGgDvs7zTixh24pBQAqsKn.png)

### Nodes 
기본적으로는 해당 Participant 내에 속해 있는 노드들(Peer, Orderer, Proxy, CA, console)의 정보를 보여주는 페이지 입니다. 리모트 Participant의 Peer 정보를 Import하면 이 페이지 내에서 Remote Peer 정보를 함께 볼 수 있습니다. 노드의 추가, 삭제, 설정 변경 등의 구성 작업과 기종, 중지 등의 제어 작업을 수행 할 수 있습니다. 

![Alt text](https://monosnap.com/image/yiYrvJKAaPRmIRqlEgSeKLahcwlS67.png)

토폴로지 뷰를 통해 어느 Peer가 어느 채널에 속해 있는지 채널 관계를 더 가시성 있게 볼 수 있습니다.

![Alt text](https://monosnap.com/image/69VwqILYU36ZYxTa9SRhu2Grm7nERu.png)

### Channels
네트워크에 구성된 채널 정보를 보여주는 페이지 입니다. 채널이란 동일 네트워크 내에서도 데이터의 Privacy를 두어야 할 경우에 사용됩니다. 같은 채널에 속한 Participant들만 채널에 속한 원장에 접근할 수 있게 됩니다. 네트워크 내애서는 필요에 따라 여러 채널을 구성할 수 있습니다.

![Alt text](https://monosnap.com/image/hRNNK3W9UYgEN5UkZA5UB6PjyviSD4.png)

특정 채널을 선택하여 채널과 관련된 상세 내용(Ledger, Instantiated Chaincode, 조인된 Peer, 참여 Participant)을 볼 수 있습니다.
Ledger는 채널 별로 저장되므로 Channel 하부 메뉴에서 Ledger 기록 상태 및 Ledger Transaction 정보를 확인 할 수 있습니다. 어떤 Chaincode의 어떤 함수를 통해서 트랜잭션이 이루어졌는지 트랜잭선 수행 시의 파라미터가 무엇이었는지에 대한 내용까지 확인할 수 있습니다.

![Alt text](https://monosnap.com/image/myIZfCoDq4Ud9GsebPTu3Xn6YsKuB5.png)

### Chaincodes
체인코드를 설치하고 업그레이드하는 관리 작업을 수행하고 체인 코드의 Instantiate 여부를 확인할 수 있습니다.

![Alt text](https://monosnap.com/image/ZcWamS9Dq9Q0buQkwEgfqCh5MdE4JP.png)

체인 코드별 버전별 설치 상태 및 Instantiate 상태를 볼 수 있고 체인코드가 설치된 Peer의 로그 및 Instantiated 채널에 대해 확인할 수 있습니다.
![Alt text](https://monosnap.com/image/1BadxytBPNMzEzfBBMPpaFzpFquHQ9.png)

### Developer Tools
블록체인 네트워크를 바로 체험해 볼 수 있도록 샘플 체인코드를 이 페이지를 통해 바로 설치하고 테스트 해볼 수 있도록 구성된 페이지 입니다. 체인코드 개발에 대해 이해하고 있지 않은 상태에서도 제공된 샘플을 가지고 네트워크의 동작 및 트랜잭션 수행 과정에 대해 살펴 보며 이해할 수 있도록 구성되어 있습니다. 이 페이지를 통해서 Client SDK를 다운 받을 수 있고, 제공돈 코드 샘플을 통해 Oracle Blockchain Cloud에 접속하는 Client 개발을 쉽게 시작할 수 있도록 도와 줍니다.

**Chaincode Development** 메뉴에서는 체인코드를 개발하기 위해 필요한 가이드 문서와 샘플 코드를 다운받을 수 있고
**Application Development** 메뉴에서는 프로그램 언어별 SDK를 바로 다운 받을 수 있게 연결되어 있습니다.

![Alt text](https://monosnap.com/image/uQ0ogNocR7QPuLedhIcES6SsbYYssC.png)

**Sample** 메뉴에서는 해당 페이지에서 바로 다음과 같은 샘플 체인코드를 바로 설치하고 트랜잭션을 수행하고 결과를 확인해 볼 수 있도록 제공하고 있습니다.
![Alt text](https://monosnap.com/image/akOTKab3kZPAYVAVgF0drvTAYmfmV2.png)

여기까지 Oracle Autonomous Blockchain Cloud Service의 관리 기능에 대해 알아보았습니다. 실제 채널을 구성하고 체인코드를 배포하는 과정에서의 콘솔 기능 사용에 대해서는 다음에 이어지는 기고를 통해 다루도록 하겠습니다.

더 자세한 사항은 아래 제품 자료를 참고하세요.
## 관련글
- 다음글 : [오라클 블록체인 클라우드에 Hyperledger Fabric 샘플 체인코드 Fabcar 배포하기](http://www.oracloud.kr/post/blockchain002/)

## 참고 자료
- [Oracle Blockchian Cloud](https://docs.oracle.com/en/cloud/paas/blockchain-cloud/index.html)
- [Oracle Blockchian Cloud - 네트워크 관리](https://docs.oracle.com/en/cloud/paas/blockchain-cloud/admintasks.html)