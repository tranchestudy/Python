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

add_argument() method
-----------------------

```python3
ArgumentParser.add_argument(name or flags...[,action][,nargs][,const][,default][,type][,choices][,required][,help][,metavar][,dest])
```

* name or flags: option string의 이름 또는 목록. e.g. foo or -f, --foo
* action: command line에서 지정된 argument에 대한 action 지정
* nargs: 지정된 option string에서 사용할 command line argument 수. option string에 하나 이상의 값을 사용할 때 사용.
* const: 일부 action이나 nargs에서 요구되는 constant value
* default: command lin에서 argument가 생략되었을 때 사용되는 기본 값
* type: command line argument 변환되야 하는 type
* choices: argument에 사용될 값 목록
* required: command line에서 생략될 수 있는지 여부 (optional argument인 경우에만 사용)
* help: argument에 대한 간단한 설명
* metavar: usage message의 argument 이름
* dest: parse_args()로 생성된 객체에 추가될 attribute 이름.

### 1. name or flags

command line의 argument가 optional argument인지 positional argument인지 지정.
* optional argument: -f나 --foo 형태
* positional argument: filename 등의 argument

~~~python3
>>> parser.add_argument('-f', '--foo')
>>> parser.add_argument('bar')
>>> parser.parse_args(['BAR'])
>>> parser.parse_args(['BAR', '--foo', 'FOO'])
~~~

### 2. action

add_argument로 추가된 command argument에 대한 action 정의. parse_args()로 반환된 개체에
attribute를 추가등을 함.

* 'store' - argument 값을 저장함. default action
   ~~~python3
   >>> parser.add_argument('--foo')
   >>> parser.parse_args('--foo 10'.split())
   Namespace(foo='10')
   ~~~

* 'store_const' - const keyword argument에 지정된 값을 저장함. flag성 optional 
argument를 지정하기 위해 사용
   ~~~python3
   >>> parser.add_argument('--foo', action='store_const', const=42)
   >>> parser.parse_args('--foo'.split())
   >>> Namespace(foo=42)
   ~~~

* 'store_true' or 'store_false' - const keyword argument 값이 True나
False로 지정된 특화된 'store_const'.
   ~~~python3
   >>> parser.add_argument('--foo', action='store_true')
   >>> parser.add_argument('--bar', action='store_false')
   >>> parser.parse_args('--foo --bar'.split())
   Namespace(bar=False, foo=True)
   >>> parser.parse_args([])
   Namespace(bar=True, foo=False)
   ~~~

* 'append' - argument value를 list로 저장. option이 command line에 여러 번 
지정될 수 있을 때 사용
   ~~~python3
   >>> parser.add_argument('--foo', action='append')
   >>> parser.parse_args('--foo 1 --foo 2'.split())
   Namespace(foo=['1', '2'])
   ~~~

* 'append_const' - const keyword argument에 지정된 값을 list로 저장. option이
command line에서 여러 번 지정되는 option에 대해 상수를 동일한 list에 저장하기 위해
사용
   ~~~python3
   >>> parser.add_argument('--str', dest='types', action='append_const', const=str)
   >>> parser.add_argument('--int', dest='types', action='append_const', const=int)
   >>> parser.parse_args('--str --int'.split())
   Namespace(types=[<class 'str'>, <class 'int'>])
   ~~~
   ~~~python3
   >>> parser.add_argument('--str', action='append_const', const=str)
   >>> parser.add_argument('--int', action='append_const', const=int)
   >>> parser.parse_args('--str --str --int'.split())
   Namespace(int=[<class 'int'>], str=[<class 'str'>, <class 'str'>])
   ~~~

* 'count' - 지정된 argument가 나타난 수를 저장. verbosity level을 지정하는데 유용
   ~~~python3
   >>> parser.add_argument('--verbose', '-v', action='count')
   >>> parser.parse_args('-vvv'.split())
   Namespace(verbose=3)
   ~~~

* 'help' - 모든 option에 대한 help message를 프린트하도록 함. 기본적으로 지정되어 있음.

* 'version' - version 정보를 프린트하도록 함. version keyword argument 사용
   ~~~python3
   >>> parser = argparse.ArgumentParser(prog='PROG')
   >>> parser.add_argument('--version', action='version', version='%(prog)s 2.0')
   >>> parser.parse_args('--version'.split())
   PROG 2.0
   ~~~

#### 2.1 사용자 정의 action
TBD

### 3. nargs

nargs keyword argument는 하나 이상의 command line argument가 한 action과 연관지음.

* N (an integer) - command line에서 N 개의 arguments가 list로 수집됨.
   ~~~python3
   >>> parser.add_argument('--foo', nargs=2)
   >>> parser.add_argument('bar', nargs=1)
   >>> parser.parse_args('c --foo a b'.split())
   Namespace(bar=['c'], foo=['a', 'b'])
   ~~~
   **nargs=1** 로 지정된 bar의 값도 list로 저장됨

* '?'

* '*'

* '+'

* argparse.REMAINDER

### 4. const


### 5. default


### 6. type


### 7. choices


### 8. required


### 9. help


### 10. metavar


### 11. dest

References
----------

* [Python Standard Library](http://docs.python.org/3.4/library/argparse.html)
