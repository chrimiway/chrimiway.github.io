---
layout:     post
title:      Scraping courses review using selenium
subtitle:   a intro to how to use selenium
date:       2018-10-04
author:     Zhenhua Wang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - data scraping
---

1. Why chose selenium?
   When we try to scrape web pages, one of the biggest problem is how to deal with dynamicly produced contents (click a button, scroll down, etc.). Selenium give us the ability to simulate the entire browser. For instance, we would be able to automate the process of clicking, scrolling. For this reason, we could trick the website to get the information we need.

2. Preparations:
   Before we start to scrape website, we need to install the following software: pyhton, pip, selenium for python, firefox.

    One of the useful feature of python is virtualenv. We use virtualenv to create a 'virtual environment' for python. Therefore, the library for data scraping won't be conflict to our other libraries.

    ```sh
    virtualenv YOURENV
    ```

    In order to use the python in this new environment, we need to activate it first.
    ```sh
    source /path/to/YOURENV
    ```

    Now, you are in your virtual environment. You could then install selenium using pip.

    After data scraping, we may want to change back to our system environment.
    ```sh
    deactivate
    ```
3. now we are ready to scrape.
    we first need to load the libraries we needed.
    ```python
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    from time import sleep
    ```
    Then we could use selenium to open a Firefox bowser, which would be controlled by our codes instead of hand. Then, we could open the website that we want to scrape.

    ```python
    driver = webdriver.Firefox()
    driver.get("https://")
    ```

    The next step is locate the information we need on the website. We could use xpath or css selector to locate it. For example, we could right click the information we need, and in the menu we click 'inspect'[<8;84;26m]option. Then the browser would open the developer tools.

    ![alt text](https://github.com/chrimiway/chrimiway.github.io/blob/master/_posts/scraping/find_elem.png "locate information")

    Then you could right click the HTML node which you're interested. You then select copy -> copy XPath or copy css selector.

    ![alt text](https://github.com/chrimiway/chrimiway.github.io/blob/master/_posts/scraping/copy_xpath.png "copy xpath")

    After you successfully locate the information, you may tell your driver to find it.

    ```python
    info = driver.find_elements_by_xpath("YOUR XPATH HERE")
    info2 = driver.find_elements_by_css_selector("YOUR CSS SELECTOR HERE")
    ```
    other functions you may find useful:
        1. to find single element:
           find_element_by_id
           find_element_by_name
           find_element_by_xpath
           find_element_by_link_text
           find_element_by_partial_link_text
           find_element_by_tag_name
           find_element_by_class_name
           find_element_by_css_selector
        2. to find multiple elements:
           find_elements_by_name
           find_elements_by_xpath
           find_elements_by_link_text
           find_elements_by_partial_link_text
           find_elements_by_tag_name
           find_elements_by_class_name
           find_elements_by_css_selector

    One important fact is that your could find sub-element based on the element you already found.
    ```python
    subinfo = info.find_element_by_xpath("XPATH")
    ```
    You could also trigger events on elements. For example you may want to click a button
    ```python
    button.click()
    ```

    Another example is that you want to scroll your page or an element to the bottom
    ```python
    elem.send_keys(Keys.END)
    ```

    At the end, your may want to collect your data.

    ```python
    text = info.text
    ```

    or

    ```python
    text = info.getAttribute("value")
    ```
