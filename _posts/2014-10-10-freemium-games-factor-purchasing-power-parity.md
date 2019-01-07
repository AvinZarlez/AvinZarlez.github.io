---
id: 73131
title: Should freemium games factor in Purchasing Power Parity?
date: 2014-10-10T10:00:36+00:00
author: Tobiah
excerpt: |
  One of the biggest strengths with the games industry today is how global it is. People download and play games from all over the work. Developers who realize this already make sure their games are localized for other languages. This leads to more players, more engagement/viral growth, and ultimately more revenue.
  
  However, but I seldom hear about game developers customizing the price of their games on a per currency basis.
  
  That's where Purchasing Power Parity (PPP) comes in.
layout: post
guid: http://www.tobiahmarks.com/?p=73131
permalink: /2014/10/10/freemium-games-factor-purchasing-power-parity/
categories:
  - In App Purchases
  - Links
  - Monetization
tags:
  - PPP
---
One of the biggest strengths with the games industry today is how global it is. People download and play games from all over the work. Developers who realize this already make sure their games are localized for other languages. This leads to more players, more engagement/viral growth, and ultimately more revenue.

However, but I seldom hear about game developers customizing the price of their games on a per _currency_ basis.

That''s where Purchasing Power Parity (PPP) comes in.<!--more-->I recently stumbled upon an article called "

<a href="https://medium.com/marketing-hashcube/one-simple-hack-to-crack-iaps-in-the-developing-world-a3a2751a0f94" target="_blank"><em>One simple Hack to Crack IAPs in the Developing World</em></a>". The article has been out a couple months now, so this may be old info to some of you out there. I think it''s worth reading if you haven''t yet already .

In it, Gurinder Pal Singh makes a great argument for developers to consider the Purchasing Power Parity of each currency, not just the exchange rate.

What is Purchasing Power Parity exactly? In Gurinder''s own words:

> <p class="graf--p">
>   The problem is that all currencies are not created equal, some are more valuable than others. A $100 bill, when converted at the exchange rate, will buy you more stuff in India or China or Mexico or Romania and so on, than it would in the United States. So a Dollar has more purchasing power in these countries than in the United States at the international exchange rate. And that is where the concept of <a class="markup--anchor markup--p-anchor" href="http://en.wikipedia.org/wiki/Purchasing_power_parity" target="_blank" rel="nofollow" data-href="http://en.wikipedia.org/wiki/Purchasing_power_parity">Purchasing Power Parity (PPP)</a> is born.
> </p>
> 
> <p class="graf--p">
>   Every year, the <a class="markup--anchor markup--p-anchor" href="http://data.worldbank.org/indicator/PA.NUS.PPP" target="_blank" rel="nofollow" data-href="http://data.worldbank.org/indicator/PA.NUS.PPP">World bank takes out a list of PPP conversion factors</a> where they estimate the amount of any country’s local currency required to buy the same amount of goods that $1 would buy you in the US. For example, India’s PPP conversion factor is around Rs. 17 but the current exchange rate is Rs. 60. So, Rs. 17 would buy you the same amount of goods in India as $1 (or Rs. 60) would buy you in the United States. That is less than 1/3rd of the exchange rate!
> </p>

That means that a "Tier 1" In App Purchase (IAP) costs three times as much in India than it does in the United States!

No wonder the conversation ratio is not as good in those countries. Could you image a developer tripling the price of all their in all purchases? Sales would drop sharply!

Gurinder decided to run an experiment. Manually adjust each In App Purchase based on the current Purchasing Power Parity in the players currency. That means with the above example if 10 coin costs $1 USD, he would charge Rs. 17 (the PPP) rather than Rs. 60 (exchange rate)

The results? The number of transactions in those countries increased by 1100%, and revenue from those countries increased by 400%!

That''s a pretty amazing success story, considering how easily copyable his methods are.

Check out the <a href="https://medium.com/marketing-hashcube/one-simple-hack-to-crack-iaps-in-the-developing-world-a3a2751a0f94" target="_blank">original article</a> for more details. I know for me personally, I am going to consider PPP when localizing my games from now on.

-Tobiah