---
title: bash를 파보자
date: 2021-02-09 23:02:93
category: development
draft: false
---

## bash의 기초!

#### Mac에서 터미널 실행하기

space + command => 터미널 검색해서 실행

#### 리눅스 간단 명령어

##### ls

디렉터리의 컨텐츠 리스트를 보여준다!

예를 들어 ls/home 경우 =>/home 디렉터리의 모든 컨텐츠를 보여준다.

현재상황에서 ls를 사용하면 현재 디렉터리의 콘텐츠를 보여준다!

- -l: 더많은 추가정보를 볼 수 있음!
- -a: 숨겨진 파일도 볼 수 있음!

ls > output.txt => 현재 디렉토리에 output.txt 만듬!

##### echo

내가 입력한 것을 보여주거나, 간단한 파일도 만들 수 있다.

echo "This is a test" > test_1.txt => This is a test 내용의 test_1 txt 파일을 만든다 라는 의미!

##### cat

파일을 볼 수있다!

cat test*1.txt == cat test*?.txt == cat test\_\_\*

cat t\* > combined.txt => t로시작하는 파일들의 내용을 합쳐 combined.txt에 저장!

기본적으로 cat > combinded.txt => 덮어쓰기 되는데..

=>

#### pwd

pwd 커맨드는 현재 실행주인 디렉터리와, 현재 실행줄인 디랙터리 이름을 보여준다 즉, 내가 어디있는지 알수 있다.

#### cd

cd는 디렉터리 바꾸기 할 수있음!

현재 내가 /home/lszhu에 있고, /etc/로 바꾸고 싶다면 cd /etc

cd ~/Desktop == cd/home/Iszhu/Desktop : ~/는 나의 홈 디렉토리에서 시작한다 라는 의미

cd \$HOME : home 디렉토리로 이동

#### rm

rm은 파일과 디렉터리를 지울때 사용한다. 예를 들어 rm ./foo.txt => 현재 디렉터리의 foo.txt를 지우는 것을 으미힌다. -r : recursive재귀를 의미

rm -r./test => test라는 이름의 파일과 그 아래 파일을 모두 지운다.

##### rmdir

디렉터리를 지울때 사용한다.! 비어있는 폴더만 지운다!

##### clear

현재 커맨드 라인들을 지워준다.

##### mv

파일을 이동할 경우 사용한다.

mv./test/var => 파일을 test에서 var로 이동

mv./test./foo => test 이름을 foo로 이름 변경이가능하다.

mv dir1/\* . => dir1의 모든 폴더를 부모페이지로 이동한다.

mv combined.txt test\_\* dir3 dir2 => dir2 안으로 combined.txt test로시작하는 파일, dir3모두 이동

mv backup_combined.txt combined_backup.txt => 이름 변경 가능!

mv tt .tt => tt는 .tt로 히든 폴더로 변경이 가능하다!

##### mkdir

새로운 디렉터리를 만들때 사용한다.

mkdir /home/Iszhu/test_dir => /home/Iszhu 디렉터리에 test_dir새로운 디렉터리 추가를 의미한다.

mkdir dir1 dir2 dir3 => 현재 디렉토리에 dir1, dir2, dir3를 만든다

mkdir -p dir4/dir5/dir6 => dir4폴더안에 dir5 폴더안에 dir6을 만든다.

##### cp

파일이나 디렉터리 복사할 경우 사용

cp ./scst.conf /var => scst.conf 파일을 디렉터리 var에 복사한다.

cp -r./test/var => test디렉터리를 복사해서 var에 붙여넣는 것을 의미한다.

cp combined.txt backup_combined.txt => combined.txt를 복사해서 backup_combined.txt 파일을 만든다

#### su

su커맨드는 superuser로 변경하는 것을 바꿔준다. 슈퍼유저는 시스템유저로 관리자 업무를 수행할 수 있는 유저를 의미

sudo poweroff => 컴퓨터를 끌 수 있다.

sudo reboot => 컴퓨터 리부팅

##### man

mas ls => 메뉴얼 볼 수 있음

##### less 와 more

less cobined.txt => 딱 cobined의 파일 내용만 표시 q로 탈출가능

more cobined.txt => 현재화면에서 추가로 파일내용을 보여줌!
