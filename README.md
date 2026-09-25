## India vs UK Tech Market

### How do the Indian and UK tech markets compare — in skills, tools, pay and experience?

Built from the Stack Overflow Developer Survey 2025 (49,191 respondents, 177 countries).

### The question

The Stack Overflow survey covers 177 countries, but most analyses of it report global figures. India and the UK are both well represented, so the two can be compared directly rather than averaged into a single worldwide picture.

### What I found

**The core stack is the same.** JavaScript, HTML/CSS, SQL and Python are used at almost identical rates in both countries.

**The UK leans Microsoft.** C# (34% vs 17%), PowerShell, SQL Server, Azure and NuGet are all noticeably higher.

**India leans elsewhere.** MongoDB shows the largest single gap in the skills data (45% vs 17%), along with MySQL, Firebase and Google Cloud.

**The salary gap is smaller than it first appears.** Raw medians differ by about 5x — but UK respondents have twice the experience. Comparing people at the same career stage, the gap runs from 6.3x at entry level down to 2.3x among those with 20+ years.

**AI use differs sharply.** 61% of Indian respondents use AI tools daily against 38% in the UK, and UK respondents are five times more likely to say they won't use them at all. A chi-square test confirmed this is not chance (p < 0.000001).

### What this suggests

The shared core stack means the baseline skills are similar in both markets. JavaScript, SQL and Python are equally valuable in both, so someone moving from the tech field in one country to another wouldn't need to relearn the fundamentals.

Where the markets diverge, the direction matters. Someone moving from India to the UK would find Microsoft tooling, i.e., C#, Azure, SQL Server, more commonly expected than their existing experience might suggest.

From the narrowing salary gap, it can be seen that the difference is widest at entry level and closes steadily with experience. This suggests that the worth of moving markets depends heavily on career stage.

**My Recommendation:** If I were advising someone in Indian tech considering a move to the UK, I'd say that the data points towards an earlier move in their career being more beneficial rather than later. The salary gap is widest at entry level, so the relative gain from moving is largest at the start of a career.

### How I did it

The data comes from Stack Overflow's published 2025 survey release, downloaded directly from [survey.stackoverflow.co](https://survey.stackoverflow.co/). No API or scraping was involved, the survey is released as a single file.

Before analysing anything, I checked whether the comparison was viable. India had 2,547 respondents and the UK had 2,042, which was enough to compare. I also considered narrowing this to data roles specifically, but there
were only around 112 UK respondents in data jobs — too few to draw any reliable comparisons. So I compared the whole tech market instead.

**Cleaning decisions:**

- Excluded students and retired respondents. A tech market means people working in it, and India had 359 student respondents against 83 in the UK, which would have pulled the pay and experience figures down.

- Removed salaries below $1,000 and above $500,000 a year. The highest value recorded was $9.5 million, which is a data entry error rather than a salary. This removed about 2% of responses and cut India's standard deviation from 310,266 to 39,616.

- Used fixed cutoffs rather than the standard IQR method. IQR would have set the limit at $90,523 for India and $233,484 for the UK, meaning the same salary would count as real in one country and an error in the other. Fixed bounds apply one rule to both.

- Left missing values out rather than filling them in. Since the project compares salaries between two countries, filling up empty values would mean comparing figures that were invented and not true.

The skills columns are stored as single strings with semicolons between each item, so they were split into one row per person per skill before counting. All skill figures are percentages rather than counts, since the two countries have different numbers of respondents.

For the statistical test, I used a chi-square test on AI tool adoption. Unlike the salary and experience gaps, AI use was genuinely uncertain, therefore, I chose to test it.

Built with Python (pandas, matplotlib, scipy) in a Jupyter notebook. The dashboard was built in LibreOffice Calc and saved as .xlsx.

### Limitations

- This is a voluntary survey, so respondents chose to take part. They lean towards people who use Stack Overflow, and aren't a representative sample of either country's workforce.

- Half of all respondents skipped the salary question, and 28% didn't give a country. Every figure here comes from the people who chose to answer.

- Salaries are in raw US dollars and don't account for the cost of living being much lower in India. The gap in what people can actually afford is narrower than what the dollar figures suggest.

- The chi-square test shows AI use significantly differs between the two countries, but not why it differs. This is because the survey doesn't ask.

- Experience bands are based on years worked, which doesn't capture seniority directly. Two people with ten years' experience may be at very different levels.

### Files

- `analysis.ipynb` — the full analysis, from loading the data through to the charts
- `india-uk-dashboard.xlsx` — summary tables and a dashboard built with live formulas, so the figures recalculate if the underlying data changes
- `chart-salary-experience.png` — median salary by experience band
- `chart-skills-comparison.png` — top 10 programming languages, databases and cloud platforms and tools side by side
- `chart-distributions.png` — salary and experience spread
- `README.md` — this file

The survey data itself isn't included here due to its large size. It is publicly available. Download `results.csv` from [survey.stackoverflow.co](https://survey.stackoverflow.co/). It will get downloaded as `results.txt`; place it in the project folder to run the notebook.