1. AWS 콘솔에 접속합니다.
   * 주의할 점은, Region 확인을 꼭해야합니다.

[##_Image|kage@mUCwi/btqCX9e1sSd/vjjtZKdsCJsBJK1OBuNY1k/img.png|alignCenter|width="100%"|_##]

2. AWS에서 발급해주는 SSL 인증서를 사용하기 위해서는 **로드밸런서**를 반드시 사용해야합니다.
   * 게다가 도메인은 네임서버 수정이 필요합니다. 일반적인 도메인 업체에서는 네임서버에 레코드를 추가할 권한이 없기 때문에 Route 53로 등록했습니다.
     * 타 도메인 업체(가비아, 고대디 등)에서 구매한 도메인도 네임서버 변경을 통해 등록 가능합니다.
     * 아쉽게도 Route 53은 무료가 아닙니다.. **도메인 1개당 월 0.5$USD**의 비용이 발생됩니다. :cold_sweat:
   * 가격은 [여기](https://aws.amazon.com/ko/elasticloadbalancing/pricing/)에서 확인할 수 있습니다.
     * 로드밸런서 유형에 따라 가격이 다릅니다. 당연하게도, Application 로드밸런서가 더욱 비쌉니다.
   * 로드밸런서 항목은 EC2 대시보드 사이드바에 존재합니다.

[##_Image|kage@Kn5wJ/btqCVE1kaYe/afD0a6HTYUUakz7uCmPRlK/img.png|alignCenter|width="100%"|_##]

3. 로드밸런서 유형을 선택합니다.
   * OSI 7계층 중 Application Layer의 정보로 로드밸런싱할 것인지 (L7 로드밸런서)
     * Http 헤더 등 좀 더 많은 정보로 정교하게 로드밸런싱을 할 수 있습니다.
   * TCP, TLS, UDP 등 Transport Layer만으로 로드밸런싱할 것인지 (L4 로드밸런서)
     * 단순한 룰을 가지고 로드 밸런싱을 할 수 있습니다.
   * 저희 서비스에서는 Network만으로도 충분히 가능할것으로 보아 **Network Load Balancer**를 선택했습니다.

[##_Image|kage@9m9od/btqCYFSe2gg/N0syGhZ9JDdOsmUFAUGA7k/img.png|alignCenter|width="100%"|_##]

4. 로드밸런서 이름과 리스너 프로토콜을 정의합니다.
   * 저희 서비스는 HTTP를 사용하지 않기 때문에, TLS 통신에서 사용하는 443 포트만 열었습니다.

[##_Image|kage@llr9N/btqCYGczwAT/an8Qkj3jVH3Y9Ul6EXehw1/img.png|alignCenter|width="100%"|_##]

5. VPC(Virtual Private Cloud)와 함께 로드밸런서 가용영역을 선택합니다.
   * 가지고 있는 인스턴스나 RDS 등이 어느 가용영역에 있는지 확인하고 설정해줍니다.
   * 같은 가용영역 내의 통신에서는 비용이 발생하지 않습니다.

[##_Image|kage@bWxi0j/btqCZ02HCEi/X452dgl35DfBN6P73vszl0/img.png|alignCenter|width="100%"|_##]

6. SSL 인증서를 선택해야합니다.
   * 아직 AWS에서 발급하는 SSL을 생성하지 못했다면 [여기](./AWS-SSL-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EB%B0%9C%EA%B8%89)에서 발급받는 방법을 확인하세요.

[##_Image|kage@eBU0kD/btqCWL6LkY1/fwSssshULHCvkoJTTsbgAk/img.png|alignCenter|width="100%"|_##]

7. `대상 그룹`은 로드밸런싱할 인스턴스나 IP의 목록입니다. 이름과 포트번호를 달아줍니다.

   * 스프링 부트를 사용하므로 8080번으로 열었습니다.
     * 8080번을 사용하기 위해서는 인스턴스의 방화벽 설정을 확인해야합니다.

   [##_Image|kage@bsKZ5u/btqCVCWLacA/e37JAYqx8fO2o2abceKCDk/img.png|alignCenter|width="100%"|_##]

   * 대상 유형을 IP로 한 이유는 개발서버를 `AWS Lightsail`을 사용했습니다. 이건 VPC이기 때문에 IP로 관리해줍니다. 

[##_Image|kage@nR0qI/btqCX9zjBji/sfp2FBcoDnzwYf6yBC8w61/img.png|alignCenter|width="100%"|_##]

8. 아까 언급했듯이 같은 VPC 내에 있는게 아니라면 다른 프라이빗 IP 주소를 찾습니다.

[##_Image|kage@HWpf1/btqCU7WZZoH/TINtBcFKuvAQAetfuz1htk/img.png|alignCenter|width="100%"|_##]

9. Lightsale 인스턴스를 보고 프라이빗 IP를 확인하여 넣어줍니다.

[##_Image|kage@ctm6Lc/btqCUytLnEU/WehOYWRXAhUrFW3fVryPf0/img.png|alignCenter|width="100%"|_##]

* **주의할 점은 Lightsale의 VPC 피어링을 활성화 해야합니다.** 그래야 로드밸런서에서 Lightsail VPC 리소스를 접근할 수 있습니다.

[##_Image|kage@bawA7a/btqCWK08yzW/SY4NNgpG8HK695Pjxw1sRk/img.png|alignCenter|width="100%"|_##]

10. 로드밸런서가 추가된 것을 확인할 수 있습니다. 이제 Route 53에서 해당 도메인으로 오는 접근을 로드밸런서 IP로 연결해주는 레코드를 추가해줍니다.

[##_Image|kage@wP0wi/btqCZyyAPII/Hf2ZFZnbSPBB9hDxt0i6Kk/img.png|alignCenter|width="100%"|_##]

11. 레코드를 추가해줄때 별칭 대상을 생성한 로드밸런서로 설정해줍니다.
    * 생성된 직후에 하면 로드가 안됩니다. 오른쪽 위 새로고침 버튼 말고 웹 브라우저 새로고침을 한번 해주세요.

[##_Image|kage@D2PdS/btqCWK7Nrye/ODnNqImV7krJ4ytLkvYHEK/img.png|alignCenter|width="100%"|_##]
