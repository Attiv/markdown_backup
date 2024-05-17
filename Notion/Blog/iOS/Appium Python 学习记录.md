- 基础配置
    
    ```Python
    from appium import webdriver
    from appium.webdriver.common.appiumby import AppiumBy
    from selenium.common.exceptions import NoSuchElementException
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC
    from selenium.webdriver.common.by import By
    import time
    
    
    desired_caps = {
        'platformName': 'iOS',
        'platformVersion': '16.4',
        'deviceName': 'iPhone 14',
        'app': '/Users/wanglikun/Downloads/Halo Fusion.app',
        'automationName': 'XCUITest',
        'autoAcceptAlerts': True,  # auto accept system dialog
    }
    ```
    
- 通过 `ACCESSIBILITY_ID` 找元素
    
    ```Python
    button_element = driver.find_element(AppiumBy.ACCESSIBILITY_ID, 'loginButton')
    button_element.click()
    ```
    
- 通过 `xpath` 找元素
    
    `settingPopButton = driver.find_element(AppiumBy.XPATH, "//XCUIElementTypeButton[@name='Setting']")`
    
- 等待直到某个元素出现
    
    `WebDriverWait(driver, 30).until(EC.presence_of_element_located((``[By.ID](http://by.id/)``, "icon setting")))`
    
- TestField 发送文本
    
    `usernameField.send_keys('text')`