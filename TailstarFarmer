from selenium import webdriver
from selenium.common.exceptions import UnexpectedAlertPresentException
from selenium.webdriver.support.ui import Select, WebDriverWait
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.alert import Alert
import requests
import time
import telegram
import re
import random

class TailstarFarmer:
    def __init__(self):
        self.driver = None
        self.bot = None
        self.chat_id = None

    def driver_init(self, _mode='local', _headless=False, _host=None):
        if _mode == 'local':
            from selenium.webdriver.chrome.options import Options
            options = Options()
            if _headless:
                options.add_argument('headless')
            self.driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)
        elif _mode == 'remote':
            from selenium.webdriver.firefox.options import Options
            options = Options()
            options.set_preference("general.useragent.override", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) "
                                                                 "AppleWebKit/537.36 (KHTML, like Gecko) "
                                                                 "Chrome/107.0.0.0 Safari/537.36")
            options.set_preference("general.platform.override", "Win32")
            self.driver = webdriver.Remote(_host, options=options)

    def bot_init(self, _token, _chat_id):
        self.bot = telegram.Bot(token=_token)
        self.chat_id = _chat_id
    
    def login(self, _uid, _passwd):
        # 로그인 페이지 이동        
        self.driver.get('https://tailstar.net/index.php?mid=main&act=dispMemberLoginForm')

        self.driver.find_element(By.XPATH, '//*[@id="uid"]').send_keys(_uid)  # 아이디 입력
        self.driver.find_element(By.XPATH, '//*[@id="upw"]').send_keys(_passwd)  # 비밀번호 입력
        self.driver.find_element(By.XPATH, '//*[@id="fo_member_login"]/fieldset/div[2]/input').click()  # 로그인 실행
        time.sleep(1)
                                                
        try:
            WebDriverWait(self.driver, 3).until(lambda driver: len(driver.window_handles) > 1)
            self.remove_popup()  # 팝업창 제거함수 호출
        except:
            pass  

    def check_login(self):
        # 마이페이지로 이동
        time.sleep(1)
        self.driver.get(url='https://tailstar.net/main')
        #time.sleep(1)
        # 인벤 팝업 포인트 열기
        _nickname = self.driver.find_element(By.XPATH, '//*[@id="header"]/div[1]/div/span[3]/a').text                
        if _nickname == _nick:
            _msg = f'{_nickname}님 테일스타 로그인 완료'
        else :
            _msg = f'{_nickname}님 테일스타 로그인 실패'
            
        return _msg



    def send_telegram(self, _msg):
        self.bot.sendMessage(chat_id=self.chat_id, text=_msg)        



    

if __name__ == '__main__':
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
    time.sleep(delay)
    farmer = TailstarFarmer()
    farmer.driver_init(driver_type, False , _host)
    farmer.bot_init(_token, _chat_id)  
    farmer.login(_uid, _passwd)
    farmer.check_login()
    result = farmer.check_login()
    print(result)
    farmer.send_telegram(result)   # 텔레그램 불필요시 비활성화
    farmer.driver.quit()
