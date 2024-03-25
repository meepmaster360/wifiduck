# wifiduck
WifiDuck payloads

YouTube
1. Open Google Chrome
2. Wait for Chrome to open (Delay: 2 seconds)
3. Press Enter (to confirm the selection of Chrome)
4. Wait for Chrome to fully load (Delay: 2 seconds)
5. Press Alt + D (to focus on the address bar)
6. Wait for the address bar to be focused (Delay: 2 seconds)
7. Type the URL "https://www.youtube.com/watch?v=xvFZjo5PgG0"
8. Press Enter

In Python:
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

# Open Chrome
driver = webdriver.Chrome()

# Wait for Chrome to open
time.sleep(2)

# Open YouTube link
driver.get("https://www.youtube.com/watch?v=xvFZjo5PgG0")

#########################################################
