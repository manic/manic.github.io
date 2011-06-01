---
title: 如何在 64 位元 Ubuntu 下安裝 Juniper Networks VPN Client
layout: post
---

參考 [這邊](http://devinfee.com/blog/2011/03/22/how-to-juniper-networks-vpn-on-64-bit-ubuntu) 寫出來的心得

1.  新增軟體來源

    增加 Canonical 的 'partner' 套件

    ![軟體來源](http://pic.pimg.tw/manic/1d676ab9f558c6b92ca25f78f6d093d7.png)

2.  執行 sudo apt-get install ia32-sun-java6-bin

3.  到你的客戶端 Juniper Networks VPN site 進行登入

4.  執行 Network Connect

    ![Network Connect](http://pic.pimg.tw/manic/873af0f1d27717f316275b02674de53f.png?v=1304151738)

5.  執行 4. 後會下載 ncLinuxApp.jar, 請允許他下載, 會放到 ~/.juniper\_networks 底下，此時會有要求輸入密碼的要求。

6.  執行
        wget http://mad-scientist.net/junipernc
        chmod 755 junipernc
        sudo cp junipernc ~/bin/

7.  執行 junipernc 並輸入需要的資訊

    ![輸入你的 VPN Site Name](http://pic.pimg.tw/manic/0f7bd31a0640b9b15a91248aba1bedfe.png?v=1304152755)

    輸入你的VPN SITE NAME

    ![Account](http://pic.pimg.tw/manic/6857ac41621de302adca439c46ae059e.png?v=1304152755)

    ![Realm](http://pic.pimg.tw/manic/b5585b7fb3b3a7b6883626427b08230e.png?v=1304152755)

    ![Alert JAVA](http://pic.pimg.tw/manic/ca3e31bb39df878f4d8dbebfd75d5556.png?v=1304152755)

    ![ia32-java-6-sun](http://pic.pimg.tw/manic/53d63a34e8feb65a97a6b1a2d7a07e5f.png?v=1304152755)

    請選擇 ia32-java-6-sun

    ![Password](http://pic.pimg.tw/manic/75fcce2f4a675272afcdef5cf944acd6.png?v=1304152755)

    ![OK](http://pic.pimg.tw/manic/3803f1ee4da0b23f83a960603b55cf84.png?v=1304152755)

