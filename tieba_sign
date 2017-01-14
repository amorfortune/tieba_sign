#coding=utf-8
import requests
import re

headers = {
    'Cookie' : ''    #这里是你的cookie
}

def GetSession(headers):
    session = requests.session()
    session.headers.update(headers)
    return session


def GetHtml(session, url):
    session = requests.session()
    session.headers.update(headers)
    response = session.get(url)
    if response.status_code == 200:
        return response.text
    else:
        return ''


def GetFindall(pattern, html):
    pattern = re.compile(pattern)
    match = pattern.findall(html)
    if match is None:
        return ''
    else:
        return match

def GetSign(session, url):
    pattern = "'isSignIn':(\d),"
    html = GetHtml(session, url)
    sign = GetFindall(pattern, html)
    if len(sign) == 0:
        return ''
    return sign[0]

def MakeSign(session, kw):
    url = 'http://tieba.baidu.com/sign/add'
    data['kw'] = kw
    session.post(url, data=data)


if __name__ == '__main__':
    data = {
        'ie': 'utf-8',
        'kw': '',
        'tbs' : 'a1600351cafc31351484362942',
    }
    session = GetSession(headers)
    url_base = 'http://tieba.baidu.com'
    url = 'http://tieba.baidu.com/f/like/mylike'
    html = GetHtml(session, url)
    pattern = '<a href="(.*?)" title=".*?">(.*?)</a>'
    loves = GetFindall(pattern, html)
    for love in loves:
        url = url_base + love[0]
        name = love[1]
        sign = GetSign(session, url)
        tie = name.encode('utf-8')
        if sign == '': #贴吧被封
            continue
        if sign == '1':
            print tie + '   已经签到了'
            continue
        elif sign == '0':
            print tie + '   没有签到'
            print tie + '   开始签到'
            MakeSign(session, name)
            print tie + '   签到完成！！！'

