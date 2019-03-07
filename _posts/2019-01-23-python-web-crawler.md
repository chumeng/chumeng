---
layout: post
title: "Python 简单网页爬虫"
date: 2019-01-23
excerpt: ""
Coding: true
tags: [Python, Web Crawler]
comments: true
---

### 方法1 手动保存网页，BeautifulSoup解析源码

1. Chrome安装[Save As MHT](https://chrome.google.com/webstore/detail/save-as-mht/hfmodljjaibbdndlikgagimhhodmobkc?hl=zh-CN&utm_source=chrome-ntp-launcher)插件

2. 将要爬取的页面保存为MHT，用Chrome打开，查看源代码，复制源码，保存为HTML

3. 将HTML放到和代码同一文件夹，运行
{% highlight python %}
import re
from bs4 import BeautifulSoup as bs

with open('helloworld.html', encoding='utf-8') as f:
    helloworld = f.read()
soup = bs(helloworld, 'html.parser')
soup_all = soup.find_all('p', {'class':'~~~'})
for i in soup_all:
    print(i.text)
{% endhighlight %}

### 方法2 Selenium配合BeautifulSoup

#### 准备工作

* 下载自己电脑对应chrome版本的chromedriver
* 安装selenium包

{% highlight python %}
from selenium import webdriver
import time
from bs4 import BeautifulSoup
driver = webdriver.Chrome('[此处填写详细路径\\chromedriver.exe]')
# driver.get('https://sou.zhaopin.com/?jl=489&kw=django&kt=3')
for i in range(2,3):
    link = "https://sou.zhaopin.com/?p=%s&jl=489&kw=c&kt=3"
    driver.get(link % i)
    # driver.fullscreen_window()
    driver.find_element_by_xpath("//div[@class='risk-warning__content']//button").click() #点击警示框
    time.sleep(5)
    src = driver.page_source
#     print(src)
    with open('智联招聘.html', 'w', encoding='utf-8') as f:
        f.write(src)
    soup = BeautifulSoup(src, 'html.parser')
#     print(soup)
    with open('智联招聘Soup.html', 'w', encoding='utf-8') as f:
        f.write(soup.text)
    atag = soup.find_all('div', {'class':"contentpile__content__wrapper__item clearfix"})
#     print(atag)
    for i in atag:
    #     print(i)
        print('-'*40)
        print(i.find('span').text)
        print(i.find('a', {'class':"contentpile__content__wrapper__item__info__box__cname__title company_title"}).text)
        print(i.find_all('li', {'class':"contentpile__content__wrapper__item__info__box__job__demand__item"})[0].text)
        print(i.find_all('li', {'class':"contentpile__content__wrapper__item__info__box__job__demand__item"})[1].text)
        print(i.find_all('li', {'class':"contentpile__content__wrapper__item__info__box__job__demand__item"})[2].text)
        print(i.find('span', {'class':"contentpile__content__wrapper__item__info__box__job__comdec__item"}).text)
        print(i.find_all('span', {'class':"contentpile__content__wrapper__item__info__box__job__comdec__item"})[1].text)
    #     print(i.find('div', {'class':"contentpile__content__wrapper__item__info__box__welfare__item"}).text) #福利 待完善 有时会报错

        print('-'*40)
    
#     time.sleep(3)
#     driver.find_element_by_xpath("//div[@class='risk-warning__content']//button").click()
{% endhighlight %}

* 尽量不要使用time.sleep(),影响爬虫速度

In pug Portland incididunt mlkshk put a bird on it vinyl quinoa. Terry Richardson shabby chic +1, scenester Tonx excepteur tempor fugiat voluptate fingerstache aliquip nisi next level. Farm-to-table hashtag Truffaut, Odd Future ex meggings gentrify single-origin coffee try-hard 90's.

* Sartorial hoodie
* Labore viral forage
* Tote bag selvage
* DIY exercitation et id ugh tumblr church-key


## Forage occaecat cardigan qui

Fashion axe hella gastropub lo-fi kogi 90's aliquip +1 veniam delectus tousled. Cred sriracha locavore gastropub kale chips, iPhone mollit sartorial. Anim dolore 8-bit, pork belly dolor photo booth aute flannel small batch. Dolor disrupt ennui, tattooed whatever salvia Banksy sartorial roof party selfies raw denim sint meh pour-over. Ennui eu cardigan sint, gentrify iPhone cornhole.

> Whatever velit occaecat quis deserunt gastropub, leggings elit tousled roof party 3 wolf moon kogi pug blue bottle ea. Fashion axe shabby chic Austin quinoa pickled laborum bitters next level, disrupt deep v accusamus non fingerstache.

## Hoodie Duis

Actually salvia consectetur, hoodie duis lomo YOLO sunt sriracha. Aute pop-up brunch farm-to-table odio, salvia irure occaecat. Sriracha small batch literally skateboard. Echo Park nihil hoodie, aliquip forage artisan laboris. Trust fund reprehenderit nulla locavore. Stumptown raw denim kitsch, keffiyeh nulla twee dreamcatcher fanny pack ullamco 90's pop-up est culpa farm-to-table. Selfies 8-bit do pug odio.

### Thundercats Ho!

Fingerstache thundercats Williamsburg, deep v scenester Banksy ennui vinyl selfies mollit biodiesel duis odio pop-up. Banksy 3 wolf moon try-hard, sapiente enim stumptown deep v ad letterpress. Squid beard brunch, exercitation raw denim yr sint direct trade. Raw denim narwhal id, flannel DIY McSweeney's seitan. Letterpress artisan bespoke accusamus, meggings laboris consequat Truffaut qui in seitan. Sustainable cornhole Schlitz, twee Cosby sweater banh mi deep v forage letterpress flannel whatever keffiyeh. Sartorial cred irure, semiotics ethical sed blue bottle nihil letterpress.