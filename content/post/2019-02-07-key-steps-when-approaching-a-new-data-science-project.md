---
title: Key Steps When Approaching a New Data Science Project
author: Devon Shurick
date: '2019-02-07'
slug: key-steps-when-approaching-a-new-data-science-project
categories: []
tags: []
---

1. **Figuring out what the customer wants to figure out.**

    For most people, machine learning and big data are simply buzzwords. The process usually starts with someone in some company getting the bright idea that “we need to do something with machine learning” or “we need to do something with big data”, which is very poor reasoning, but that’s besides the point.

    Once the company tells me about their business and their problems (everyone has problems), I start figuring out how to convert that into problem statements that can be solved using data science, if possible. It is very important to come up with a problem that is both solvable within a realistic time frame and that can genuinely help the company if solved. Thus, the problem should be defined in close collaboration with the customer/stakeholder. Once we’ve narrowed it down to a single idea, it’s time to attack the data.

2. **Exploring the data.**

    Once I have access to the database/API/data repository/data lake/data whatever, I start browsing through the data. Extract, visualize, ask questions, rinse and repeat. It’s important to have a domain expert that’s willing to share knowledge about the data. Otherwise, it’s easy to get stuck.

3. **Identifying statistical correlations.**

    Next, I look for variables that are related and try to find statistically meaningful correlations. This will assist in selecting and creating the right features, as well as understanding how everything fits together.

4. **Constructing a proof of concept.**

    Before investing a lot of time and energy on developing a full-scale solution and putting it into production, I find it useful to do a quick proof of concept, or mockup, to show the customer that I can indeed create something of value. If this is successful, it will be much easier to gain support and acceptance for the project with the right people.

5. **Wrangling the data and creating features.**

    Once the proof of concept is finalized and the core project begins, it is all about finding the right features to use as inputs and converting them into convenient formats. This can include feature scaling/normalization, encoding class labels and categorical data and other preprocessing techniques. Often, this is the most time-consuming step of the project.

6. **Creating subsets of the data.**

    In order to test and cross-validate the results, the dataset needs to be split into several partitions. With time series data, this can sometimes be tricky.

7. **Training and testing a bunch of algorithms.**

    Finding the best algorithm is often an exercise in trial and error. With modern tools and a good pipeline, this is rather simple. Sometimes I have to implement something from scratch, but even that is not that hard with all the available literature.

8. **Tuning the hyperparameters.**

    To really optimize things, the hyperparameters should be tuned according to some learning technique and not just arbitrarily chosen. If the project has limited hours, I might skip this step almost entirely.

9. **Putting the solution into production.**

    At this stage, I either have a model, an ensemble of models or a solution that dynamically selects a model. Whatever the solution, it has to be automated and deployed into a production environment so that it can run continuously as a service. Not all data science projects are like this, though. Sometimes, the initial analysis is enough. Other times, the model is used to take real-time actions, and the production solution becomes very important.

10. **Documenting.**

    I’m one of the few engineers who actually likes to document things I do. That’s the scientist in me as a data scientist. Sadly, very few people ever read that stuff unless it’s an actual publication, which in industry it’s usually not.

11. **Presenting to management.**

    If the project has been a success, some top-level managers will surely have heard about it at this point. They will be wanting a presentation, and one that isn’t too technical. I try to focus on the bigger scheme and use lots of illustrations, but I don’t shy away from buzzwords, because we all know that managers love them.

12. **Celebrating a job well done.**

    The project is finished and it’s time for a celebration. In reality, this means jumping straight to the next project, because data science is awesome!

---

This material comes from a post on Quora by [Håkon Hapnes Strand](https://www.quora.com/profile/H%C3%A5kon-Hapnes-Strand) and can be found at [https://www.quora.com/What-are-your-key-steps-when-approaching-a-new-data-science-project](https://www.quora.com/What-are-your-key-steps-when-approaching-a-new-data-science-project)
