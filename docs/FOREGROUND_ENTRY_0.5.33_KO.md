# 0.5.33 / 빌드 67 — 첫 전면 진입 기록과 알림 본문 진입 방지

## 원인 조사 범위

11월 25일 REA로 보관한 빌드 66 화면 기록에서 메인 화면의 첫 foreground 진입과 이후 inactive/active 반복을 분리했습니다. 12:42:19와 12:50:39 KST의 foreground 전환 직전에는 상세 알림 수신이 각각 약 17초·4초 앞서 있습니다. 그러나 `notification.detail.received`는 상세 알림 표시 완료나 터치 기록이 아닙니다. 알림이 원인이라고 확정하거나 사용자가 눌렀다고 추정하지 않습니다. 전환 당시 연결·인증은 이미 정상이고 위치 세션은 eligible입니다. [기존 관측](MAIN_SCREEN_2026-11-25_KO.md).

추가 REA 읽기와 설치는 Mac–워치 개발 터널 시간 초과(`CoreDevice 4000 / RemotePairing 1001`)로 실패했습니다. Mac의 사용자 소유 연결 서비스만 재시작했지만 같은 오류가 남았습니다. Bluetooth 켜짐, Wi-Fi IPv6 자동 설정과 link-local 주소는 확인됐으므로 IPv6 꺼짐을 원인으로 기록하지 않습니다. 기기 목록의 paired/available은 앱 컨테이너에 실제로 접근됐다는 뜻이 아닙니다.

## 변경한 동작

기존 `CompactNotificationController`는 `isInteractive` 기본값 false를 사용했습니다. 이 경우 상세 알림 본문 터치로도 기본 앱 열기가 가능합니다. 이제 true와 본문 전용 탭 처리를 사용해 **원본 아이콘이 있는 상세 알림의 본문을 눌러도 연결 메인 화면으로 넘어가지 않게 합니다.** 탭은 고정 이벤트만 남깁니다. 상단 앱 아이콘·sash의 명시적 앱 열기와 시스템 기본 알림 화면은 watchOS 동작을 유지합니다. 이번 실사용 사건이 본문 터치 때문이라는 증거는 아직 없습니다.

알림 카테고리에 `customDismissAction`을 추가했습니다. 기존 `notification.dismiss` 처리 코드는 이 옵션이 없어 명시적 닫기 이벤트를 받을 수 없었습니다. 닫기 처리는 기록만 남기며 차량 명령이나 화면 열기를 실행하지 않습니다.

## 자동 기록 보완

- 메인 인터페이스의 첫 foreground 콜백에서 `watchbridge-foreground-episodes.json`에 직전 화면 64개와 연결 이벤트 32개를 즉시 고정합니다. 반복 손목 활성화는 새 묶음을 만들지 않으며 첫 진입 문맥을 덮어쓰지 않습니다. 최근 32묶음을 보관합니다.
- 첫 main scene 활성화, 근처 알림·위치 이벤트, 뒤늦게 전달된 명시적 진입 표식, background 복귀를 같은 묶음에 연결합니다. 시간상 연관은 인과관계의 확정이 아닙니다.
- 알림 상세 view의 appear/disappear와 전면 알림 전달을 구분합니다. 알림 수신 콜백 하나를 메인 화면 표시로 분류하지 않습니다.
- 위치 활동 객체의 생성/복원 요청을 객체별 ID와 함께 **생성 전에** 기록합니다. 기존 세션 객체 수명, 위치 권한, 재참여·자동 연결 로직은 유지합니다.
- SwiftUI URL 및 웹 사용자 활동의 진입 표식을 추가합니다. 임의의 OS 진입 이유를 모두 관측한다는 뜻은 아닙니다. URL·알림 내용·사용자 활동 payload·좌표는 기록하지 않습니다.

## 설치 상태와 남은 작업

소스와 서명 빌드는 **0.5.33 / 67**입니다. 이 문서 작성 시 소유자 워치의 마지막 설치 성공은 **0.5.32 / 66**이며 새 설치는 개발 연결 복구 대기입니다. 개인 주간 갱신 소스/상태도 설치된 66을 그대로 가리킵니다. 등록·차량 설정·BLE/암호화·백그라운드 연결 방식은 변경하지 않았습니다.

**최초 OS 전면 전환 계기는 아직 미확정입니다.** 이번 수정은 확인 가능한 알림 본문 진입 경로를 막고 첫 전환 기록의 빈틈을 줄이는 조치이며, 자동 열림 전체 해결이나 백그라운드 연결의 새 실기 관측을 주장하지 않습니다. 시스템 로그·관리자 인증·실제 차량 제어·별도 QA는 진행하지 않았습니다.

REA Evidence: 추가 읽기 `ev_d77b82013b7c8a03dcd9a2e921a2628ff8a70b1e23e63aee86103f6ce0e5ae84`, 설치 실패 `ev_0b3317ec86f2e4543a844e7c1bd01e3e8940e2b08d98486733c784a1b222329b`, 서비스 재시작 후 읽기 실패 `ev_805056439f1ffa4340c0f9cca0fb019e59999c2f68e1a3a6b1878e8083d8569a`. 원본은 로컬에만 보관합니다.

공식 근거: [알림 터치 시 앱 진입 범위](https://developer.apple.com/documentation/watchos-apps/presenting-notifications-on-apple-watch), [기본 isInteractive 값](https://developer.apple.com/documentation/swiftui/wkusernotificationhostingcontroller/isinteractive), [명시적 닫기 이벤트 조건](https://developer.apple.com/documentation/usernotifications/unnotificationdismissactionidentifier), [SwiftUI 사용자 활동 처리](https://developer.apple.com/documentation/watchkit/handling-user-activity).
