# A/B Test Analysis
This project analyzes a comprehensive database of books, authors, publishers, and user reviews. The goal is to extract key market insights to help a startup develop a unique value proposition for a new book-related application.

---

## ⚙️ Project Type Flags

- [ ] Exploratory Data Analysis (EDA)
- [x] SQL Analysis / Querying
- [ ] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [x] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Repository Structure](#3-repository-structure)
4. [Data Processing & Methodology](#4-data-drocessing-and-methodology)
5. [Key Insights](#5-key-insights)
6. [Deliverables](#6-deliverables)
7. [Final Verdict & Recommendations](#8-final_recomendations)
8. [Author](#7-author)

---

## 1. Project Overview

This project involves the analysis of an A/B test conducted on an e-commerce platform to determine if a new landing page design (Test Group) leads to a statistically significant increase in conversion rates compared to the existing design (Control Group). The study focuses on user behavior metrics and statistical validation to drive data-informed product decisions.

---

## 2. Objectives

Primary Objective:
Analyze the competitive landscape of the digital book market by querying a relational database to identify popular trends in publishing and user engagement.

Secondary Objective 1:
Assess the quality and reception of literary works through the aggregation of user ratings and text-based reviews to determine market "favorites."

Secondary Objective 2:
Clean and filter raw metadata (such as page counts and minimum rating thresholds) to ensure that the analysis focuses on significant publications rather than brochures or low-engagement titles.

---

## 3. Repository Structure

```
[project-root]/
│
└── notebooks/                # Jupyter, R Markdown, or Colab notebooks
│
└── visuals/                  # Exported charts, dashboard screenshots, ERD diagrams


```



---



## 4. Data processing and methodology

The project was executed in a Jupyter Notebook using Python (Pandas) and SQLAlchemy to interact with a PostgreSQL database hosted on AWS RDS.

Key SQL Implementations:
1. Filtering by Publication Date:
To understand the modern market, I identified books published after the millennial turn.

```SQL
SELECT COUNT(book_id) AS total_libros_recientes
FROM books
WHERE publication_date > '2000-01-01';
```

2. Multi-Table Aggregation:
Used LEFT JOIN to consolidate reviews and ratings per title without losing data on unreviewed books.

```SQL
SELECT b.title, COUNT(DISTINCT rev.review_id) AS total_reseñas, AVG(rat.rating) AS calificacion_promedio
FROM books AS b
LEFT JOIN reviews AS rev ON b.book_id = rev.book_id
LEFT JOIN ratings AS rat ON b.book_id = rat.book_id
GROUP BY b.book_id, b.title;
```

3. Quality Threshold Filtering:
Identified top publishers by focusing only on full-length publications (>50 pages).

```SQL
SELECT p.publisher, COUNT(b.book_id) AS total_libros
FROM publishers AS p
JOIN books AS b ON p.publisher_id = b.publisher_id
WHERE b.num_pages > 50
GROUP BY p.publisher_id, p.publisher
ORDER BY total_libros DESC LIMIT 5;
```

4. Subqueries for Statistical Significance:
Isolated authors with high average ratings, but only for books with at least 50 user ratings to ensure data reliability.

```SQL
SELECT a.author, AVG(rat.rating) AS avg_rating
FROM authors AS a
JOIN books AS b ON a.author_id = b.author_id
JOIN ratings AS rat ON b.book_id = rat.book_id
WHERE b.book_id IN (SELECT book_id FROM ratings GROUP BY book_id HAVING COUNT(rating_id) >= 50)
GROUP BY a.author_id, a.author
ORDER BY avg_rating DESC LIMIT 5;
```

5. CTEs for User Behavior Analysis:
Used Common Table Expressions to profile "Super-Users" and analyze their specific review habits.

```SQL
WITH super_usuarios AS (
    SELECT username FROM ratings GROUP BY username HAVING COUNT(book_id) > 50
)
SELECT AVG(conteo_reseñas) AS promedio_reseñas_texto
FROM (
    SELECT username, COUNT(review_id) AS conteo_reseñas
    FROM reviews
    WHERE username IN (SELECT username FROM super_usuarios)
    GROUP BY username
) AS subconsulta;
```

---


## 5. Key insights

<!--
  Findings + implications. Not just what happened - what it means.

  WHAT GOOD LOOKS LIKE:
  ✅ "Return rates, not sales volume, explain Region A's underperformance.
      Region A's return rate on home goods was 34% - more than double the
      company average. Revenue was not lost at the point of sale; it was
      lost post-sale through refunds. This points to a fulfilment or
      product quality issue specific to that region, not a demand problem."

  WHAT TO AVOID:
  ❌ "Region A had lower revenue than other regions in Q4."
     (That's an observation. It describes what happened.
      An insight says what it means and where to look next.)

  Aim for 3–6 insights. Quality over quantity.
-->

Modern Market Relevance: Query 1 confirmed a robust post-2000 catalog, ensuring findings align with current consumer preferences.

Content Quality Filtering: By isolating books with more than 50 pages (Query 3), we identified the top 5 publishers that lead the professional market, excluding minor publications.

Reliable Author Rankings: Using a 50-rating threshold (Query 4) eliminated statistical noise, identifying authors with genuine community prestige.

"Super-User" Profiling: The CTE analysis (Query 5) revealed a crucial behavioral pattern: users who rate more than 50 books (the most active readers) do not always provide long-form text reviews. This allows us to distinguish between "Express Critics" (quick scorers) and "Detailed Reviewers" (content contributors), which is vital for building a community-driven platform.

---


## 6. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| Code | Jupyter Notebook | `notebooks/Sprint-15S-2.ipynb` |



---


## 7. Final verdict and recommendations

Verdict: The data demonstrates that high reading volume does not guarantee high qualitative participation. The user base is divided between mass consumers and detailed critics.

Recommendations: * Differentiated Incentives: Implement a reward system that honors "Detailed Reviewers" to encourage high-quality text content, not just high rating volume.

Strategic Cataloging: Prioritize the catalogs of the top 5 publishers identified to ensure a professional and substantial launch library.

Personalization: Use the high-engagement author list from Query 4 to power the "Community Recommended" engine for new users.


---


## 8. Author

**Cristian Barrientos**

- 🔗 [https://www.linkedin.com/in/cristian-barrientos-pomposo/](https://www.linkedin.com/in/cristian-barrientos-pomposo/)
- 💼 [https://github.com/cris971107](https://github.com/cris971107)
- 📧 cristian971107@hotmail.com



