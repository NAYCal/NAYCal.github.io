---
layout: post
title: "Validation at Scale: Early Lessons from Research Labs to Real-World Impact"
summary: "What production systems, an LLM research lab, and neural rendering taught me about why validation can be as demanding as building the model itself."
date: 2025-07-27
tags: [Validation, Machine Learning, Research, Career]
source_url: "https://www.linkedin.com/pulse/validation-scale-early-lessons-from-research-labs-real-world-ng-rxh4c/"
source_name: "LinkedIn"
---

After spending 1.5 years at Fortune 1, I've gained a deeper appreciation for a concept that began to resonate during my undergraduate studies: the importance of **validation**.

As the primary developer for Walmart Global Tech's new replenishment order management system, and later as a contributor to data pipelines for Demand Forecasting using regression models, I have seen firsthand how essential validation is at scale. Even a minor issue in production has enormous financial consequences, potentially costing millions or even billions of dollars. Beyond ensuring system reliability, validation also enables teams to measure the tangible business value of their work. As a relatively new software engineer, I am continuing to learn how to increase business visibility and identify high-impact areas where efficient, validated solutions can be implemented.

My education at the University of California, Berkeley established a foundation for the skills I now rely on daily: solving complex, real-world challenges and writing clean, maintainable code designed for collaborative workflows. Yet, among the most valuable lessons learned at Berkeley, the significance of validation stands out clearly.

While working in a linguistics lab under Professor Zehlia Babaci-Wilhite, our research focused on how large language models (LLMs) could better incorporate cultural context, an important component in her mission to enhance early language education. One of our biggest challenges was evaluating model performance in this domain. Cultural accuracy is inherently difficult to quantify, making validation an intricate blend of extensive manual effort and the innovative creation of specialized evaluation methods and datasets.

This focus on validation extended beyond formal research. Even smaller side projects with friends and classmates (special thanks to Bridget Agyare), such as Fine-Tuning GPT-2 for Historical Comprehension ([available on GitHub](https://github.com/NAYCal/GPT-Histories)), required careful manual inspection to ensure that outputs aligned meaningfully with cultural and historical expectations.

Further, my work in computational photography highlighted another challenge in validation, especially as machine learning systems become integral parts of daily life. When developing convolutional neural networks (CNNs) to generate images from novel angles, traditional metrics like Structural Similarity Index (SSIM) are usually sufficient, provided reference images exist. However, the problem deepens when generating views that have no real-world reference. What happens when outputs with visible artifacts inexplicably score higher on automated validation metrics than visually cleaner ones?

My experience developing Neural Radiance Fields (NeRF), as illustrated below, and my ongoing research into techniques such as Gaussian Splattering, have reinforced that human judgment remains an indispensable part of validation, even as we strive toward robust automation.

<figure>
  <img src="{{ '/assets/img/nerf-lego-turntable.gif' | relative_url }}" alt="Turntable animation of a Lego bulldozer rendered by a trained NeRF" width="200" height="200">
  <figcaption>My NeRF results from undergraduate. <a href="https://github.com/NAYCal/Neural-Radiance-Field-">Code on GitHub</a>.</figcaption>
</figure>

Ultimately, my journey has underscored a key insight: building comprehensive and effective automated validation pipelines can be as intricate, demanding, and rewarding as developing the core machine learning models themselves.
