# 관리 품목 가이드
## 책과 대여 가능한 기자재

Econo Beep 서비스를 통해 대여/반납, 관리/추가/삭제를 합니다.
자세한 가이드는 [Econo Beep Guide](https://github.com/JNU-econovation/econo-beep-2.0)를 참고하세요.
---

## 서버

에코노베이션은 1층 동방의 데스크탑 뒤 쪽에 1개, 2층 전산원 서버실 내에 1개, 총 2개의 가상화 ESXi 서버를 소유하고 있습니다.
- 소프트웨어 & 하드웨어적인 모든 문제를 관리부에서 유지보수
- 부원들로부터 서버 대여 요청이 오면, 인스턴스 세팅을 하고 전달한다.
  1. ESXi 콘솔로 대여해줄 인스턴스를 확보한다.
  2. Ubuntu를 재설치해서 복구하고 대여자의 기본정보대로 Ubuntu 세팅을 한다.
  3. 대여자에게 사용할 Instance name, User name, User password **(!! password는 특수문자 포함 8자리 이상 !!)** 를 요구한다.
  4. SSH 세팅과 방화벽 세팅(e.g. ufw)을 한다. (만약, 해당 인스턴스가 사용하는 아이피에 개방된 포트가 없거나 추가로 포트를 개방해야 한다면, [IP/Port 가이드](./server-maintenance.md) 참고)
  5. 주의 사항을 안내하고 대여해준다.
     * 주의사항
     * 동아리 서버는 전산원가 연결되어 있으며 노출된 서버입니다. 보안이 굉장히 중요하고, 늘 해킹시도가 있을 수 있습니다.
     * 사전에 요청하여 개방된 포트외에서는 전산원단에서 차단됩니다. (20번 포트 사용 불가)
     * user password 유출에 주의하세요.
- 매 학기 개강전에 대여한 인스턴스를 전수조사한다. 더이상 사용하지 않는 인스턴스라면 환수하고, 초기화한다.
---

## IT 기기

동방 내의 모니터, 공유기, 인터넷 등의 IT 기자재들의 유지보수는 관리부가 담당하고 있습니다.
책임 소재가 관리부에 있는 것은 아니지만, 문제가 발생시 주도적으로 해결하기 위해 노력해야 합니다.

동방 내 기자재의 소유는 두 가지 종류가 있습니다.
1. 전산원 소유 **(물품 뒤에 물품관리용 봉인 스티커가 붙어있습니다)**

저희가 기증 혹은 대여받아 사용중인 물품입니다.
고장 혹은 노후화되어 사용하지 않고 보관되어 있는 물품도 있는데, 저희 소유가 아니므로 버리면 안된다고, _인수인계 받았습니다. (11기 정회형 -> 21기 권순찬)_

2. 동아리 소유
    - 동아리 예산으로 구매한 물품
    - 부원에게 기증받은 물품
일부 모니터, 라쿠라쿠 의자, 모니터 젠더 등이 이에 속합니다. 
---

## 동방 인프라 구조

### 인터넷
동방으로 들어오는 메인 랜선 한 개를 허브에 연결하고, 그 허브에 공유기, 프린터, 데스크탑이 연결된 구조입니다.
그리고 전산원의 네트워크는 화이트리스트 구조입니다. 허브에서 연결된 기기들과 가상화 서버의 인스턴스가 사용하는 아이피들은
전산원에서 직접 추가하였기 때문에 사용가능합니다. 임의로 랜선에 연결하여 아이피를 사용하면 연결되지 않습니다.

만약 인터넷에 문제가 생긴다면 (네트워크 엣지 -> 허브 -> 랜선 or 네트워크 or 화이트리스트) 순서로 문제를 파악해야합니다.
**대부분 네트워크 엣지, 허브 단에서 문제가 생깁니다.**

~~(21기에서 유지보수해본 결과, 화이트리스트가 적용되어 있는지 불분명, 그냥 사용가능한 경우도 있었음)~~

### 전기
동방에 콘센트가 적습니다. 동방 벽면의 책상마다 올려진 멀티탭은 하나의 플러그에서 직렬로 연결되어 있습니다. 과부화와 화재에 주의합시다.