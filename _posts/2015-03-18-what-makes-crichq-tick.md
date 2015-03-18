---
layout: post
title: "What makes CricHQ tick?"
description: ""
category:
tags: ["Technical"]
---
{% include JB/setup %}

Welcome to the first technical blog post at CricHQ. My name is Daniel Ryan and I’m the CricEngine lead developer here at CricHQ. Technically I’m a jack of all trades when it comes to programming at CricHQ, but there isn’t a title suited to that!
In the early days of CricHQ we had a number of problems when developing for both iOS and Android platforms. When it came to our scoring logic, there were inconsistant bugs between the two platforms. We were basically copying the same code from one platform to the other, duplicating our efforts to get the difficult (a whole article could be written on this) “cricketing logic” correct. At the time we decided to find a piece of technology which would allow us to share the same codebase across multiple platforms. Nearly everything we looked at was too slow for some of the heavy logic we had, but we found C++ fitted our needs. This was the beginning of the CricEngine.

##What is the CricEngine?

The CricEngine is a portable platform independent state machine. Its sole purpose is the capture and manipulation of cricket logic. Every event in a match of cricket can be input into the CricEngine by an API, put on an event stack and then manipulated to provide statistics about a match. The CricEngine is the core housing of CricHQ’s cricket logic. The API can be used across all platforms including iOS, Android and the web.

##Event Driven Scoring

The CricEngine is a state machine that holds the state of a cricket match currently being scored, this is driven by user actions in the form of events. The events get saved to a database and fed back into the CricEngine when reloading the match. This enables CricHQ to replay a match exactly how the scorer scored it. When each event gets pushed into the CricEngine by the scoring device, it gets streamed to the server which allows people watching the match to download each event as it happens to provide the worlds fastest live cricket feed. The CricEngine calculates statistics on the fly to generate a suite of rich interactive cricket content. Using a differential sync ensures we save internet bandwidth by only retrieving the newest events from the server. This in turn allows for very fast updates by only sending new events which are computed with existing events to update the state of a match.

##Code Reuse via Cross-Platform Compatibility

Built to be portable - Being written in C++, allows CricHQ to write once and use on all services and platforms, whilst maintaining speed and interoperability. The CricEngine library handles the game state and statistics on iOS and Android versions of CricHQ. The engine can also compile and run on Ruby, Windows Mobile, Javascript and more. This shared code backend enables defects on all platforms to be addressed simultaneously once they have been identified. Each platform communicates through a wrapper and communicates via the CricEngine API. Data is usually served from the CricEngine in JSON objects.
<img src="http://i.imgur.com/wqbreFJ.png" alt="CricEngine Diagram" style="width: 100%;" />


##Real Time Statistics Calculation

The CricEngine is able to calculate match statistics as needed. Ranging from simple calculations such as run rate(runs scored per over) and bowler economy(runs conceded per over) to complex mathematical functions like CricHQ projected scores, [MVP](http://www.thepca.co.uk/about-mvp.html) or [Duckworth Lewis Stern](http://www.thepca.co.uk/about-mvp.html) (DLS). I’ll do a quick overview of some of what we offer.

###CricHQ Projections

CricHQ Projections provide the ability to project the score for short innings(Twenty20) matches and project the percentage chance of winning throughout the course a cricket match. The projections are a proprietary algorithm developed by Dr. Paul Bracewell. Currently in progress is the ability to predict longer cricket matches such as 50 over and Test cricket. This has also been prototyped on our ruby server to allow advanced analysis of projections during the life cycle of a match.
Further calculations and algorithms are currently being developed to accurately provide rich content about a player's individual impact on the outcome of a match. This information will then be collated and aggregated via Data Warehousing to display a players match impact, allowing CricHQ to create an accurate pre match prediction. With this we have some great future possibilities.

###Most Valuable Player (MVP)

MVP is a cumulative points system that rewards players for every run scored and every wicket taken – and, how well they do it. A player achieves bonus points based on certain criteria. The points they then receive can be used to rank players in that match and are aggregated over numerous dimensions via CricHQ’s Data Warehouse.

###Duckworth Lewis Stern (DLS)

DLS is a mathematical formulation designed to calculate the target score for the team batting second in a limited overs cricket match interrupted by weather and/or other circumstances. CricHQ has a partnership in place with the ICC to vendor the DLS formula. It is used in all cricket matches scored on CricHQ and is also a stand alone calculator in the iOS application.

##Natural Language Generation

Every event scored and pushed into the CricEngine has match commentary generated for it. The CricEngine on load-up parses an advanced JSON format of commentary rules. This allows commentary to be generated (and randomised) to be different for every kind of match event, but still sound like natural language. The type of event that occurs during a match dictates the variables used when generating commentary per ball. Balls use wagon wheel data, number of runs, if it was a boundary or an extra, and the players names that had impact on the ball.



I hope this has given you a good understanding of what makes CricHQ’s scoring and viewing platforms tick, the CricEngine. Thank you for reading and feel free to leave a comment or get in touch with us directly. Keep an eye out for more blogs to come as we continue to redefine the way cricket is administered, shared, analysed and followed.


Daniel Ryan
CricEngine Lead Developer
CricHQ
