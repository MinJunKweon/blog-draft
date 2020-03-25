1.  Route 53 대시보드에서 `DNS 관리` 부분에 호스팅 영역을 생성해줍니다.

[##_Image|kage@ctQj6Q/btqCZxfoELs/KcJITdPmRI26VaZpPzf1Ik/img.png|alignCenter|width="100%" data-origin-width="1406" data-origin-height="679"|||_##]

2.  도메인 이름은 도메인 업체에서 구입한 도메인 명을 입력해줍니다.

[##_Image|kage@bpzK8U/btqCZyL74kz/JpD12Klx6ImfS6CHbCK8RK/img.png|alignCenter|width="100%" data-origin-width="1191" data-origin-height="679"|||_##]

3.  등록하고나면 레코드가 기본으로 세트되어 있는데, NS 레코드의 값 4개는 AWS에서 제공하는 네임서버입니다. 도메인 업체 네임서버에 설정해줍니다.

[##_Image|kage@c5TEwM/btqCZZQhphE/3dzl1LsIJKr06UL3tTZd81/img.png|alignCenter|width="100%" data-origin-width="1194" data-origin-height="652"|||_##]

4.  도메인 업체의 도메인 관리 페이지로 가서 네임서버를 설정해줍니다. 이렇게 하면 도메인 설정이 끝났습니다.

[##_Image|kage@nPkOC/btqCUxn1uyq/yc5I9qpojRfsZXRF3KQXq1/img.png|alignCenter|width="100%" data-origin-width="1207" data-origin-height="726"|||_##]