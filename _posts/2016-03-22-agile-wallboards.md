---
published: true
title: "Agile Wallboards - What, Why and How?"
layout: post
"section-type": post
comments: true
date: "2016-01-22 05:47:23 +0530"
---

Agile Team Wallboards make an agile team's workspace meaningful.  Wallboard is an information radiator mounted on wall (pretty self-explanatory, huh!).  Wallboard displays relevant information, aggregated from multiple sources, to help in making decisions regarding daily work.

Team Wallboard is typically electronic, powered by widgets and dashboards available in popular Agile tools like JIRA, Rally, etc.  There are teams which have a manually maintained wallboard as well.

##Why is a Wallboard needed?
Wallboard serves two sets of people in the organization:

1. **The team** - The team uses real data to make daily decisions to reach their iteration goal.

2. **Everyone else**- No one needs to go and ask about iteration's health from team members or scrum master.  They can just spend some minutes looking at the wallboard and they have the metrics.

##What information can be included in Team Wallboard?
Anything that helps!  You can include burn down charts, bug counts, days-until-iteration-end counters, etc.  

The idea is to evolve the design of wallboard's information over time. You need to discuss the design improvements in wallboard during retrospectives.

#How to setup a Team Wallboard?

## Option 1 : Wallboard using an Always-on Whining Machine

Anyone who thinks about wallboard setup will get this in their mind the first time.  This is the most basic setup.  All this contains is a LCD/LED monitor hooked up to an age-old desktop computer.

Let's do a quick cost analysis of this setup
### Fixed Costs
1. LCD Monitor - 5000 INR approx.
2. CPU+Other Hardware - 10000 INR approx.
Total - 15000 INR approx.

### Variable Costs
1. Electricity (as per computer hardware)

### Advantages
Straight-forward setup

### Disadvantages
1. Consumes too much electric power
2. Generates a lot of noise almost all the time (Always-on whining machine)
3. Needs a lot of real-estate to place the CPU

## Option 2: Wallboard using a laptop

In this option, we replace the desktop computer with an always-on laptop.  LCD/LED monitor is hooked up to the laptop using a VGA or HDMI setup.  

Some organizations replace the laptop with a Macbook.  In that case, you might need appropriate Mac adapters as well.

Cost Analysis of this setup is as follows
### Fixed Costs
1. LCD Monitor - 5000 INR approx.
2. Laptop - 60,000 INR (or Macbook - 1,00,000 INR) approx.
3. Display Accessories (HDMI/Adapter) - 1500 INR approx.
TOTAL - 66,500 INR approx in case of laptop and 1,06,500 INR approx in case of Macbook

### Variable Costs
1. Electricity (as per hardware)

### Advantages
1. Easy to setup
2. Less power consumption than Option 1
3. Provides inbuilt power backup in case of power outage.

### Disadvantages
1. Laptop's inbuilt screen goes unused
2. Just to run a browser, a fully loaded OS is used. This slows down the system.
3. Costly solution for a simple browser based functionality

## Option 3 : Apple TV Wallboard (with hacks)
I recently came across [this blog post](http://blogs.atlassian.com/2011/10/using_an_appletv_as_a_build_monitor/) at Atlassian's site which talks about how to use JIRA wallboards by jailbreaking Apple TV with a third party software.  Read the original blog post for more information.

Let's do the cost analysis of this setup

### Fixed Costs
1. LCD Monitor -  5000 INR approx
2. Apple TV - 13,000 INR approx
Total - 18,000 INR approx

### Variable Costs
1. Power consumption

### Advantages
1. Less power consumption than Option 1 and 2
2. Takes up very less area

### Disadvantages
1. Jailbreaking AppleTV voids the warranty
2. Not sure when this hack will stop working

## Option 4: Raspberry Pi Wallboard
Raspberry Pi is a credit-card sized computer that runs on Linux. It is generally available in [market](http://potentiallabs.com/cart/IoT-Starter-Kits-Arduino-Raspberry-Pi-ESP8266/raspberry-pi-2-iot-kit-hyderabad-india), with a package containing all interfaces like HDMI, USB, etc.

You can set this up to serve a LCD/LED monitor using HDMI Interface.  This can connect to the network using Ethernet or even a USB Wifi Dongle.  For all practical purposes, you can use this as a personal computer, connecting keyboard and mouse using USB.

Instead of hard disk, a SD Card serves as a primary memory.  The OS is light-weight and can be used on a daily basis without significant lag in performance.

![raspi.jpg]({{site.baseurl}}/images/raspi.jpg)
![raspi2.jpg]({{site.baseurl}}/images/raspi2.jpg)

### Fixed Costs
1. LCD Monitor -  5000 INR approx
2. Raspberry Pi Kit - 4,000 INR approx
Total - 9,000 INR approx

### Variable Costs
1. Power consumption

### Advantages
1. Less power consumption than Options 1, 2 and 3
2. Very less area required
3. Cheaper than options 1,2 and 3

### Disadvantages
1. Wifi Connectivity in Raspberry Pi is known to [get complicated](http://weworkweplay.com/play/automatically-connect-a-raspberry-pi-to-a-wifi-network/) under certain circumstances
2. Might need to buy a casing in case of crowded places otherwise, prone to mishandling as all the parts are exposed.
