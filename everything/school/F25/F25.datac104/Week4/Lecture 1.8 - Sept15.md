The lecture critiques the standard narrative of algorithmic fairness through a sociotechnical lens, using the COMPAS risk assessment tool as a primary case study. The standard view of algorithms is that they are formal, automatic processes that are more objective and reliable than human judgment.

### The COMPAS Case Study

COMPAS is a proprietary algorithm used in courtrooms to predict the likelihood of a defendant reoffending, known as the recidivism rate. A ProPublica study found that the tool was biased, as **Black defendants were twice as likely as white defendants to be incorrectly labeled as higher risk**, while white defendants were more likely to be incorrectly labeled as lower risk. This raised concerns about a tool that was supposed to be objective and race-blind.

The case highlighted that **"fairness" is a contested concept**:

- **ProPublica** argued COMPAS was unfair because a fair algorithm shouldn't make prediction errors more frequently for one racial group than another.
- **Northpointe**, the developer, argued it was fair because a risk score meant the same thing regardless of race. For instance, a similar percentage of Black and white defendants who scored a "7" went on to reoffend.
- It was later noted that these two definitions of fairness are **mathematically incompatible**.

### Critiquing the Standard Response to Bias

The typical response to findings of bias is to "fix the algorithm" by auditing for disparities, using different models, or getting more and better data. However, the lecture argues for a sociotechnical response that goes beyond this "Garbage In, Garbage Out" (GIGO) framework.

A **sociotechnical critique** involves asking deeper questions about the data and the system itself:

- **What is being predicted?** The algorithm predicts not crime itself, but how police and courts observe and record crime.
- **What does the data represent?** The data reflects interactions between individuals and the criminal justice system, not an objective reality of criminal behavior.
- **What proxies are used?** "Crime" itself is a proxy, an act of classification resulting from interactions between a system and an individual.
- **What is the "ground truth"?** The model's accuracy is evaluated against a "ground truth" defined by police and courts, but other choices could be made.

### Intersectionality and the Limits of Auditing

The lecture also introduces intersectionality using the **Gender Shades study**, which found that facial recognition algorithms had the highest error rates for dark-skinned women. This oppression was only visible through an intersectional analysis, not by looking at race or gender as separate, single axes. Auditing algorithms for bias often relies on this flawed "single-axis thinking" and treats social categories like race and gender as natural kinds rather than complex social constructs.

### What "Fairness" Misses

The concept of fairness is **contextual, contested, and political**. Choosing a fairness metric (e.g., minimizing false positives or false negatives) is a political choice, and the impact of errors is not experienced uniformly by everyone.

The focus on fairness, as framed by anti-discrimination law, often translates the complex social concept of "fairness" into a narrow, technical question of whether errors are distributed equally across protected groups. This approach has several limitations:

- It **reduces structural oppression** to abstract, measurable metrics.
- It **overlooks power and privilege** by focusing only on disadvantage.
- It assumes the technology is inherently beneficial and that only its failures are an ethical problem.

### Key Takeaways

The main takeaways are that algorithmic systems like COMPAS can **reproduce and reinforce existing structural inequalities**. The standard narrative frames algorithmic bias as a technical problem of accuracy and datasets that can be fixed with better statistics. However, a sociotechnical perspective reveals that **fairness is a contested concept**, and focusing too narrowly on "bias" can obscure the larger systemic social issues that underpin these technical failures.

