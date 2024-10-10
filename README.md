# 예외(Exception) 처리

# ** 예외
#  - 프로그램을 개발하면서 예상하지 못한 상황
#    ex) 사용자 입력 오류
#  - 예외가 발생하면 프로그램이 종료됨!(크리티컬 상황)
#    → 예외처리를 하면 예외가 발생해서 동작 가능
#  - 예외처리는 의무는 아님!(개발자 마음)
#    → 파일시스템과 데이터베이스는 반드시 예외 처리!

# ※ 예외상황은 사용자로부터 많이 발생!
#  ex) "-없이 전화번호를 입력하세요."
#       사용자1: 010-1234-1234 → 정규식
#       사용자2: 010-1234-ㄷㄷㄷ
#       사용자3: 111-1111-1111
#       개발자 : 01012341234

#  → 유효성 체크: 사용자가 입력한 값에 대한 체크
#      1. 확장자 체크
#      2. 파일이름 체크
#      3. 파일 사이즈 체크


# ** 예외의 종류
#  1. 예측 가능한 예외
#   - 발생 여부를 개발자가 사전에 인지 → 예외 처리
#  2. 예측 불가능한 예외
#   ex) 카카오톡 서버에 화재로 인해 카카오톡 서비스 중지!

# 번외.
# ※ 정부통합전산센터
#  1. 메인(대전)
#  2. 서브1(광주)
#  3. 서브2(대구)


#  ** 개발자 취업
#   1. SI(시스템 통합)
#       - 회사 자체 프로그램 개발 x
#       - 사업을 수주 → 사업 관련 프로그램 개발
#         하드웨어 + 소프트웨어
#   2. 솔루션
#       - 회사 자체 프로그램(당근, 한글과컴퓨터, ...)

# SI 기업
#  1. "정부통합전산센터" 사업 발주 
#     → "2024년도 데이터 이전 사업", 1년, 20억
#  2. 다수의 기업들이 사업제안서 참여!
#     → 심사를 통해서 회사 선별
#  3. 선별(중견 기업)
#     → 대신정보통신(400명)
#         ↓
#       1하청업체
#         ↓
#       2하청업체
#         ↓
#       3하청업체
#  4. 정부통합전산센터 사무실 → 해당 사업 방을 만들고
#     → 대신, 1하청, 2하청, 3하청 : 1년동안 개발   


# 1. 예외 기본 문법
#try:
#    예외가 발생할 수 있는 코드
#except:
#    예외 처리
#else:
#    예외가 발생하지 않은 경우 실행되는 코드
#finally:
#    예외 유무와 상관없이 실행되는 코드

# else, finally는 생략 가능

from urllib.request import urlopen, HTTPError
# except HTTPError: → 예외 중 HTTPError 관련 예외만 처리

# except HTTPError: → 다수의 예외 처리
# except Error:
# except Error:

#except: → 모든 예외 처리
#try:
#    html = urlopen("http://www.naver.com")
#except HTTPError as e:
#    print(e)    #예외처리 x, 예외 관련 내용을 출력
#else:
#    print("No Error")
#finally:
#    print("지원해제")
    
try:
    html = urlopen("http://www.naver.com")
except:
    print("올바른 URL을 입력해주세요.")    #예외처리
else:
    print("No Error")
finally:
    print("지원해제")

from datetime import datetime, timedelta
import time

# 1. 날짜 포맷팅(원하는 형식으로 날짜 출력)
now = datetime.now().strftime("%Y년%m월%d일 %H시%M분%S초")
print(now)

# 2. 날짜 계산(현재 시간에서 13시간 빼기)
now = datetime.now()
before_time = (now - timedelta(hours=13))
print(before_time)

# 3. 실행시간 계산
start_time = time.time()
# → 실행코드(시간을 알고 싶은)
end_time = time.time()
execution_time = end_time - start_time
print(f"실행시간: {execution_time}"초)

# 스제쥴러
#  - 일정시간에 반복저으로 동작해야하는 작업을 등록 사용
#  ex) 12시간에 한번씩
#      매일 자정 한번씩
#      5분에 한번씩
#      매월 1일 자정에 한번씩
#      → CRON 표기법

# 스케쥴러 종류
#  1. scheduler
#      → 매우 쉬움, 기능이 약함
#  2. apscheduler 
#      → 매우 쉬움, 기능이 강함\
    
from apscheduler.schedulers.blocking import BlockingScheduler
from apscheduler.schedulers.background import BackgroundScheduler

# 백그라운드 스케쥴러
#  - 메인 작업이 있어야만 동작
#  - 백그라운드 즉 서브로 동작하기 때문에

# 메인
# while True
#   print("test")
# 서브
#  - 스케쥴러 실햄

# 1. 스케쥴러 생성
# sched = BlockingScheduler()
sched = BackgroundScheduler()

# 2. 할 일 생성
def print_hello():
    print("Hello")
    
# 3. 스케쥴러 할일 등록
sched.add_job(print_hello, "cron", hour="17",minute="26",id="chosun")

# 4. 스케쥴러 실행
sched.start()

while True:
    print("test")
