---
layout: post
title:  "GSoC 2017: Directly accessing MusicBrainz DB in CritiqueBrainz"
date:   2017-08-28 15:53:08 +0530
categories: gsoc
---

<i> Find original blog here: https://blog.musicbrainz.org/2017/08/28/gsoc-2017-directly-accessing-musicbrainz-db-in-critiquebrainz/ </i>

Hello, everyone! The summer of 2017 was fantastic for me! :)
I participated in Google Summer of Code 2017 contributing code to CritiqueBrainz, which is a child project of the MetaBrainz Foundation. Alastair Porter mentored me during this GSoC programme. This post summarizes my contributions to the project and experiences that I had throughout the summer.

I started contributing to CritiqueBrainz in January, 2017 and before the start of the SoC programme, I mainly worked on writing raw SQL for retrieving data from the CB database and replacing the ORM code (CB-230). Other than that I worked on issues like CB-120, CB-235 and other minor bugs and issues. They were my first proper contributions to the open source world. Thank you MetaBrainz!!

For the Google Summer of Code 2017, my project involved retrieving data related to various entities (release-groups, artists, releases, events and places) directly from the MusicBrainz database instead of querying the MusicBrainz web service (CB-231). This became necessary as some pages on CB required to fetch too much data and thus made many requests to the MB web service. These pages were taking a long time to load. Thus, by connecting directly to the database, we could reduce the load time of these pages.

Here is a summary of my contributions to the project during the summer:

<i> Accessing the MusicBrainz database </i>

New Infrastructure is allowing us to easily read data directly from the MusicBrainz database. For accessing the database in the development environment, another service running the MusicBrainz database was added which uses an existing Docker image which the MusicBrainz project was already using. This allowed us to share resources between projects. I worked on adding an option to download the database dumps and import the data into the database (see PR#523). Also, I added the service in CB docker-compose files and updated the documentation for setting up the development environment (see PR#115 and PR#92).

<i> Fetching data using mbdata.models </i>

After setting up the development environment, my mentor suggested to me to use the mbdata package for writing queries to fetch data from the database instead of writing raw SQL. I worked on retrieving information for the entity: places and added helpers for fetching the relationship information. Following that, I worked on retrieving information for other entities (release-groups, releases, events, and artists). Also, since SQLAlchemy makes lazy queries to the database, a number of queries were being issued to the database. This could slow things down as for each query it was going to require one trip to the SQL server (network trip in production). So, as suggested by my mentor, I also worked on reducing the number of queries made for fetching data related to each entity (see PR#135). For pages that made a number of requests to the web service, I made this PR#121 for fetching information related to multiple entities at the same time.

<i> Testing </i>

For testing, the database queries are mocked using the unittest.mock Python package. The tests added make sure that the code (serializing RowProxy objects to dictionaries, caching, etc.) works properly (see PR#134). Adding up a new service (as a separate Docker container) in the test environment and running tests was taking too much time (in creating the tables and truncating them). So as suggested by my mentors, mocking the database queries was the best option. Throughout my GSoC period, I learned how important it was to write tests (especially when you break things more when you fix something) and make them run fast. I learned that «If tests don’t run fast, they would be a distraction rather than a help» (quoting from the book “The Art of Agile Development” by James Shore).
Other than these, I also worked on some UI/UX issues, namely CB-80 (adding option to filter releases with reviews), CB-84 (ordering release groups according to release year) and CB-261 (authenticating requests to Spotify Web API). CB-130 (reviewing entities with MBID redirects – see PR#145) was also solved while solving a production server issue.

This summer was awesome for me. I learned a lot of new things and techniques for writing better code. Thanks to my mentors, Alastair Porter and Roman Tsukanov. Also, great thanks to the lovely MetaBrainz community and Google for this opportunity. I’m really looking forward to keep contributing to CritiqueBrainz and to dive into other MetaBrainz projects.
