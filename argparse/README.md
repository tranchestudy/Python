argparse
========

python argparse 표준 라이브러리 관련한 내용을 정리했음

argparse 목적
-----------

options, arguments등을 쉽게 파싱할 수 있게 함으로써 command line
program을 쉽게 만들 수 있게 함.


간략 기능 소개
------------

필수 arguments와 options을 정의하면, argparse는 sys.argv에서 넘겨 받은
인자를 파싱해줌. help와 사용메시지등도 자동으로 생성해 주고 잘못된
arguments를 주는 경우 에러메시지도 생성을 해줌.

### 간략 사용 방법

* Creating a Parser 
~~~python3
>>> import argparse
>>> parser = argparse.ArgumentParser(description='Process some integers.')
~~~

* Adding arguments
~~~python3
>>> parser.add_argument('integers', metavar='N', type=int, nargs='+',
help='an integer for the accumulator')
~~~

* Parsing arguments
~~~python3
>>> parser.parse_args()    # 프로그램 실행시 인자로 받은 sys.argv를 파싱함
>>> parser.parse_args(['--sum', '7', '-1', '42'])  # 인자로 받은 list를 파싱함
~~~

References
----------

* [Python Standard Library](http://docs.python.org/3.4/library/argparse.html)
