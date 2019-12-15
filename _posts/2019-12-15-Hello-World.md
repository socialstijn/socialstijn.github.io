---
layout: post
title: Automatically rename Macs using Addigy maintenance scripts
categories: [Addigy, macOS]
---

When onboarding new clients in Addigy I like to add a few maintenance scripts. One of these scripts automatically renames a Mac according to the logged in user, type of Mac (MacBook Pro, Mac mini etc), company name and last digits of serial number. This results in something like this 

> John-MBP-FruitCo

Addigy allows you to run scripts based on values in a [Custom Fact](https://support.addigy.com/support/solutions/articles/8000075303-best-practices-and-examples-for-custom-facts), or on a specified time. In this case I usually go for the latter.

