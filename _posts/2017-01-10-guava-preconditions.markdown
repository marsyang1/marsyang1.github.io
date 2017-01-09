---
layout: post
title: Guava的Preconditions
date: '2017-01-10 00:20:00 +0800'
categories: java
tags:
  - java
  - guava
---

最近的工作幾乎都在重構專案 , 不管是前台還是後來. 舊專案重構專案的工作一開始 , 我幾乎都會直接放入幾個Library.

- joda-time
- guava
- gson(看情況)

joda-time 就算專案的JDK拉到8, 還是可以考慮放入 , 因為實在太常需要做 toDate()的動作. Guava可以用的就更多了. 例如Preconditions

範例舊code

~~~ java
public class UserService{

    ...

    public String updatePhone(String loginName,String phone){
      User user  = userDao.find(loginName);
      if(user == null){
         return "帳號不存在";
      }
      user.setPhone(phone);
      userDao.update(user);
      return "";

    }
}
~~~

上面是目前我處理專案最常看到的樣子 , 先不管直接回傳字串的問題. 如果用Preconditions來處理 if判斷的話 , 會變成

~~~ java
public class UserService{

    ...

    public String updatePhone(String loginName,String phone){
      try{
        User user  = userDao.find(loginName);
        Preconditions.checkState(user != null,"帳號不存在");
        user.setPhone(phone);
        userDao.update(user);  
      } catch(IllegalStateException ise){
        return ise.getMessage();
      }
    }

}
~~~

但大部分會改成直接拋出Exception , 變成

~~~ java
public class UserService{

    ...

    public String updatePhone(String loginName,String phone) throw IllegalStateException {
        User user  = userDao.find(loginName);
        Preconditions.checkState(user != null,"帳號不存在");
        user.setPhone(phone);
        userDao.update(user);
    }

}
~~~

Exception的handle 交給最外層處理.最近幾乎只要是PreCheck的部分 , 我都直接改用Preconditions處理.

用Preconditions好處

1. 檢查規則同向化. 避免if( xx == xx) or if(xx != xx)的混淆困擾.
2. Exception統一化 , 而且是使用標準的JavaSE Exception.
3. IllegalStateException 這個Exception滿好用的, 不太會跟Library衝到混淆.
4. if三行變一行, 越多if少越多行.

----

後記

有一個教了一陣子的學弟 , 最近跟我說他打算改找Node.JS的工作了. 台中的Java工作缺不是很理想.
聽了很感慨,但目前我也沒什麼可以幫他的了,只能祝他找工作順利.有機會再多多討論, 畢竟這年頭 , 什麼都要會.
