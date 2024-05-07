---
Created by: Shudipto Trafder
Created time: 2024-04-04T16:21
Last edited by: Shudipto Trafder
Last edited time: 2024-04-04T16:21
---
```Python
from selenium import webdriver

from recruit.settings import BASE_DIR


class ChromeHelper:
    @staticmethod
    def get_chrome_driver() -> webdriver:
        options = webdriver.ChromeOptions()
        options.headless = True
        # options.add_argument("--incognito")
        options.add_argument('disable-infobars')
        options.add_argument('--disable-extensions')
        options.add_experimental_option(
            'excludeSwitches', ['enable-automation'])
        driver = webdriver.Chrome(executable_path=path, options=options)
        driver.maximize_window()
        return driver
```