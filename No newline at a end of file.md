### Git - No newline at a end of file, 왜 체크해야하나?

가끔 개발을 하다보면 Github에서 '파일 끝에 개행문자(newline)이 없습니다.'라는 문구를 볼 때가 있다.

![image-20200718170427762](/Users/minjunkweon/Library/Application%20Support/typora-user-images/image-20200718170427762.png)

자바스크립트의 `eslint` 에서도 파일 끝에 개행문자를 넣으라는 rule([eslint](https://eslint.org/docs/rules/eol-last))이 있다. 파일 끝에 엔터만 쳐주면 되는 것이라 대수롭지 않게 넘어갔지만..

직접 찾아보지 않으면 그 누구도 **이게 왜 생겼고, 왜 필요한지는 설명해주고 있지 않아서** 포스팅을 쓰게되었다.

## 파일 끝에 개행문자(`\n`)를 넣게된 역사

결론부터 말하자면, 옛날에 IEEE가 책정한 **[POSIX](https://ko.wikipedia.org/wiki/POSIX)에서 [줄(line)](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_206)을 그렇게 정의했기 때문이다.**

> **3.206 line**
>
> A sequence of zero or more non- \<newline\> characters plus a terminating \<newline\> character.
>
> *번역 : 0 또는 개행문자(newline)가 아닌 문자들이 나오다가 개행문자(newline)로 끝이 나는 시퀀스*

C 컴파일러인 `gcc`는 POSIX에 근거해서 동작하였는데, 소스코드를 한 줄씩(line by line)으로 읽게되므로 파일 끝에 EOF가 없으면 문제가 발생하는 것이었다. 

실제로 파일은 끝이 났지만 개행문자가 없어서 한 줄이 끝나지 않은 것으로 인식해서 정상적으로 동작하지 않는 이슈가 발생한다.

게다가, `cat` 과 같이 터미널상에서 파일 내용을 출력하는 명령어들을 사용할 경우, 아래와 같은 형태로 출력되는 것을 종종 보곤한다.

```sh
$ cat nonewline.txt # newline 하지 않았을 때
nonewline$ cat newline.txt
newline
$
```

`cat` 은 여과없이 모든 문자를 출력하기 때문에 파일 끝부분에 개행문자가 있는 것이 훨씬 보기 좋다.

## 결론

현대에 사용되는 컴파일러들은 위와 같이 파일 끝에 개행문자가 없어서 컴파일이 안되는 상황은 없을 것이다. *(Warning 메시지는 나오겠지만)*

하지만, 내가 의도한 것과 다르게 결과가 노출되는 경우*(위에서 말한 `cat`과 같이)*가 있을 수 있기 때문에 항상 파일 끝에 개행문자를 넣어놓는 것이 좋다.

많이 사용되고 있는 VSCode 에디터, 젯브레인 계열 IDE 등 모두 [editorconfig](https://editorconfig.org/)를 지원하기 때문에 `insert_final_newline` 옵션을 `true`로 설정해놓고 사용하자!

