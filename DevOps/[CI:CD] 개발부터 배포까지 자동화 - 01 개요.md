### 계기

* 이번에 정부에서 공적마스크 5부제를 시행하면서 판매처*(약국, 우체국, 농협 하나로마트)*의 재고현황을 알 수 있는 [공공 API](https://app.swaggerhub.com/apis-docs/Promptech/public-mask-info/20200307-oas3#/)가 생겼습니다.
* 예상대로 공공 API를 활용해 재고현황을 알려주는 앱들이 플레이스토어에 많이 런칭되고 있는 상태였고, 저도 그 사용자 중 한명이었습니다.
* 하지만, 제가 정작 필요한 것은 **마스크가 입고되었을 때 푸시알림을 날려주는 앱**이었는데 비슷한 앱조차 없어서 만들기로 결심했습니다. :smile:
* 따라서, 서비스를 만드는 과정에서 API 서버와 Batch 서버를 만들고 배포하는 과정을 자동화하는 CI/CD 툴들을 적용한 사례와 함께 'CI/CD란 무엇인지?', '자동화를 하는 과정'에 대해서 자세히 쓸 예정입니다.
* 마스크타임 앱은 현재 런칭되었으며 [플레이스토어](https://play.google.com/store/apps/details?id=shop.maskalarm.android)에서 다운로드 받으실 수 있습니다. :tada:

---

### CI/CD란 무엇인가?

> * CI<sup>Continuous Integration</sup> (지속적 통합) : 지속적으로 [퀄리티 컨트롤](https://en.wikipedia.org/wiki/Quality_control)을 적용하는 프로세스를 실행하는 것.
> * CD<sup>Continuous Delivery</sup> (지속적 배포) : 팀이 짧은 주기로 소프트웨어를 개발하는 [소프트웨어 공학](https://ko.wikipedia.org/wiki/소프트웨어_공학)적 접근의 하나로, 소프트웨어가 언제든지 신뢰 가능한 수준으로 출시될 수 있도록 보증하기 위한 것.
>
> 출처 - Wikipedia

![image-20200326010352288](%5BCI:CD%5D%20%E1%84%80%E1%85%A2%E1%84%87%E1%85%A1%E1%86%AF%E1%84%87%E1%85%AE%E1%84%90%E1%85%A5%20%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%E1%84%81%E1%85%A1%E1%84%8C%E1%85%B5%20%E1%84%8C%E1%85%A1%E1%84%83%E1%85%A9%E1%86%BC%E1%84%92%E1%85%AA%20-%2001%20%E1%84%80%E1%85%A2%E1%84%8B%E1%85%AD.assets/image-20200326010352288.png)

> *Image from [Devops Explained](http://www.dcaulfield.com/devops-explained/)*

서비스를 개발하는 일은 단순히 코딩으로만 끝나는 것이 아니다. 