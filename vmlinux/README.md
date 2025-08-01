
# vmlinux

## 1. vmlinux란?

정의: 리눅스 커널 빌드 결과물 중 하나로, 링커(linker)에 의해 만들어진 압축되지 않은 커널 ELF 실행파일.

형식: ELF (Executable and Linkable Format)

용도:

- 디버깅 (GDB)
- 심볼 분석 (objdump, nm)
- 커널 모듈 로딩 시 심볼 참조
- eBPF 또는 ftrace 등에서 심볼 조회
- 실제로 부팅에 사용되는 이미지는 이 파일이 압축되거나 가공된 형태 (bzImage, zImage, etc).

## 2. vmlinux 파일의 내부 구성

vmlinux는 ELF 실행파일이기 때문에 다음과 같은 세그먼트/섹션들로 구성

### 주요 ELF 세그먼트 및 섹션

- .text : 커널 고드(함수, 루틴)
- .rodata : 읽기 전용 상수 데이터
- .data : 초기화된 전역 변수
- .bss : 초기화되지 않은 전역 변수
- .symtab : 커널 심볼 테이블 (디버깅용)
- .strtab : 심볼 이름 스트링 테이블
- .debug_* : 디버깅 정보 (GDB, DWARF 형식)
- .init.text, .exit.text : 커널 초기화/해제용 코드
- .kallsyms : 커널 심볼 목록 (주소 <-> 함수명 매)

### 예시 - readelf -S vmlinux 결과의 일부
```
  [Nr] Name             Type         Address           Offset
  [ 1] .text            PROGBITS     ffffffff81000000  000100
  [ 2] .rodata          PROGBITS     ffffffff82200000  1f0000
  [ 3] .data            PROGBITS     ffffffff82400000  400000
  [ 4] .bss             NOBITS       ffffffff82600000  600000
  [ 5] .symtab          SYMTAB       0000000000000000  800000
```
