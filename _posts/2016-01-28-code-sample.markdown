---
layout: post
title:  "Code Block Sample Test"
date:   2016-01-28 00:25:00 +0800
categories: javaee
tags: [javaee, spring]
---

Test Java with markdown block

~~~ java

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

~~~

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
