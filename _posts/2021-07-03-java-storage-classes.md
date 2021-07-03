---
layout: post
title:  "Java Storage Classes"
date:   2021-07-03 00:00:00 +0530
categories: []
tags: java
author: "Hardik Jogani"
---

One of the most important type of object is for a storage class. Storage classes are not meant to run at the command lines, the main() mathod is not usually used inside a java storage class.

A storage class is used to hold data, and represents th attributes of the object that the storage class is supposed to represent.

Here is a simplified version of storage class that we will use for a Book object.

``` java
public class Book {
   // instance variables
   private String title;
   private String author;
   private double price;

   // constructor
   public Book(String t, String a, double p) {
      title = t.trim();
      author = a.trim();
      price = p;
   }
}
```

In simple any POJO in java is a simple storage class