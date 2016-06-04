Recently, I created a crawler and wanted to run it 24/7. So let it run on cloud seems like a good solution. The solution below
works on Ubuntu 14.04, which is Heroku base OS; if you decide to work with other provider(aws, dedicated hosting, ...) you can easily
install Ubuntu 14.04

First, install Google Chrome for Debian/Ubuntu:

```
sudo apt-get install libxss1 libappindicator1 libindicator7
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome*.deb
sudo apt-get install -f
```

Now, let’s install xvfb so we can run Chrome headlessly:
```
sudo apt-get install xvfb
```

Install ChromeDriver
```
sudo apt-get install unzip
wget -N http://chromedriver.storage.googleapis.com/2.21/chromedriver_linux64.zip
unzip chromedriver_linux64.zip
chmod +x chromedriver
sudo mv -f chromedriver /usr/local/share/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
```

My spider is based on scrapy so I have to install Python dependencies for scrapy & Selenium:
```
sudo apt-get install python-pip
# if you desire to use scrapy, you also need to install dependencies for scrapy
# sudo apt-get install python-dev python-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev
# pip install Scrapy
pip install pyvirtualdisplay selenium 
```

Now, we can do stuff like this with Selenium in Python:
```
from pyvirtualdisplay import Display
from selenium import webdriver

display = Display(visible=0, size=(800, 600))
display.start()
driver = webdriver.Chrome(executable_path = "path/to/chromedriver")
driver.get('https://www.google.com')
print driver.title
```
