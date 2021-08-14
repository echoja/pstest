# 42 Piscine test tools

42 피신 테스트 툴입니다.

## SHELL

서브젝트 폴더에 해당 스크립트 파일을 복사하여 넣고 `bash run.sh`로 실행시킵니다.

## C

### 기본 사용법

- 해당 서브젝트의 최상위 폴더에 ``test_cxx_gen` 파일을 복사하여 붙여넣습니다.
- `bash run.sh` 로 쉘 스크립트를 실행시킵니다. 

### 유의사항

- 아래 사항이 지켜져야 테스트가 올바로 작동합니다.
  - ex00, ex01 등의 문제 폴더 안에 소스파일이 하나만 존재해야 합니다.
  - 소스파일 이름과 함수 이름이 일치해야 합니다. 
- 테스트를 실행을 하게 되면 `src` 폴더와 `build` 폴더가 자동으로 생성되며 필요한 파일들이 추가적으로 생성됩니다. 이 파일/폴더들은 오직 테스트를 위한 것이기 때문에 언제든지 삭제해도 무방합니다.
- 프로그램에 결함이나 오류가 있을 수 있으므로 본인이 작성한 소스코드는 관리를 잘해주세요. 삭제하거나 옮기는 기능을 최대한 지양했지만 불상사는 언제든 생길 수 있습니다...
- 테스트 용도로만 이용해주시기 바랍니다. 평가 시에는 보조적으로만 이용하시고 코드를 살펴보는 걸 중점적으로 진행하면 좋을 것 같습니다.
- 기타 문의는 이슈를 남기거나 eszqsc112@gmail.com 으로 연락주세요.

### 부가 옵션

옵션을 추가하여 테스트의 동작을 더 세밀하게 지정할 수 있습니다. 

- `-c` : 컴파일 및 실행만 수행합니다. (플래그 설정 되어있음)
- `-n` : norminette만 수행합니다. (플래그 설정 되어있음)
- `-{숫자}` : `ex{숫자}`만 테스트를 수행합니다. (옵션으로 넣는 숫자는 앞에 0이 없어야 합니다.) (예: `-4` 로 해야 `ex04`의 테스트를 진행함)

예시 (위 이미지에서 c03 폴더에 터미널을 켰다고 가정)

- `bash asdf/run.sh -4 -c` : ex04만 컴파일하여 수행 (norminette 검사 수행하지 않음)

### test_c_template

- test_c_template 란 테스트를 생성하기 위한 도구를 모아놓은 것입니다. 서브젝트마다 테스트의 구조가 크게 다르지 않기 때문에 새로운 서브젝트의 테스트를 만들 때마다 이 test_c_template 으로부터 새 테스트를 만들어나가면 됩니다.
- `run.sh` 파일은 테스트가 동작하는 로직이 담겨져 있고, `testcode` 에는 실제로 테스트를 수행할 코드와 기대되는 결과값 등이 작성되어 있습니다.
- `testcode` 수정법
  - 공간은 `레이블:` 로 구분됩니다.
  - include: #include 할 헤더들의 목록입니다.
  - ex숫자: 해당 ex문제에서 실행할 코드입니다. ( >= 0.2) 프로그램을 실행시키는 과제일 경우, 즉 main 함수가 포함되어 있는 경우에는 해당 코드는 모두 명령 실행모드로 됩니다. 이 때, ;로 명령어를 구분하면 됩니다.  test 명령은 자동으로 해당 코드의 목적 파일 이름으로 대체됩니다. (예: test 1 2 3 ; test 4 5 6: 해당 프로그램을 실행시키는데, 첫 번째에는 1, 2, 3을 인수로 넘기며, 두 번째 실행에는 4, 5, 6을 인수로 넘깁니다.)
  - ex숫자-expected: 테스트 기댓값으로 나오는 평문입니다. 코드랑은 아무런 관계가 없고, 텍스트 그대로 출력됩니다. 중요한 곳은 아닙니다.
  - end: `testcode`의 끝을 나타냅니다.

## 변경 이력

`2020. 7. 15.`

- c02 업데이트 (run.sh 파일 갱신, ex01 잘못된 테스트 코드 수정)
- c03 업데이트 (run.sh 파일 갱신)
- c04 업데이트 (run.sh 파일 갱신)
- c05 업데이트 (run.sh 파일 갱신)
- (0.3) main 외부에 선언할 것 testcode에 지정할 수 있도록 하기. (ex00-other: 레이블 활용)
- 컴파일 실패 유무에 따라 파일 실행시키기/실행시키지 않기 기능 추가 (컴파일이 되지 않음에도 가장 최근에 성공한 실행 파일이 실행되는 문제 해결)
- (0.3) Exercise 폴더 내에 있는 모든 .c 파일을 읽어서 구현된 함수에 대하여 선언부를 자동으로 추가하도록 함. (소스 파일이 여러 개일 때 동작하지 않던 문제 해결)
- (0.3) .c 파일을 제외한 파일은 무시됨. (폴더에 상관 없는 파일들이 포함되어 있을 경우 제대로 동작하지 않던 문제 해결)

`2020. 7. 14.`

- c06 최초 업로드
- c05 최초 업로드

`2020. 7. 13.`

- C 과제 테스트용 스크립트 run.sh 파일을 다소 개선했습니다.
  1. 재귀함수 등이 존재할 때 테스트 코드가 잘 작성되지 않던 문제 수정
  2. 프로그램을 만드는 과제일 때 (소스 파일 내에 main 함수 선언이 되어있을 시) 자동으로 인식하여 테스트코드를 c코드가 아닌 터미널 명령어로 인식하여 명령어 실행. (자세한 사용법은 안내 참조)

## 이슈

- norminette 3.0 대응 미비
- 헤더 파일 (`.h`)을 읽지 못함. (c08 이후는 다소 제한됨)
- Makefile 관련 기능 없음.
- c03-ex02 테스트코드에서 처음 배열을 초기화하는 과정에서 쓰레기값이 들어가있을 수 있는 문제 (mosong 제보)
- 소스 파일이 여러 개이거나 `ex..` 폴더에 상관 없는 파일들이 포함되어 있을 경우 제대로 작동하지 않음