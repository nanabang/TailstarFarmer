# TailstarFarmer
사용자 변경 부분

코드 87줄 하단에 보면 아래와같이 있는데 

셀레니움remote 이 따로 있으면 주소를 넣고 driver_type 을 remote 로 하고  local에서 진행시 local로 변경한다.

테일스타 아이디,비번, 텔레그램토큰,아이디 를 넣고 1~120초 의 딜레이를 넣었으니 변경이 필요하다면 변경하면 된다.


_host = 'http://127.71:4444/wd/hub'  # Selenium Remote 주소
_uid = ''  # 테일스타 아이디
_passwd = ''  # 테일스타 비밀번호
_token = ''  # 텔레그램봇 토큰
_chat_id = ''  # 텔레그램 전송받을 챗아이디
_nick =  '' # 테일스타 닉네임

driver_type = 'remote'
#driver_type = 'local'
delay = random.randint(1,120)
print(f'{delay} 초 랜덤 딜레이')
