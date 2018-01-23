Q1:大量爬虫的时候怎么避免被封IP：
1. 有钱的就多拿几个c段，在段内NAT，随机ip/port出
2. 没钱的proxy，淘宝上似乎能买proxy，就是http的 
3. 上算法，探测对方的prison策略。
4. 最后就是自己的抓取，随机一点
        header拼写方法、顺序随机，process time随机，抓取间隔不要太固定。
        agent长得像浏览器最好，带假cookie最好，爬取顺序类似人类浏览最好
 
Q2:如何打包发布呢？
1.pyinstaller，打包成exe
2.python wsgi挂apache下
3.setuptools
4.docker