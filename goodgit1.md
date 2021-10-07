# Git을 사용 하는 것 vs Git을 잘 사용하는 것 (1부)


## 대상 독자

이 글(1장)은 **형상관리도구 / Git 에 대한 개념이 부족한 사람들을 대상**으로 해당 개념을 짚고 넘어가는 데에 목적을 둔다.
- 만일 개념은 어느 정도 이해하고 있고, Git에 대한 기초를 배우고자 한다면? => 2부에서 포스팅 예정
- 만일 형상관리도구에 대한 개념을 알고, Git을 이미 사용하고 있다면? =>  3부에서 포스팅 예정

이 포스팅 시리즈는 기본적으로 **개발 소스 코드를 다뤄본 적이 있다는 것을 가정**한다. (Hello,World!라도...)
또한 셜명은 GUI 대신 CLI환경을 기준으로 하기에 Linux 터미널 환경에 익숙하다면 더욱 좋다.(몰라도 지장은 없다)

## Git이란 무엇인가?

당신이 개발자 혹은 개발자가 되기 위해 공부를 하는 사람이라면 "형상관리도구" 혹은 Git이라는 말을 들어본 적 있을 것이다.(없다고 하더라도 상관 없다. 알려줄 예정이니까...)

우선 Git에 관하여 알기 전에 **형상관리도구**에 대해서 알 필요가 있다.
소프트웨어 개발에서는 많은 개발자가 동시에 개발에 참여하여, 각자 맡은 담당 개발 분야를 개발하여 단일한 플랫을 완성한다.(물론 혼자 독고로 개발하는 경우도 많다)
그런데 "단일한 플랫폼"을 "다수의 개발자"가 만들면서 발생하는 문제가 있어, 소스 코드에 대한 관리가 필요하게 되었다. 또한 소스 코드의 배포/개발 현황/변경 내역 등을 볼 수 있는 히스토리도 필요했다.
변경사항이 기록되어야 코드의 추가/수정/삭제로 말미암은 이슈가 발생되었을 때, 어느 시점에 누가 어떤 코드를 변경한지 알 수 있기 때문이다.
> ![enter image description here](https://youngjunstudy.files.wordpress.com/2019/07/git1.png)
<이미지 출처 : [https://youngjunstudy.wordpress.com](https://youngjunstudy.wordpress.com/2019/07/15/git-%EA%B8%B0%EC%B4%88-git%EC%9D%B4%EB%9E%80/)>

그래서 나온 것이 형상관리도구이다. 형상관리도구에는 다양한 도구가 존재한다. 초창기에는 CVN, SVN 등을 시작으로 발전해왔는데, 대략 국내 기준으로 10여년 전부터는 **Git으로 거의 대동단결**되는 모습이다.
<br/>
> ![Git](https://git-scm.com/images/logo@2x.png)
<이미지 출처 : [https://git-scm.com](https://git-scm.com)>

그렇다! **Git!** 형상관리도구 중에 단연 으뜸이 있으니 그것은 Git이다. 사실 리누스 토르발스가 필요에 의해(원격 서버에 접속 없이 로컬 환경에서 개발하기 위한 것이 첫번째 이유였다고 한다. ~~나라면 옳타쿠나 하고 쉬었을 거 같은데...~~) 후딱 만들었는데 그 수준이 가히 엄청나다.(이건 필자의 생각이지만 기존 CVN, SVN은 파일간 차이를 기록하는 방식이었지만, Git은 상태를 Snapshot으로 저장하는 방식이기 때문이다. 그것도 매우 적은 용량으로...)
Git이 세상에 나온지는 오래 되었지만(2005년 첫 버전인 0.99가 출시되었으니 벌써 16년이 된 도구이다) 아직도 구형 형상관리도구를 사용하거나 그 조차도 사용하지 않는 곳이 많다.
또한 사용은 하는데, 제대로(?), 잘~! 사용하는 곳이 많지 않다는 것을 종종 전해 듣는다. 참으로 안타까운 일이 아닐 수 없다. 그 안타까움운 마음을 담아 이제부터 Git에 대해 알고 있는 지식을 조금이나마 나누어 보려고 한다.

## Git의 특징

1. Branching 모델, 로컬에 다수의 독립성이 보장되는 Branch를 허용하고 쉽게 생성, 병합, 삭제를 지원
   > 각기 다른 로컬(개발자 컴퓨터) 개발 환경에서 나 혼자 개발하듯이 개발하고 다른 개발자가 개발한 내용을 상시로 업데이트(Pull) 받고, 이를 내 코드와 병합(Merge)하는 등의 작업을 할 수 있다는 뜻이다.
2. 원격 서버 Git Repository에 Push 하지 않은 채 여러 Branch 생성 가능
   > 원격 서버(Remote Origin)의 저장소(Repository)는 개발자들의 여러 코드가 모이는 곳이며, 이와 별개로 로컬 환경에서도 별도의 기능단위 개발을 Branch라는 것을 생성하여 개발할 수 있다는 것을 의미한다.
3. 로컬 우선 작업을 통해 성능이 SVN, CVS보다 우수
   > 원격 서버(Remote Origin)로의 네트워크 접속은 실제 반영(Push)하기 전까지는 불필요하기 때문에 속도면에서 월등한 퍼포먼스를 보여준다.
4. 팀 개발을 위한 분산 환경 코딩에 최적화
   > 2번의 특징과도 비슷한 내용이다. 여러 개발자가 동일한 서비스를 각자의 환경에서 자유롭게 개발하여 원격 서버에 반영할 수 있다.
5. 파일 암호화 및 체크섬(checksum)을 통한 데이터 보장
   > 실제 Git을 사용하면 .git이라는 디렉토리를 생성하게 되는데, 이곳 하위 디렉토리인 objects의 내부를 살펴보면 각 Event에 해당하는 파일의 변경 부분 등이 저장되어있다. 이 내용은 Binary로 관리되어 복호화할 수 없도록 설계되어있다. 또한 각각의 Event에 대한 것은 checksum(SHA-1 Hash)을 이용하여 관리되기 때문에 무결성을 보장할 수 있다. (Git은 모든 것을 Hash로 식별한다.)
6. Staging Area를 통해 서버의 Repository로 업로드
   > 이 부분이 조금 어려울 수 있는데, Staging Area는 말 그대로 준비 영역으로 곧 반영(Commit)될 예정의 파일 정보를 저장하는 곳이다. Working Tree(작업 공간)에서 작업된 반영 예정을 선정하면 그것은 Staging Area로 올라가고, 실제 저장소에 반영이 될 때는 이 Staging Area에 적용된 파일이 반영된다.
![enter image description here](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/BiPDi/btqxImYCeWy/b8kX54ZRgvbEQlcXMRoUO0/img.png)
<이미지 출처 : [https://hees-dev.tistory.com](https://hees-dev.tistory.com/41)>

7. 원격 Repository 장애에도 문제없이 버전 관리 가능
   > 계속해서 나오는 이야기(Git의 가장 강력한 기능이다)이지만, 2번의 특징과 마찬가지로 로컬 환경에서 개발하고 원격 저장소(Remote Origin Repository)가 정상화 되었을 때, 반영(Push)할 수 있다.

여러 특징들이 나와있지만 심플하게 정리한다면, 여러 개발자가 로컬 개발 환경에서 각자의 개발 담당 기능별로 Branch라는 것을 만들어, 개발하고 완성되면 이를 일종의 저장소(Remote Origin Repository)에 모아 관리하는 역할을 하는 것이다. 즉, 하나의 요리(된장찌개)를 완성하기 위해 누군가는 양파를 썰고, 누군가는 애호박을, 누군가는 물을 끓이는 일련의 과정들을 기록하고 섞어(Merge) 된장찌개를 완성하는 것이라고 볼 수 있다!!
>  ![](https://www.mjmedi.com/news/photo/201904/36633_26233_4154.jpg)
<이미지 출처 : [https://www.mjmedi.com](https://www.mjmedi.com/news/articleView.html?idxno=36633)>

## 설치

Git 설치에 대해 다루는 것보다는 필자의 생각에 가장 참고하기 좋은 Link를 첨부하는 것으로 대체하겠다.(절대 귀찮아서 그런 것은 아니다.)
1. For Ubuntu
   > [제타위키 Ubuntu Git 설치](https://zetawiki.com/wiki/%EC%9A%B0%EB%B6%84%ED%88%AC_git_%EC%84%A4%EC%B9%98)
2. For CentOS
   > [제타위키 CentOS Git 설치](https://zetawiki.com/wiki/CentOS_git_%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)
3. For MacOS
   > [https://investechnews.com/2021/06/14/mac-git-setting](https://investechnews.com/2021/06/14/mac-git-setting)
4. For Windows
   > [제타위키 Windows Git 설치](https://zetawiki.com/wiki/%EC%9C%88%EB%8F%84%EC%9A%B0_Git_%EC%84%A4%EC%B9%98)

## 마치며
다음 포스팅에서는 실제 Git을 사용하여 CLI환경에서 코드를 반영하고, 적용하는 등 실무에 바로 활용할 수 있도록 기본적인 Git Command에 대해 포스팅하겠다.

## Reference
- https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88
- https://ko.wikipedia.org/wiki/%EA%B9%83_(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4)
- https://zetawiki.com/wiki/Git
- https://investechnews.com/
- https://youngjunstudy.wordpress.com/2019/07/15/git-%EA%B8%B0%EC%B4%88-git%EC%9D%B4%EB%9E%80/
- https://hees-dev.tistory.com/41
