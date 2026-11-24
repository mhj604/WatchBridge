# 2026-11-23 — Mac 개발 연결 실패 범위

**후속 결과 — 2026-11-24:** 0.5.32 / 빌드 66 설치와 백그라운드 실행 완료. 아래의 11월 23일 실패·대기 상태는 당시 기록입니다. [최신 설치 기록](DEPLOYMENT_0.5.32_KO.md).

워치 소유자의 개발 연결에 대한 기록입니다. WatchBridge의 갤럭시–워치 BLE 연결이나 차량 창 자동 열림의 원인을 확정한 문서가 아닙니다.

## 관측한 내용

- 개발 모드와 저장된 Mac 개발 페어링은 활성 상태입니다. Mac Bluetooth도 켜져 있습니다.
- CoreDevice의 실제 연결은 disconnected에서 unavailable로 바뀌었습니다. 마지막 성공 연결 시각은 11월 23일 15:27 KST입니다.
- REA의 앱 파일 읽기와 설치는 CoreDevice 4000 / RemotePairingError 1001로 실패했습니다.
- 이후 앱 파일 읽기는 CoreDevice **4016**으로 즉시 실패했습니다. 필요한 `coreDeviceServicesLoaded`, `remoteServiceDiscoveryTrustedConnectivityAvailable`, `powerAssertionTaken` 상태를 확보할 수 없고, `CurrentlyAssertableStates`는 비어 있습니다. 이 메시지만으로 배터리 부족이나 암호 잠금이 원인이라고 단정하지 않습니다.
- 기기 정보 명령은 캐시된 정보를 반환하며 종료 코드 0을 낼 수 있습니다. `outcome=success`만으로 실제 연결 성공으로 기록하지 않습니다.
- 짧은 Bonjour 검색 구간에서 remote-pairing 서비스는 발견되지 않았습니다. 별도의 rp-tunnel 서비스는 발견됐지만 워치 서비스라는 식별 근거가 없으며, 검색된 포트는 TCP 연결을 거부했습니다.
- Mac의 로컬 경로와 IPv6 link-local 주소는 존재하며, Device Hub와 remotepairingd는 방화벽에서 수신 허용입니다. VPN 연결은 끊겨 있어도 네트워크 확장 등록은 활성 상태였습니다. 확장 등록만으로 실제 차단을 증명하지는 못합니다.

## 결론과 미확정 원인

직접 실패 지점은 **Apple 개발 서비스 검색·신뢰 연결·터널 수립**입니다. 앱 파일 읽기와 설치 전에 실패하므로 해당 실패를 WatchBridge 앱 로직이나 APK 문제로 진단하지 않습니다. 워치 개발 서비스 상태, Mac의 네트워크 필터 간섭, 협상 주소의 유효성은 아직 분리되지 않았습니다.

[동일 watchOS 27.2·Ultra 2의 개발 재연결 사용자 보고](https://developer.apple.com/forums/thread/848740)가 있지만, 우리 기기의 동일 결함이나 Apple의 공식 원인 확인을 뜻하지 않습니다.

REA Evidence: `ev_1aeed59090846d1e0341c9358900849c1924aed472a8c101b640d640f4ea05ff`, `ev_7ca442a529c1a86334bd85b37166275dd578204656edf8fefca68d2f0d34eee9`, `ev_c458242dfabed511a7025da58a03c694c7119a695a32f961649d7d21229d065e`. 원본은 로컬에만 보관합니다.

기기·앱 등록 초기화, 방화벽·네트워크 보호 설정 변경, 시스템 로그 수집, 관리자 인증, 차량 명령은 진행하지 않았습니다. Mac 기기 검색 창은 닫았습니다. 설치본은 여전히 0.5.30 / 64이며 0.5.32 / 66은 설치 대기입니다.
