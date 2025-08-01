
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

- 주요 ELF 세그먼트 및 섹션
-- .text : 커널 고드(함수, 루틴)
