argparse
========

python argparse 표준 라이브러리 관련한 내용을 정리했음

argparse 목적
-----------

options, arguments등을 쉽게 파싱할 수 있게 함으로써 command line
program을 쉽게 만들 수 있게 함.


간략 기능 소개
------------

필수 arguments와 options을 정의하면, argparse는 sys.argv에서 이를
어떻게 파싱해줌. help와 사용메시지등도 자동으로 생성해 주고 잘못된
arguments를 주는 경우 에러메시지도 생성을 해줌.


