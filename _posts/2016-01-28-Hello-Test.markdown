---
layout: post
title:  "Hello Jekyll!"
date:   2016-01-28 11:37:00 +0800
categories: jekyll update
tags: [github, github-pages, jekyll]
---
想架一個寫技術Note的文件很久了 , 但一直沒找的一個容易維護+免費+有code format的地方.
曾經試過Google 協作平台 , openshift+wordpress , 但都沒有很滿意.
希望這邊應該是可以讓我養成習慣的好地方.
----

Test Java with markdown block
```
@Data
@Entity
@Table(name = "user")
@EqualsAndHashCode(of = "sid")
@ToString(of = {"sid","id","name"})
@XmlRootElement
public class User implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Basic(optional = false)
    @Column(name = "UserSID")
    private Integer sid;
    @Column(name = "Status")
    private Integer status = 0;
    @Column(name = "PrimaryOrgSID")
    private Integer primaryOrgSID;
    @Basic(optional = false)
    @NotNull
    @Size(min = 1, max = 45)
    @Column(name = "DX_UserID")
    private String id = "";
    @Size(max = 45)
    @Column(name = "UserName")
    private String name = "";
    @Size(max = 36)
    @Column(name = "UUID")
    private String uuid = "";

    public User() {
    }

    public static User getEmptyDefault() {
        return new User();
    }

}

```

Test Java with jekyll highlight
{% highlight java %}

@Data
@Entity
@Table(name = "user")
@EqualsAndHashCode(of = "sid")
@ToString(of = {"sid","id","name"})
@XmlRootElement
public class User implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Basic(optional = false)
    @Column(name = "UserSID")
    private Integer sid;
    @Column(name = "Status")
    private Integer status = 0;
    @Column(name = "PrimaryOrgSID")
    private Integer primaryOrgSID;
    @Basic(optional = false)
    @NotNull
    @Size(min = 1, max = 45)
    @Column(name = "DX_UserID")
    private String id = "";
    @Size(max = 45)
    @Column(name = "UserName")
    private String name = "";
    @Size(max = 36)
    @Column(name = "UUID")
    private String uuid = "";

    public User() {
    }

    public static User getEmptyDefault() {
        return new User();
    }

}
{% endhighlight %}

----

架設過程還是有遇到一些狀況 , 一直到參考github page的document才架起來
[GitHub Page](https://help.github.com/articles/using-jekyll-with-pages/)
https://help.github.com/articles/using-jekyll-with-pages/
