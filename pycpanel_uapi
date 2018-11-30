__title__ = 'pycpanel_uapi'
__version__ = '0.0.1'
__date__ = '2018-11-30'
__licence__ = 'Apache License Version 2.0'
__author__ = 'myuksektepe'

import requests

def unauthorised():
    raise Exception('Access denied:  Please check the username and password.')

class connect(object):
    def __init__(self, hostname, username, password, ssl=True):
        self.url = ""
        self.securityToken = ""
        self.authorised = None
        self.username = username
        self.password = password
        self.ssl = ssl
        self.__session__ = requests.Session()

        # CREATE HOST URL
        if ssl:
            self.hostname = 'https://' + str(hostname) + ':2083/'
        else:
            self.hostname = 'http://' + str(hostname) + ':2082/'

        # CHECK AUTHORIZATION
        data = {
            'user': self.username,
            'pass': self.password
        }
        r = self.__session__.post(self.hostname + "login/", data)
        if r.status_code == 200:
            self.authorised = True
            self.url = r.url
            self.securityToken = self.url.split("/")[3]

    def check(self):
        if self.authorised:
            return True
        else:
            unauthorised()
            return False

    def getSecurityToken(self):
        if self.securityToken:
            return self.securityToken
        else:
            unauthorised()

    def doit(self, module=None, function=None, parameters=None):
        if self.check():
            if not module:
                raise Exception('Module cannot be empty!')
            elif not function:
                raise Exception('Function cannot be empty!')
            else:
                url = self.hostname + self.securityToken + "/execute/" + module + "/" + function
                if not parameters:
                    r = self.__session__.get(url)
                else:
                    r = self.__session__.get(url, params=parameters)
                return r.text
        else:
            unauthorised()

    def logout(self):
        self.__session__.post(self.hostname + "logout/")
