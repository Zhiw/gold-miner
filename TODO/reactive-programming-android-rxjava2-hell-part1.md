> * 原文地址：[Observer Pattern – Reactive Programming [Android RxJava2]\( What the hell is this ) Part1](http://www.uwanttolearn.com/android/reactive-programming-android-rxjava2-hell-part1/)
* 原文作者：[Hafiz Waleed Hussain](http://www.uwanttolearn.com/author/admin/)
* 译文出自：[掘金翻译计划](https://github.com/xitu/gold-miner)
<<<<<<< Updated upstream
* 译者：[Zhiw](https://github.com/Zhiw)
* 校对者：[dubuqingfeng](https://github.com/dubuqingfeng)，[Vivienmm](https://github.com/Vivienmm)

## 观察者模式 – 响应式编程 [Android RxJava2]（这到底是什么）：第一部分

哦，我们又过了一天，是时候来学习新东西让这一天变得很棒了🙂。

大家好，希望你们做的更好。今天我打算开始一个关于 Rx Java2 的新系列，但是首先的 2-3 篇文章是关于响应式编程的。希望我们能够学到新的东西，然后一起消除所有的困惑。

**动机：**

说实话，我一开始学习 Rx 的时候遇到了许多问题。我尝试了许多教程、书籍，但是最后我都无法在我的应用里面使用 Rx。许多教程让我感到很困惑，就像有些部分说，迭代器模式是基于拉模式（Pull），同样的，Rx 是基于推模式的（Push），并且给了一些例子，但那对于我来说毫无用处。我想学习 Rx，我想了解它的好处，我想知道它如何将我从大量的 bug 和冗长鸡肋的代码中拯救出来。但是每次我都会得到关于推和拉的比较，有些时候则是命令式和响应式的比较，我从来都得不到我想要的真正的 Rx 的答案。在一些文章中作者提到，Rx 就像观察者模式。随着时间的流逝，疑惑越来越多，学习曲线变得很困难。后来我得到一些关于 FRP (译者注：Functional Reactive Programming，函数式响应性编程)，lambda 表达式和函数式编程的一些教程。我看到一些例子，他们使用 lambda 表达式来调用 map，filter 等函数。
但我依然待在原地，我还是不知道 Rx 是什么以及我为什么要选择它。后来我遇到了使用 Rx 的朋友，我就问他们能否指导一下如何使用 Rx。他们是这样教我的：你知道我们有一个 EditText，如果你想检查用户是否输入了新文本，你用什么方法得知？我回答说我会用改变监听器。

哦，你知道这个接口太难了，你可以用 Rx，通过使用 debounce 和简单的 Rx Observable 来会变得非常简单。我问道，难道为了节省 10 行代码我就要使用 Rx 吗？他们回答我不是。你可以使用 map，filter 或者其他的函数让你的代码变得整洁简单。我不相信这是它的唯一好处，因为我可以通过一个类来统一管理这些事情。另一方面，我知道像 Netflix 和其他大公司都是使用这种范式，他们使用后都觉得很好。因此我更加困惑了。那天在我说好以后结束了。我还是没有搞懂 Rx 但是我了解我自己。虽然我有时会休息，但是我从来不会放弃，从来都不会。我决定了，我已经在很多教程里面学到了很多东西，但它们对我来说只是一堆拼图，是时候把拼图合成合适的形状了。

关键的一点，我要感谢我读的所有这些教程和书籍的作者，他们让我很困惑，但同时也教会了我。所以每个人都应该好好感谢写这些教程和书籍的作者。

另外一个关于我文章的关键点，我给你百分百保证，在该教程系列结束以后，你将会了解到 Rx Java2 的 80% 左右，但是别指望我会直接从 Rx Java2 开始。我会从最基础的部分开始，慢慢的指导，但是最后没人会感到困惑。

好长的动机，但是这对我很重要，是时候进攻了 🙂。

我在本教程中使用 IntelliJ 来执行编码任务。

**介绍：**

=======
* 译者：[Zhiw](https://github.ocm/Zhiw)
* 校对者：

## Observer Pattern – Reactive Programming [Android RxJava2]\(What the hell is this) Part1 ##
## 观察者模式 - 响应式编程[Android RxJava2]（这到底是什么）：第一部分

WOW, we got one more day so its time to make this day awesome by learning something new 🙂.

哦，

Hello Guys, hope you are doing good. Today I am going to start a new series of Rx Java2 more specific in Android but first 2-3 posts are general related to reactive programming. Hope we will learn something new and clear our all confusions together.

大家好，希望你们做的很好。今天我打算开始一个关于 Rx Java2 的新系列，但是首先的 2-3 篇文章是关于响应式编程的。希望我们能够学到新的东西，然后一起消除所有的疑虑。

**Motivation:**

**动机：**

Truly saying I faced a lot of issues when I start learning Rx. I tried lot of tutorials, books but in the end I am not able to start working with Rx in my app. Lot of tutorials confused me, like some are saying as we know iterator pattern which is pull based in a same way Rx is push based and giving some example but that is useless for me at that time. I want to learn Rx, I want to know the benefits, I want to know how this will save me from lot of bugs, lines of boiler plate code but every time I will get push vs pull or some times I will get imperative vs reactive but never got the real Rx answers which I want. On some posts authors are saying, this is just like Observer pattern. With the passage of time confusion increased, learning curve is going very difficult. Later I got some more tutorials on FRP then lambda expressions, functional programming. I got lot of examples in which people are using lambda expressions with calling map, filter blah blah blah functions. But I am on a same page What is Rx and why I choose this paradigm. Later I met with some friends who are using Rx. I ask these guys, can you teach me. They teach me like hey as you know we have a EditText. If you want to check user added any new text. How you will know? I gave answer I will use change listener.

说实话，我一开始学习 Rx 的时候遇到了许多问题。我尝试了许多教程，书籍，但是最后我都无法在我的应用里面使用 Rx。许多教程让我感到很困惑，就像有些部分说，迭代器模式是基于拉取，同样的，Rx 是基于推送的，并且给了一些例子，但那对于我来收是无用的。我想学习 Rx,我想了解它的好处，我想知道它如何将我从大量的 bug 和冗长鸡肋的代码中拯救我。但是每次我都会得到关于推和拉的比较，有些时候则是命令式和响应式的比较，我从来都得不到我想要的真正的 Rx 的答案。在一些文章中作者提到，Rx 就像观察者模式。随着疑惑时间的增多，学习曲线变得很困难。后来我得到一些关于FRP(译者注：Functional Reactive Programming，函数式响应性编程)，lambda 表达式，函数式的编程，我看到一些例子，他们使用 lambda 表达式来调用 map，filter 等函数。
和他们一样，我也想知道到底 Rx 是什么以及我为什么要选择它。后来我遇到了使用 Rx 的朋友，我就问他们能否指导一下如何使用 Rx。 他们是这样教我的，你知道我们有一个 EditText，如果你想检查用户是否输入了新文本，你用什么方法得知？我回答说我会用改变监听。

Oh you know the API is really difficult you can use Rx and that will be very easy by using debounce and simple Rx observable but I asked the question only to save from 10 lines of code I will go with Rx. They replied me no. You can use map, filter or lot of other functions to make your code in good shape and easy. I am not convinced because I can make one class that will manage all these things for me if that is the only benefit. On the other side I know Netflix and many other big companies are using this paradigm and there stats are good after using Rx. So I am more confused. The day come when I say ok, done. I am not going with Rx but I know myself. I never quit sometimes I take rest but I never quit. So I decided I already learned a lot of things, in lot of tutorials but that is just like a puzzle blocks for me. So Its time to make that puzzle blocks into a proper shape.

你知道这个接口太难了，你可以用 Rx，通过使用 debounce 和简单的 Rx 观察者来实现非常简单。我问道，难道为了节省 10 行代码我就要使用 Rx 吗？他们回答我不是。你可以使用 map，filter 或者其他的函数让你的代码变得整洁简单。我不相信这是它的唯一好处，因为我可以通过一个类来统一管理这些事情。另一方面，我知道像 Netflix 和其他大公司都是使用这种范式，他们使用后都觉得很好。因此我更加困惑了。那天在我说好以后结束了。我还是没有搞懂 Rx 但是我了解我自己。虽然我有时会休息，但是我从来不会放弃，从来都不会。我决定了，我已经在很多教程里面学到了很多东西，但它们对我来说只是一块拼图，是时候把拼图合成合适的形状了。

Important point. All those tutorials or books which I read I really want to appreciate there authors because they confused me but also they teach me. So everybody really thanks for writing all tutorials and books.

关键的是，我要感谢我读的所有这些教程和书籍的作者，因为他们让我很困惑，但同时也教会了我。所以每个人都应该好好感谢写这些教程和书籍的作者。

One important point about my post. I am giving you 100% guarantee. In the end of this tutorial series, you will know 80% about Rx Java2 but do not expect I will start directly from Rx Java2. I will go very slow and from very basics but in the end no body will confused.

另外一个关于我文章的关键点，我给你百分百保证。在该教程系列结束以后，你将会了解到 Rx Java2 的 80% 左右，但是别指望我会直接从 Rx Java2 开始。我会从最基础的部分开始，慢慢的指导，但是最后没人会感到困惑。

Very long motivation but that is important for me. Its time to attack 🙂 .

好长的动机，但是这对我很重要，是时候进攻了 🙂。

I am using IntelliJ in this tutorial for coding tasks.

我在本教程中使用 IntelliJ 来执行编码任务。

**Introduction:**

**介绍：**

One suggestion if you are confused just like me then try to forgot all terms which are mentioned below.

>>>>>>> Stashed changes
提个建议，如果你和我一样困惑，那就尝试忘掉下面提到的所有术语。

Rx

Observable

Observer

Map

Filter

FlatMap

Lymbda

Higher order functions

Iterator or Pull

Imperative

Reactive

Dataflow

Streams

FRP

<<<<<<< Updated upstream
等等。。。

因此我们将编写一个真实的企业应用系统的一个组件。这是响应式范式的第一步。基本上，这不会给你任何关于 Rx 的信息，但是这将为我们后面的教程打下基础。

**需求：**

我们的客户有一个网站，他要求，当他发布一篇新教程时，所有订阅的成员都会收到邮件。

**解决方案：**

我不打算去实现每一件事，但是我会通过一个方式去实现，所以我们就能轻易的抓住我们想要的概念。

是时候分解我们的需求了。

1. 我们有订阅的用户，那意味着我们要保存有关订阅用户的信息。

2. 这里应该有数据库，当用户发布新帖子的时候，插入行。简单来说，当帖子发布的时候，我们的数据应该发生改变。这个是我们关心的，因为当发生变化的时候，我需要通知我的订阅用户。

3. 邮件客户端，这不是我们的重点。

前面两点非常重要。我需要通过实现某些内容来实现这两点功能。

你可以使用很多方法，但是我要用对我来说最简单的一个，它将传达我想与你们分享的消息。

=======
etc… oh man.

So we are going to write a one component of a real enterprise application system. Which is our first step to reactive paradigm. Basically that will not give you any information about Rx but that will make some base which we will use in later tutorials.

因此我们将编写一个真正的企业应用系统的一个组件。这是响应式范式的第一步。基本上，这不会给你任何关于 Rx 的信息，但是这将为我们后面的教程打下基础。

**Requirement:**

**需求：**

Our client has a website. He wants, when he publish a new tutorial, all members who subscribed will get an email.

我们的客户有一个网站，他要求，当他发布一篇新教程时，所有订阅的成员都会收到邮件。

**Solution:**

**解决方案：**

I am not going to implement every thing real but I will implement in a way, so the concept which we want we will grasp easily.

我不打算去实现每一件事，但是我会通过一个方式去实现，所以我们就能轻易的抓住我们想要的概念。

Its time to breakdown our requirement.

是时候分解我们的需求了。

1. We have users who are subscribing. Its mean we need to save information about users who subscribed.

1. 我们有订阅的用户，那意味着我们要保存有关订阅用户的信息。

2. There should be some database where some row will be inserted when user published a new post. In simple words, on some place our data should be changed when tutorial published. Which we need to take care because when that change I need to inform to my subscribe users.

2. 这里应该有数据库，当用户发布新帖子的时候，插入行。简单来说，当帖子发布的时候，我们的数据应该发生改变。这个我们是我们关心的，因为当发生变化的时候，我需要通知我的订阅用户。

3. Email client, that is not our focus.

3. 邮件客户端，这不是我们的重点。

First two points are important. I need to implement something which will achieve these two points functionality.

前面两点非常重要。我需要通过实现某些内容来实现这两点功能。

There are lot of approaches which you can use but I am going with the simplest one according to me. Which will convey my message which I want to share with you.

你可以使用很多方法，但是我要用对我来说最简单的一个，它将传达我想与你们分享的消息。

So we have a one class User which contain only Name and Email of a member. Some people may think, we should have a isSubscribed filed. In my opinion that will make our code complex because then we need to use a loop to determine which are the subscribed users like shown below.

>>>>>>> Stashed changes
因此我们有一个只包含成员姓名和邮件的 User 类。有些人可能会想，我们应该有一个 isSubscribed 的变量。在我看来，这将会使我们的代码更复杂，因为之后我们需要使用一个循环来决定哪些是订阅用户，就像如下代码所示。

```
public static class User {

    private String name;
    private String email;
    private boolean isSubscribed;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public boolean isSubscribed() {
        return isSubscribed;
    }

    public void setSubscribed(boolean subscribed) {
        isSubscribed = subscribed;
    }
}
```

<<<<<<< Updated upstream
所以如果我使用这个类，然后很有可能，我在 main 方法中实现发送电子邮件的代码，将会如下所示。
=======
So If I am using this class then most probably I have some thing in my main method code where I want to send email code like shown below.

所以如果我使用这个类，然后很有可能，我在主要方法发送电子邮件的代码，如下所示。
>>>>>>> Stashed changes


```
public static void sendEmail(List<User> userList){

    for (User user : userList) {
        if(user.isSubscribed){
<<<<<<< Updated upstream
            // 发送邮件给用户
=======
            // send email to user
>>>>>>> Stashed changes
        }
    }
}
```

<<<<<<< Updated upstream
=======
But I am going in a different way. So my user class is given below

>>>>>>> Stashed changes
但我要用一种不同的方法，我的 User 类如下所示：

```
public static class User {

    private String name;
    private String email;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

<<<<<<< Updated upstream
我没有任何的 isSubscribed 变量，这意味当我调用 sendEmail 方法的时候，就不再使用 if，如下所示：
=======
So I did not have any isSubscribed filed. Its mean when I will call sendEmail function there is no if like shown below.

因此我没有任何的 isSubscribed 变量，这意味当我调用 sendEmail 方法的时候，就不用 if，如下所示：
>>>>>>> Stashed changes

```
public static void sendEmail(List<User> userList){
    for (User user : userList) {
<<<<<<< Updated upstream
            // 发送邮件给用户
=======
            // send email to user
>>>>>>> Stashed changes
    }
}
```

<<<<<<< Updated upstream
=======
Good. OK now its time to check how I can manage my subscribed users. Basically in this example I am going to take things in Memory so I am going to initialize one list of users. In which, I only save those users, who click subscribed button. If that is in real app then I have one table in database. Its time to show you some more code.

>>>>>>> Stashed changes
那现在是时候来检查一下我是如何管理我的订阅用户。最基本的，在本例中，我要从内存中取数据，所以先初始化一个用户列表。在这里，我只保存点了订阅按钮的用户。如果这是在真实的应用里，在数据库里面将有一张表。是时候给你们展示更多代码了。

```
private static List<User> subscribedUsers = new ArrayList<>();
```

<<<<<<< Updated upstream
=======
Imagine we have four users A, B, C and D. All will subscribe except B. So I am going to show you code how I will do that in our main method.

>>>>>>> Stashed changes
设想我们有 A, B, C, D 四个用户，除了 B 以外都订阅了。让我给你们展示一下代码，看看我在 main 方法里面都做了什么。

```
public static void main(String[] args){

    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");

<<<<<<< Updated upstream
    // 现在用户 A,C,D 点击了订阅按钮
=======
    // Now A,C and D click subscribe button
>>>>>>> Stashed changes

    subscribedUsers.add(A);
    subscribedUsers.add(C);
    subscribedUsers.add(D);
}
```

<<<<<<< Updated upstream
现在第一点已经完成了。我们需要保存那些需要订阅邮件的用户信息。

是时候去看一下第二点了。当用户发布新教程时，我想通知。这里我有一个 Tutorial 类如下所示。
=======
Now first point is done. In which we need to save information about those users who wants email.

现在第一点已经完成了。我们需要保存那些需要订阅邮件的用户信息。

Its time to take care of second point. When user publish new tutorial I want to inform. Here I have one class, Tutorial like shown below.

是时候去看一下第二点了。当用户发布新教程时，我想通知。这里我有一个类，教程如下所示。
>>>>>>> Stashed changes

```
public static class Tutorial{

    private String authorName;
    private String post;

    public String getAuthorName() {
        return authorName;
    }

    public void setAuthorName(String authorName) {
        this.authorName = authorName;
    }

    public String getPost() {
        return post;
    }

    public void setPost(String post) {
        this.post = post;
    }
}
```

<<<<<<< Updated upstream
=======
Here again we need a some place where we will save our tutorials. So in real app I should have a table but in this example I am going to initialize one List of Tutorials. Which will save all my old and new tutorials just like shown below.

>>>>>>> Stashed changes
这里我们需要一个地方来保存我们的教程。在真实的应用里面我应该有一个表，但是在本例中，我将初始化一个教程的列表，用来保存所有的新老教程，就像下面所示。

```
private static List<Tutorial> publishedTutorials = new ArrayList<>();
```

<<<<<<< Updated upstream
=======
Here I am going to increase complexity of our code :P. For example I have already 3 tutorials Android 1, Android 2 and Android 3.  All users subscribed, after 3 tutorials already published.  Its mean when I will add Android 4 tutorial then all users will get email. First I am going to show you only first part how I am going to add first 3 tutorials and later user will subscribe for email.

>>>>>>> Stashed changes
这里我将增加我们代码的复杂性 :P。例如我已经有 3 篇教程，Android 1, Android 2 和 Android 3。3 篇文章都已经发布了，然后所有用户都订阅了。这意味着当我添加 Android 4 教程的时候，所有用户都会收到邮件。首先我将展示第一部分，我如何添加开始的 3 篇教程，然后用户订阅邮件。

```
public static void main(String[] args){

    Tutorial android1 = new Tutorial("Hafiz", "........");
    Tutorial android2 = new Tutorial("Hafiz", "........");
    Tutorial android3 = new Tutorial("Hafiz", "........");

    publishedTutorials.add(android1);
    publishedTutorials.add(android2);
    publishedTutorials.add(android3);

<<<<<<< Updated upstream
    // 我已经有三篇教程了，然后用户订阅了邮件
=======
    // I have already three tutorials and later user subscribed for email
>>>>>>> Stashed changes

    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");

<<<<<<< Updated upstream
    // 现在用户 A,C,D 点击了订阅按钮
=======
    // Now A,C and D click subscribe button
>>>>>>> Stashed changes

    subscribedUsers.add(A);
    subscribedUsers.add(C);
    subscribedUsers.add(D);
}
```

<<<<<<< Updated upstream
=======
Now the most important point comes. Now I published fourth tutorial as shown below.

>>>>>>> Stashed changes
现在最重要的一点来了，我发布了第四篇教程，如下所示：

```
public static void main(String[] args){
<<<<<<< Updated upstream
    // 忽略下面的代码直到粗线开始（指 android4 开始的地方）
=======
    //Ignore the below code up to bold lines start
>>>>>>> Stashed changes
    Tutorial android1 = new Tutorial("Hafiz 1", "........");
    Tutorial android2 = new Tutorial("Hafiz 2", "........");
    Tutorial android3 = new Tutorial("Hafiz 3", "........");
    publishedTutorials.add(android1);
    publishedTutorials.add(android2);
    publishedTutorials.add(android3);
<<<<<<< Updated upstream
    // 我已经有三篇教程了，然后用户订阅了邮件
=======
    // I have already three tutorials and later user subscribed for email
>>>>>>> Stashed changes
    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");
<<<<<<< Updated upstream
    // 现在用户 A,C,D 点击了订阅按钮
=======
    // Now A,C and D click subscribe button
>>>>>>> Stashed changes
    subscribedUsers.add(A);
    subscribedUsers.add(C);
    subscribedUsers.add(D);

<<<<<<< Updated upstream
   Tutorial android4 = new Tutorial("Hafiz 4", "........");   
   publishedTutorials.add(android4);
=======
   Tutorial android4 = new Tutorial("Hafiz 4", "........");   publishedTutorials.add(android4);
>>>>>>> Stashed changes

}
```

<<<<<<< Updated upstream
我如何确定何时第四篇或者任何新教程发布，以便于我能发送邮件。

嗯，非常关键的要求。我打算实现轮询，轮询意味着我要实现一个定时器，它会在一段时间间隔后检查我的数据是否发生改变。这里我将设置一个 int 对象作为数据改变的通知者，如下所示：
=======
How I can determine fourth or any new tutorial published so I can send emails.

我如何确定当第四篇或者任何新教程发布的时候，我能发送邮件。

Hmmm very critical requirement. I am going to implement polling. Polling means I have timer which will check any thing change in my data after some time interval. Here I am going to take an int object which will work for me as a data changed informer as shown below.

嗯，非常关键的要求。我打算实现轮询，轮询意味着我要是只一个定时器，它会在一段时间间隔后检查我的数据是否发生改变。这里我将设置一个 int 对象作为数据改变的通知者，如下所示：
>>>>>>> Stashed changes

```
private static int lastCountOfPublishedTutorials = 0;

<<<<<<< Updated upstream
=======
```

```
>>>>>>> Stashed changes
Tutorial android1 = new Tutorial("Hafiz 1", "........");
Tutorial android2 = new Tutorial("Hafiz 2", "........");
Tutorial android3 = new Tutorial("Hafiz 3", "........");

publishedTutorials.add(android1);
publishedTutorials.add(android2);
publishedTutorials.add(android3);
lastCountOfPublishedTutorials = publishedTutorials.size();
polling();
```

<<<<<<< Updated upstream
=======
Now I got a focus point. Which I need to take care. If this count change its mean something change. In our case that always new tutorial publish so I need to send email. Its time to see how I implement Polling.

>>>>>>> Stashed changes
现在我有一个需要关注的点，如果这个数量变了，意味着有些东西发生了改变。在本例中，就是指新的教程发布我需要发送邮件。是时候让你们来看看我是如何实现轮询的。

```
private static void polling(){

    Polling polling = new Polling();
    Timer timer = new Timer();
    timer.schedule(polling, 0,1000);

}
```

<<<<<<< Updated upstream
=======
This method will call when server start or in our case when main method called. This method always active and after one second will check my data as changed or not shown below.

>>>>>>> Stashed changes
当服务启动或者在本例中 main 方法被调用的时候，该方法会被调用。该方法将一直处于活跃状态，每隔一秒检查我的数据是否发生变化，如下所示。

```
public static class Polling extends TimerTask{

    @Override
    public void run() {

        if(lastCountOfPublishedTutorials < publishedTutorials.size()){
            lastCountOfPublishedTutorials = publishedTutorials.size();
            sendEmail(subscribedUsers);
        }
        System.out.println("Polling");
    }
}
```

<<<<<<< Updated upstream
=======
Very simple. I am only checking if count changed then update count and send email to all subscribed users. Output on IDE shown below

>>>>>>> Stashed changes
非常简单，我只检查这个数量是否发生变化，然后更新数量并且发送邮件给所有的订阅用户。IDE 的输出如下所示。

---

Polling

Email send: A

Email send: C

Email send: D

Polling

Polling

Polling

<<<<<<< Updated upstream
---

用户交给的所有事情都已经完成了，但是是时候来回顾一下我们的方法了。我认为轮询非常糟糕。我们还能使用其他方法吗？

是的，当然可以。是时候来使用第二种方法来实现这个功能了。

现在我要改变一下我们类中的代码。伙计们，我会再次从最基本的部分开始，因此目前没什么接口，没有任何抽象的内容，所有事情都是具体的。最后我要做一点点的重构，以便我们可以很清晰的看到如何在专业软件开发中工作。
=======

Done. Everything which is given by client is done but its time to review our approach. I think polling is really bad. Any thing else which we can use?

用户交给的所有事情都已经完成了，但是是时候来回顾一下我们的方法了。我认为轮询非常糟糕。我们还能使用其他方法吗？

Yes we can. Its time to use second approach to achieve this functionality.

是的，当然可以。是时候来使用第二种方法来实现这个功能了。

Now I am going to change some code in our classes. Guys I am again going from very basic so currently no interfaces, nothing abstract every thing will be concrete. In the end I will do little bit refactoring so we can see clear picture like how things are working in Profession Software development.

现在我要改变一下我们类中的代码。伙计们，我会再次从最基本的部分开始，所有目前没什么接口，没有任何抽象的内容，所有事情都是具体的。最后我要做一点点的重构，以便我们可以很清晰的看到如何在专业软件开发中工作。

Its time to see what new changes occurred in Tutorial class as shown below.
>>>>>>> Stashed changes

让我们来看一下 Tutorial 类里面发生的新改变，如下所示。

```
public static class Tutorial{

    private String authorName;
    private String post;
    public Tutorial() {
    }

    public Tutorial(String authorName, String post) {
        this.authorName = authorName;
        this.post = post;
    }

    private static List<Tutorial> publishedTutorials = new ArrayList<>();
    private static List<User> subscribedUsers = new ArrayList<>();

    public static void addSubscribedUser(User user){
        subscribedUsers.add(user);
    }

    public static void publish(Tutorial tutorial){
        publishedTutorials.add(tutorial);
        sendEmail(subscribedUsers);
    }
}
```

<<<<<<< Updated upstream
=======
In new code, Tutorial class will take care of publish tutorials. Tutorial class will take care of subscribed users. Like you can see **addSubscribedUser **method. Now its time to show you main method code. You can easily compare what are the changes between these two approaches.

>>>>>>> Stashed changes
在新的代码中，Tutorial 类将关注于发布的教程和订阅的用户。就像你可以使用 **addSubscribedUser** 方法。现在给你们展示一下 main 方法的代码。你们可以很轻易的比较两种方法的变化。

```
public static void main(String[] args){

    Tutorial android1 = new Tutorial("Hafiz 1", "........");
    Tutorial android2 = new Tutorial("Hafiz 2", "........");
    Tutorial android3 = new Tutorial("Hafiz 3", "........");

    Tutorial.publish(android1);
    Tutorial.publish(android2);
    Tutorial.publish(android3);

<<<<<<< Updated upstream
    // 我已经有三篇教程了，然后用户订阅邮件
=======
    // I have already three tutorials and later user subscribed for email
>>>>>>> Stashed changes

    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");

<<<<<<< Updated upstream
    // 现在用户 A,C,D 点击了订阅按钮
=======
    // Now A,C and D click subscribe button
>>>>>>> Stashed changes

    Tutorial.addSubscribedUser(A);
    Tutorial.addSubscribedUser(C);
    Tutorial.addSubscribedUser(D);

    Tutorial android4 = new Tutorial("Hafiz 4", "........");
    Tutorial.publish(android4);

}
```

<<<<<<< Updated upstream
现在 Tutorial 类负责发布教程，也负责管理订阅用户。因此我们移除第一个轮询，这真是一个巨大的成就。然后开发者就再也不用负责写谁来通知数据变化的逻辑代码了，因此我们移除了 **lastCountOfPublishedTutorials** 对象。

那真是太棒了，输出如下所示。

---
=======
Now tutorial class is responsible for publishing tutorial. Also that class managing subscription of users. So we remove first polling. Which is a really big achievement. Then developer no more responsible to write logic which will inform any thing change in data so we remove Object **lastCountOfPublishedTutorials**.

现在 Tutorial 类负责发布教程，也负责管理订阅用户。因此我们移除第一个轮询，这真是一个巨大的成就。然后开发者就再也不用负责写谁来通知数据变化的逻辑代码了，因此我们移除了 **lastCountOfPublishedTutorials** 对象。

That is really awesome. Output is shown below.

那真是太棒了，输出如下所示。

>>>>>>> Stashed changes

Email send: A

Email send: C

Email send: D

<<<<<<< Updated upstream
---
我知道上面的输出不太清楚，因为程序退出了，所以我将实现一个逻辑，它将让我们的程序运行在内存中，从不退出，然后在 1 秒钟后发布新的教程。这样我们就能看到邮件是怎么发出去的。

---
=======

I know above output not clear because program exit so I am going to implement one logic which only make our program always run in memory, never exit and also published new tutorial after 1 second. So we can see how emails are going.

我知道上面的输出不太清楚，因为程序退出了，所以我将实现一个逻辑，它将让我们的程序运行在内存中，从不退出，然后在 1 秒钟后发布新的教程。这样我们就能看到邮件是怎么发出去的。
>>>>>>> Stashed changes

Email send: A

Email send: C

Email send: D

Email send: A

Email send: C

Email send: D

Email send: A

Email send: C

Email send: D

<<<<<<< Updated upstream
--- 

从不退出

现在该去找一些更好更专业的方法了，我们有任何方法吗？

是的，我们有，但在那之前，我要解释一些英文术语。

有人能解释 Observable 吗？

在英语中，任何可以被观察的事物，比如说我的花园里面有一颗很漂亮的树，我经常观察它，这就意味着它是 Observable 的。当我在观察树的时候，现在有一场雷暴，我观察到树叶因为疾风而落下，这发生了什么呢？树是 Observable 的，我是 Observer。当我是 Observer时，我能感受到树的变化。现在我不是一个人了，有我老婆陪着我，但她没有在观察树。因此当第一片树叶掉落的时候，我能感受到变化，但我老婆不能。后来她也开始观察树。这时当第二片叶子掉落的时候，我们两个都能感受到变化。这意味着树作为 Observable，能够将变化告知它的 Observer。

如果同样的事情，我使用轮询的方法，那将发生什么。我数一下树叶的数量然后记住。一秒钟以后我再数一遍，然后和上一个结果作对比，所以我感受到了变化，但是我得每一秒钟都这么做。哈哈，在现实中，我可做不了。

在第一种情况下，Observable 负责将变化通知他们的 Observer，我们可以称为 Push（Rx 就是 Push）。

在第二种情况下，我的轮询需要来检查任何发生的变化，然后通知我们的用户，你可以称为 Pull。

所以现在是实现 Observable 和 Observer 的时候了。

在我们的应用中，Observable 是什么？没错，正是教程。那 Observer 又是谁呢？没错，用户。
=======
…… Never exit
从不退出


Now its time to find some more good and professional approach. We have any approach?

现在该去找一些更好更专业的方法了，我们有任何方法吗？

Yes we have but before that I am going to explain some english terms.

是的，我们有，但在那之前，我要解释一些英文术语。

Any body can explain Observable?

有人能解释 Observable 吗？

In my english. Any thing which can be observe. Like I have a really beautiful tree in my garden. I mostly observe that so its mean tree is observable. Now there is a thunderstorm when I am observing tree. I observed some of there leafs are fallen down due to fast wind. So what is happening. Tree is observable and I am observer. The time when I am observer, I can feel the change in tree. Now I am not alone my wife also with me but she is not observing tree. So when first leave fallen down, I can feel something change but my wife not. Later she also start observing tree. This time when second leave fallen down we both can feel the change. Its mean tree as an Observable, telling to its observers something changed.

在英语中，任何事物都可以被观察。比如说我的花园里面有一颗很漂亮的树，我经常观察它，这就意味着它是可被观察的。当我在观察树的时候，现在有一场雷暴，我观察到树叶因为疾风而落下，这发生了什么呢？树是可被观察的，我是观察者。当我是观察者时，我能感受到树的变化。现在我不是一个人了，有我老婆陪着我，但她没有在观察树。因此当第一片树叶掉落的时候，我能感受到变化，但我老婆不能。后来她也开始观察树。这时当第二片叶子掉落的时候，我们两个都能感受到变化。这意味着树作为被观察者，能够告知他的观察者发生了变化。

If I do the same thing by using polling then what will happen. I count the tree leafs and remember the result. After one second I count again and I compare this result with last result so I feel there is a change but I am doing after every one second. hahahaha In reality I am not able to do.

如果同样的事情，我使用轮询的方法，那将发生什么。我数一下树叶的数量然后记住。一秒钟以后我再数一遍，然后和上一个结果作对比，所以我感受到了变化，但是我得每一秒钟都这么做。哈哈，在现实中，我可做不了。

In first scenario Observable is responsible to inform there observers about change that you can say Push (Rx is Push).

在第一种情况下，Observable 负责将变化通知他们的观察者，我们可以称为 Push（Rx 就是 Push）。

In second scenario my Polling is checking any change then need to inform our users that you can say Pull.

在第二种情况下，我的轮询需要来检查任何发生的变化，然后同志我们的用户，你可以称为 Pull。

So its time to implement Observable, Observer strategy.

所以现在是实现 Observable 和 Observer 的时候了。

In our app what is Observable? Yes, you are right Tutorials. And who is observing? Yes, Users.

在我们的应用中，Observable 是什么？是的，正是教程。那 Observer 又是谁呢？没错，用户。

Now I am going to introduce the interfaces which we used in professional software development for Observer pattern.
>>>>>>> Stashed changes

现在我要介绍一下我们在专业软件开发中用于观察者模式的接口。

```
public interface Observer{
<<<<<<< Updated upstream
    // 新教程发布
=======
    // New tutorial published
>>>>>>> Stashed changes
    void notifyMe();
}
```

```
public interface Observable{

 void register(Observer observer);

 void unregister(Observer observer);

 // New tutorial published to inform all subscribed users
 void notifyAllAboutChange();
}
```

<<<<<<< Updated upstream
现在我们可以看看抽象或者通用接口。Observer 和 Observable。

在我们的应用中，用户就是 Observer，所以我要在该类中实现 Observer 接口，而教程就是 Observable，所以我要在该类中实现 Observable 接口，如下所示。
=======
Now we can see abstract or generic interfaces. Observer and Observable.

现在我们可以看看抽象或者通用接口。Observer 和 Observable。

In our app User is observer so I will implement Observer interface on that class and Tutorial is Observable so I am implementing Observable to Tutorial class as shown below.

在我们的应用中，用户就是 Observer，所以我要在该类中实现 Observer 接口，而教程就是 Observable 所以我要在该类中实现 Observable 接口，如下所示。
>>>>>>> Stashed changes

```
public static class User implements Observer{

    private String name;
    private String email;
    public User() {    }
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }
    public String getName() {   return name;    }
    public void setName(String name) {        this.name = name;    }
    public String getEmail() {        return email;    }
    public void setEmail(String email) {        this.email = email;    }

    @Override
    public void notifyMe() {
        sendEmail(this);
    }
}
```

<<<<<<< Updated upstream
=======
Now here User will be informed by Tutorial, hey I published new post by calling notifyMe() method.

>>>>>>> Stashed changes
现在用户将会被教程通知，我调用 notifyMe() 方法发布了一篇新文章。

```
public static class Tutorial implements Observable{

    private String authorName;
    private String post;
    private Tutorial() {};
    public static Tutorial REGISTER_FOR_SUBSCRIPTION = new Tutorial();

    public Tutorial(String authorName, String post) {
        this.authorName = authorName;
        this.post = post;
    }

 private static List<Observer> observers = new ArrayList<>();
    @Override
    public void register(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void unregister(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyAllAboutChange() {
        for (Observer observer : observers) {
            observer.notifyMe();
        }
    }

    public void publish(){
        notifyAllAboutChange();
    }
}
```

<<<<<<< Updated upstream
所以该类中发生了什么变化呢？首先我将用户变为 Observer，因此它可以注册任何他想知道的新的教程发布。在本例中，就是 User，因为 User 实现了该接口。

然后注册和取消注册两个简单的方法管理着订阅或者未订阅。

对于注册和取消注册，我们使用类的对象 **REGISTER_FOR_SUBSCRIPTION**。然后是 **notifyAllAboutChange** 方法，它将把变化通知所给有的 Observer。最后一个方法是 **publish**，它是当前实例的方法。任何时候当我调用 publish 方法时，所有注册的 Observer 都会通过调用 **notifyMe()** 被通知。
=======
So what changes occur in this class. First I changed User to Observer. So any observer want to know any new tutorial published he can register. In our case that is User because User implemented this interface.

所以该类中发生了什么变化呢？首先我将用户变为 Observer，因此它可以注册任何他想知道的新的教程发布的。在本例中，就是 User 因为 User 实现了该接口。

Then register and unregister simple methods which manage the subscription or un subscription.

然后注册和取消注册简单的方法管理着订阅或者没订阅。

For register and unregister we are using class level object **REGISTER_FOR_SUBSCRIPTION.** Then **notifyAllAboutChange** method. Which will inform to all observers hey some thing changed. The last method is **publish,** which currently instance level method. Any time I call publish method, all register observers will informed by calling there **notifyMe()** method.

对于注册和取消注册，我么使用类级别的对象 **REGISTER_FOR_SUBSCRIPTION**。然后是 **notifyAllAboutChange** 方法，它将把变化通知所给有的观察者。最后一个方法是 **publish**，它是当前实例的方法。任何时候当我调用 publish 方法时，所有注册的观察者都会通过调用 **notifyMe()** 被通知。
>>>>>>> Stashed changes

```
public static void main(String[] args){

    Tutorial android1 = new Tutorial("Hafiz 1", "........");
    android1.publish();
    Tutorial android2 = new Tutorial("Hafiz 2", "........");
    android2.publish();
    Tutorial android3 = new Tutorial("Hafiz 3", "........");
    android3.publish();

<<<<<<< Updated upstream

=======
    // I have already three tutorials and later user subscribed for email
>>>>>>> Stashed changes
    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");

<<<<<<< Updated upstream

=======
    // Now A,C and D click subscribe button
>>>>>>> Stashed changes

    Tutorial.REGISTER_FOR_SUBSCRIPTION.register(A);
    Tutorial.REGISTER_FOR_SUBSCRIPTION.register(C);
    Tutorial.REGISTER_FOR_SUBSCRIPTION.register(D);

    Tutorial android4 = new Tutorial("Hafiz 4", "........");
    android4.publish();

}
```

<<<<<<< Updated upstream
这太简单了，没必要解释。现在我感觉每个人都应该知道 Observable 和 Observer 是什么了。这些才是真正重要的，它们是唯一在 Rx 中使用时间占 99.9% 的术语。所以如果你对此有一个清晰的印象，另外看到在我们的应用中使用这个模式获得了巨大的好处，那么你就能轻易的掌握 Rx 范式。现在我要利用 Rx 库再改变一下最后的代码。开始之前，我想讨论几个点。

1. 这不是一个很棒的例子，但是我想让你应该知道 Observable，Observer，Pull，Push 分别是什么。

2. 我想通过 RxJava 实现的这个功能，从 Rx 好处的角度来说，是一件非常小的事情。

3. 我不打算向你们解释任何我将使用的那些方法。只要去回顾一下代码并且不要紧张，在后面的教程中你就会明白了。

4. 重申一下，这不是 RxJava 的真正力量。基本上我是用这个例子来为我和我朋友打基础。

将 RxJava 集成到你的工程里，你可以从 [这里](https://mvnrepository.com/artifact/io.reactivex/rxjava/1.0.2) 下载。

是时候来享受一下使用 Rx 库以后节省了多少行代码。你也可以设想一下，如果我要在工程的 8 个地方实现这个观察者模式，我需要写多少样板代码，但是使用 Rx，什么都不用。

首先我将 Observable 和 Observer 接口从我的类中移除。
=======
That is really simple no need to explain. Ok guys so now I have a feeling every body will know what is Observable and what is observer. These are really important instead these are the only terms which used 99.9% time in Rx. So if you have clear image what is that you can easily grab the Rx paradigm. Also if you saw we get a really big benefit by using this pattern in our app. Now I am going to change this last code again by using Rx lib. Before start I want to discuss some points.



1. This is not awesome example but I want you should know what Observable, Observer, Pull, Push

2. The functionality which I am going to implement by RxJava is a very very small thing in perspective of Rx benefits.

3. I am not going to explain you any thing about methods which I am going to use. Only try to review code and don’t take tension. In later tutorials you will know everything.

4. Again this is not the only real power of Rx Java. Basically I used this example to make basic ground for me and my friends.

Integrate java rx lib in your project. You can download from [here](https://mvnrepository.com/artifact/io.reactivex/rxjava/1.0.2).

Its time to enjoy how many line of code will remove by using this rx library. Also you can imagine if I want to implement this Observer Patteren on 8 places in my project how much code I need to write which is boilerplate but by using Rx that is nothing.

First I removed Observable and Observer interfaces from my classes.
>>>>>>> Stashed changes

![Markdown](http://p1.bpimg.com/1949/f26cfb93088350ac.png)

![Markdown](http://p1.bpimg.com/1949/e1de180148389eb9.png)

![Markdown](http://p1.bpimg.com/1949/4e3d085c47acfff5.png)

<<<<<<< Updated upstream
现在我要实现 RxJava 库的方法。

使用 Rx 以后的 User 类（Observer）如下所示。

```
public static class User implements Action1 {
=======
Now I am going to implement Rx Java lib methods.

User (Observer) class after Rx applying shown below.

```
public static class User **implements Action**1{
>>>>>>> Stashed changes

    private String name;
    private String email;
    public User() {}
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }
    public String getName() {return name;}
    public void setName(String name) {this.name = name;}
    public String getEmail() {return email;}
    public void setEmail(String email) {this.email = email;}

    @Override
    public void call(Object o) {
        sendEmail(this);
    }
}
```

<<<<<<< Updated upstream
我们可以说 Action1 是 Rx 库用来给 Observer 的一个辅助接口。

使用 Rx 以后的 Tutorial 类（Observable）如下所示。
=======
We can say Action1 is the helper interface from Rx lib which used for Observers.

Tutorial (Observable) class after Rx applying shown below.
>>>>>>> Stashed changes

```
public static class Tutorial {

    private String authorName;
    private String post;
    private Tutorial() {}

    public static rx.Observable REGISTER_FOR_SUBSCRIPTION =
                  rx.Observable.just(new Tutorial());

    public Tutorial(String authorName, String post) {
        this.authorName = authorName;
        this.post = post;
    }

    public void publish(){
        REGISTER_FOR_SUBSCRIPTION.publish();
    }

}
```

<<<<<<< Updated upstream
如果我们将这两个类和之前的对比，我们移除了许多代码。通过使用 Rx，我将我的 **REGISTER_FOR_SUBSCRIPTION** 转换成 Rx Observable。现在我们已经知道什么是 Observable。所以任何 Observer 都可以订阅我的 Observable，然后当 Observable 的 publish 方法被调用时，所有的 Observer 都会被通知。

main 方法如下所示。
=======
Wow if we compare this class with old one, we removed a lot of code. What I did here. By using Rx I converted my **REGISTER_FOR_SUBSCRIPTION** to Rx Observable. Now we already know what is Observable. So any observer can subscribed to my Observable and when Observable publish method will called automatically all observers will informed.

Its time to show you main method code.
>>>>>>> Stashed changes

```
public static void main(String[] args){

    Tutorial android1 = new Tutorial("Hafiz 1", "........");
    android1.publish();
    Tutorial android2 = new Tutorial("Hafiz 2", "........");
    android2.publish();
    Tutorial android3 = new Tutorial("Hafiz 3", "........");
    android3.publish();

    // I have already three tutorials and later user subscribed for email
    User A = new User("A","a@a.com");
    User B = new User("B","b@a.com");
    User C = new User("C","c@a.com");
    User D = new User("D","d@a.com");

    // Now A,C and D click subscribe button

    Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(A);
    Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(C);
    Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(D);

    Tutorial android4 = new Tutorial("Hafiz 4", "........");
    android4.publish();

}
```

<<<<<<< Updated upstream
main 方法代码块没有什么大的变化，输出如下。
=======
There is no big difference in main method code block. Output of above code.
>>>>>>> Stashed changes

---

Email send: A

Email send: C

Email send: D

---

<<<<<<< Updated upstream
欢呼一下。一切工作都是相同，除了实现角度上我们更简单和容易。

**结论：**
作为结论，我们只是尝试去学了观察者模式，它只是 Rx 的基础。第二点，如果我要求你在同一段代码里，有 8 个模块需要实现通知功能，你怎么办。你需要实现 8 次 Observer 和 Observable 接口和一些样板代码。但是通过使用 Rx，你只需要调用 rx.Observable.just() 方法，然后那个对象就可以像 Observable 一样工作。然后任何的 Observer 都可以订阅该 Observable。如果你们又迷惑了，那么你可以忘掉 Rx 这部分。只要记住什么是观察者模式。在下一篇文章中，我将使用我们今天学习的这个概念，正确的介绍 Rx。

所有代码都写在下面，你可以复制粘贴到你的 IDE 然后尽情玩耍。

好的，大家伙拜拜了。下一篇文章 [Pull vs Push & Imperative vs Reactive – Reactive Programming [Android RxJava2] ( What the hell is this ) Part2](http://www.uwanttolearn.com/android/pull-vs-push-imperative-vs-reactive-reactive-programming-android-rxjava2-hell-part2/)。

**轮询方法：**
=======
Hurray. Everything working same except we make thing simple and easy in implementation perspective.

**Conclusion:**
As a conclusion. We only try to learn Observer Pattern which is a base of Rx. Second if I ask you I have 8 modules which required notification functionality in a same code. So you need to implement eight times Observer and Observable interfaces and lot of boilerplate code. But by using Rx now you know only called rx.Observable.just() method and that object work like observable. Then any observer can subscribe to that Observable. If you guys are confused again you can forgot the Rx part. Only remember what is Observer Pattern. In next post I will introduce Rx in a proper way by using this concept which we learned today.

All codes are written below. You can copy and past on your IDE and play with these.

OK Guys Bye Bye. Next post [Pull vs Push & Imperative vs Reactive – Reactive Programming [Android RxJava2] ( What the hell is this ) Part2](http://www.uwanttolearn.com/android/pull-vs-push-imperative-vs-reactive-reactive-programming-android-rxjava2-hell-part2/).

.

**Polling Approach:**
>>>>>>> Stashed changes

```
import java.util.ArrayList;
        import java.util.List;
        import java.util.Timer;
        import java.util.TimerTask;

/**
 * Created by waleed on 04/02/2017.
 */
public class Main {

    private static List<User> subscribedUsers = new ArrayList<>();

    private static List<Tutorial> publishedTutorials = new ArrayList<>();
    private static int lastCountOfPublishedTutorials = 0;

    public static void main(String[] args){

        Tutorial android1 = new Tutorial("Hafiz 1", "........");
        Tutorial android2 = new Tutorial("Hafiz 2", "........");
        Tutorial android3 = new Tutorial("Hafiz 3", "........");

        publishedTutorials.add(android1);
        publishedTutorials.add(android2);
        publishedTutorials.add(android3);
        lastCountOfPublishedTutorials = publishedTutorials.size();

        polling();
        // I have already three tutorials and later user subscribed for email

        User A = new User("A","a@a.com");
        User B = new User("B","b@a.com");
        User C = new User("C","c@a.com");
        User D = new User("D","d@a.com");

        // Now A,C and D click subscribe button

        subscribedUsers.add(A);
        subscribedUsers.add(C);
        subscribedUsers.add(D);

        Tutorial android4 = new Tutorial("Hafiz 4", "........");
        publishedTutorials.add(android4);

    }

    public static void sendEmail(List<User> userList){

        for (User user : userList) {
            // send email to user

            System.out.println("Email send: "+user.getName());
        }
    }

    public static class User {

        private String name;
        private String email;

        public User() {
        }

        public User(String name, String email) {
            this.name = name;
            this.email = email;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getEmail() {
            return email;
        }

        public void setEmail(String email) {
            this.email = email;
        }
    }

    public static class Tutorial{

        private String authorName;
        private String post;

        public Tutorial() {
        }

        public Tutorial(String authorName, String post) {
            this.authorName = authorName;
            this.post = post;
        }

        public String getAuthorName() {
            return authorName;
        }

        public void setAuthorName(String authorName) {
            this.authorName = authorName;
        }

        public String getPost() {
            return post;
        }

        public void setPost(String post) {
            this.post = post;
        }
    }

    private static void polling(){

        Polling polling = new Polling();
        Timer timer = new Timer();
        timer.schedule(polling, 0,1000);

    }

    public static class Polling extends TimerTask{

        @Override
        public void run() {

            if(lastCountOfPublishedTutorials < publishedTutorials.size()){
                lastCountOfPublishedTutorials = publishedTutorials.size();
                sendEmail(subscribedUsers);
            }
            System.out.println("Polling");
        }
    }

}

```

<<<<<<< Updated upstream
**第一次重构方法：**
=======
**First Refactoring Approach:**
>>>>>>> Stashed changes

```
/**
 * Created by waleed on 04/02/2017.
 */
public class Main {

    public static void main(String[] args){

        polling();

        Tutorial android1 = new Tutorial("Hafiz 1", "........");
        Tutorial android2 = new Tutorial("Hafiz 2", "........");
        Tutorial android3 = new Tutorial("Hafiz 3", "........");

        Tutorial.publish(android1);
        Tutorial.publish(android2);
        Tutorial.publish(android3);

        // I have already three tutorials and later user subscribed for email

        User A = new User("A","a@a.com");
        User B = new User("B","b@a.com");
        User C = new User("C","c@a.com");
        User D = new User("D","d@a.com");

        // Now A,C and D click subscribe button

        Tutorial.addSubscribedUser(A);
        Tutorial.addSubscribedUser(C);
        Tutorial.addSubscribedUser(D);

        Tutorial android4 = new Tutorial("Hafiz 4", "........");
        Tutorial.publish(android4);

    }

        private static void polling(){

        Polling polling = new Polling();
        Timer timer = new Timer();
        timer.schedule(polling, 0,1000);

    }

    public static class Polling extends TimerTask{

        @Override
        public void run() {
            Tutorial android4 = new Tutorial("Hafiz 4", "........");
            Tutorial.publish(android4);
        }
    }

    public static void sendEmail(List<User> userList){

        for (User user : userList) {
                // send email to user

            System.out.println("Email send: "+user.getName());
        }
    }

    public static class User {

        private String name;
        private String email;

        public User() {
        }

        public User(String name, String email) {
            this.name = name;
            this.email = email;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getEmail() {
            return email;
        }

        public void setEmail(String email) {
            this.email = email;
        }
    }

    public static class Tutorial{

        private String authorName;
        private String post;
        public Tutorial() {
        }

        public Tutorial(String authorName, String post) {
            this.authorName = authorName;
            this.post = post;
        }

        private static List<Tutorial> publishedTutorials = new ArrayList<>();
        private static List<User> subscribedUsers = new ArrayList<>();

        public static void addSubscribedUser(User user){
            subscribedUsers.add(user);
        }

        public static void publish(Tutorial tutorial){
            publishedTutorials.add(tutorial);
            sendEmail(subscribedUsers);
        }
    }
}
```

<<<<<<< Updated upstream
**专业/观察者模式方法：**
=======
**Professional/Observer Pattern Approach:**
>>>>>>> Stashed changes

```
import java.util.*;
/**
 * Created by waleed on 04/02/2017.
 */
<<<<<<< Updated upstream

=======
```

```
>>>>>>> Stashed changes
public class Main {

    public static void main(String[] args){

        Tutorial android1 = new Tutorial("Hafiz 1", "........");
        android1.publish();
        Tutorial android2 = new Tutorial("Hafiz 2", "........");
        android2.publish();
        Tutorial android3 = new Tutorial("Hafiz 3", "........");
        android3.publish();

<<<<<<< Updated upstream
        // 我已经有三篇教程，稍后用户会订阅邮件
=======
        // I have already three tutorials and later user subscribed for email
>>>>>>> Stashed changes
        User A = new User("A","a@a.com");
        User B = new User("B","b@a.com");
        User C = new User("C","c@a.com");
        User D = new User("D","d@a.com");

<<<<<<< Updated upstream
        // 现在 A,C,D 点了订阅按钮
=======
        // Now A,C and D click subscribe button
>>>>>>> Stashed changes

        Tutorial.REGISTER_FOR_SUBSCRIPTION.register(A);
        Tutorial.REGISTER_FOR_SUBSCRIPTION.register(C);
        Tutorial.REGISTER_FOR_SUBSCRIPTION.register(D);

        Tutorial android4 = new Tutorial("Hafiz 4", "........");
        android4.publish();

    }

    public static void sendEmail(User user){
            System.out.println("Email send: "+user.getName());
    }

    public static class User implements Observer{

        private String name;
        private String email;

        public User() {
        }

        public User(String name, String email) {
            this.name = name;
            this.email = email;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getEmail() {
            return email;
        }

        public void setEmail(String email) {
            this.email = email;
        }

        @Override
        public void notifyMe() {
            sendEmail(this);
        }
    }

    public static class Tutorial implements Observable{

        private String authorName;
        private String post;
        private Tutorial() {}

        public static Tutorial REGISTER_FOR_SUBSCRIPTION = new Tutorial();

        public Tutorial(String authorName, String post) {
            this.authorName = authorName;
            this.post = post;
        }

        private static List<Observer> observers = new ArrayList<>();
        @Override
        public void register(Observer observer) {
            observers.add(observer);
        }

        @Override
        public void unregister(Observer observer) {
            observers.remove(observer);
        }

        @Override
        public void notifyAllAboutChange() {
            for (Observer observer : observers) {
                observer.notifyMe();
            }
        }

        public void publish(){
            notifyAllAboutChange();
        }

    }

    public interface Observable{

        void register(Observer observer);

        void unregister(Observer observer);

<<<<<<< Updated upstream
        // 新教程发布，通知所有订阅用户
=======
        // new tutorial published to tell all subscribed users
>>>>>>> Stashed changes
        void notifyAllAboutChange();

    }

    public interface Observer{

<<<<<<< Updated upstream
        // 新教程发布
=======
        // New tutorial published
>>>>>>> Stashed changes
        void notifyMe();
    }
}
```

<<<<<<< Updated upstream
**Rx 方法：（记住把 Rx 库整合到你的工程里）**
=======
**Rx Approach: (Note integrate Rx lib in your project)**
>>>>>>> Stashed changes

```
import rx.*;
import rx.Observable;
import rx.Observer;
import rx.functions.Action;
import rx.functions.Action1;
import rx.observers.Observers;

import java.util.*;
/**
 * Created by waleed on 04/02/2017.
 */
public class Main {

    public static void main(String[] args){

        Tutorial android1 = new Tutorial("Hafiz 1", "........");
        android1.publish();
        Tutorial android2 = new Tutorial("Hafiz 2", "........");
        android2.publish();
        Tutorial android3 = new Tutorial("Hafiz 3", "........");
        android3.publish();

        // I have already three tutorials and later user subscribed for email
        User A = new User("A","a@a.com");
        User B = new User("B","b@a.com");
        User C = new User("C","c@a.com");
        User D = new User("D","d@a.com");

        // Now A,C and D click subscribe button

        Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(A);
        Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(C);
        Tutorial.REGISTER_FOR_SUBSCRIPTION.subscribe(D);

        Tutorial android4 = new Tutorial("Hafiz 4", "........");
        android4.publish();

    }

    public static void sendEmail(User user){
        System.out.println("Email send: "+user.getName());
    }

    public static class User implements Action1{

        private String name;
        private String email;
        public User() {}
        public User(String name, String email) {
            this.name = name;
            this.email = email;
        }
        public String getName() {return name;}
        public void setName(String name) {this.name = name;}
        public String getEmail() {return email;}
        public void setEmail(String email) {this.email = email;}

        @Override
        public void call(Object o) {
            sendEmail(this);
        }
    }

    public static class Tutorial {

        private String authorName;
        private String post;
        private Tutorial() {}

        public static rx.Observable REGISTER_FOR_SUBSCRIPTION = rx.Observable.just(new Tutorial());

        public Tutorial(String authorName, String post) {
            this.authorName = authorName;
            this.post = post;
        }

        public void publish(){
            REGISTER_FOR_SUBSCRIPTION.publish();
        }

    }

}

```
