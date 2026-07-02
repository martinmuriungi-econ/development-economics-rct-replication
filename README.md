# Replication Project: Loans, Grants and Microenterprise Development

This repository contains a replication and extension exercise based on:

Crepon, B., Komi, M., & Osman, A. (2024). "Is It Who You Are or What You Get? Comparing the Impacts of Loans and Grants for Microenterprise Development." *American Economic Journal: Applied Economics*, 16(1), 286-313.

The project was completed as an MSc Economics replication assignment. It reproduces selected tables and figures from the published paper using the authors' replication package, then extends the core research question to a new setting using Nigerian household survey data.

## Research Question

The paper asks whether microenterprise outcomes are shaped more by the type of capital support offered or by the characteristics of the entrepreneurs who receive support. In particular, it compares the effects of three financial instruments - subsidized loans, cash grants and in-kind grants - on business creation, business assets, profits, employment, income and time use.

This question is central to development economics and policy design. Governments, NGOs and multilateral organizations frequently use credit and grant programs to promote entrepreneurship and poverty reduction. If repayment obligations, liquidity constraints and contract structure determine program impacts, policy should focus on product design. If recipient heterogeneity is more important, screening, targeting and complementary support may be more effective.

## Empirical Design

The original study is a randomized controlled trial conducted in Egypt among screened and loan-approved microenterprise applicants. After applicants had passed the lending screen, they were randomly assigned to one of four groups:

- Control group: no capital transfer
- Microcredit: subsidized loan offer
- In-kind grant
- Cash grant

This post-approval randomization holds applicant selection approximately constant while varying the financial instrument. The replication estimates intention-to-treat effects using ordinary least squares regressions with cohort or round fixed effects and heteroskedasticity-robust standard errors. The analysis is conducted separately by gender and includes tests of equality across treatment arms. The figure scripts also implement distributional analysis using quantile treatment effect methods.

## Repository Structure

```text
.
|-- 00_SetUp.do
|-- Data/
|   |-- AEJ_CKO_baseline.dta
|   |-- AEJ_CKO_endline.dta
|   |-- AEJ_CKO_baseline_edited.dta
|   |-- AEJ_CKO_endline_edited.dta
|   |-- AEJ_CKO_baseline_endline_edited.dta
|   `-- analysis_data.csv
|-- Do Files/
|   |-- 01_DataClean.do
|   |-- 02_Main_Tables.do
|   |-- 03_Main_Figures.do
|   `-- Appendix/
|       |-- AppendixA.do
|       |-- AppendixB.do
|       |-- AppendixC.do
|       |-- AppendixD.do
|       |-- AppendixE.do
|       |-- fdr_sharpened_qvalues.do
|       `-- R_ML_CDDF/
|           |-- cleanSFSDdata_forCDDF.do
|           |-- ML_Functions.R
|           `-- SFSD_CDDF_5Groups.R
|-- Logs/
|-- Output/
|   |-- Figures/Main_Figures/
|   `-- Tables/Main_Tables/
|-- Surveys/
`-- EC982 Replication assignment-ADM 5699720.docx
```

## Replication Workflow

The replication is controlled by `00_SetUp.do`, which defines the project root and then runs the full pipeline:

1. `01_DataClean.do` constructs treatment indicators, gender interactions, cleaned baseline and endline outcomes, winsorized income and asset measures, standardized indices, time-use variables and merged baseline-endline datasets.
2. `02_Main_Tables.do` reproduces the main in-text tables, including baseline balance, compliance, financial instrument use, business outcomes, income and employment, time use and heterogeneity tests.
3. `03_Main_Figures.do` reproduces the main figures, including capital assistance received by gender and quantile treatment effect routines for income.
4. `Appendix/*.do` runs additional robustness, appendix and multiple-testing procedures, including false-discovery-rate sharpened q-values and machine-learning related routines.

## Main Replication Outputs

The current output folder contains:

- `Tab1_BaselineBalance.csv`
- `Tab2_Compliance(Female)_rerun.tex`
- `Tab2_Compliance(Male)_rerun.tex`
- `Tab3_Loan(Female).tex`
- `Tab3_Loan(Male).tex`
- `Tab4_business(Female).tex`
- `Tab4_business(Male).tex`
- `Tab5_Income(Female).tex`
- `Tab5_Income(Male).tex`
- `Tab6_time(Female).tex`
- `Tab6_time(Male).tex`
- `Graph_CA_female.png`
- `Graph_CA_male.png`

## Summary of Replication Results

### Baseline Balance

The baseline balance table confirms that treatment groups are broadly comparable before the intervention. Most differences between the control group and treatment arms are small and statistically insignificant. The assignment write-up reports a joint balance-test p-value of 0.11, consistent with successful randomization.

### Compliance and Treatment Delivery

Compliance with treatment assignment is high. The replicated compliance tables show that:

- Loan take-up is approximately 88.2 percent for women and 86.2 percent for men.
- In-kind grant receipt is approximately 99.2 percent for women and 98.5 percent for men.
- Cash grant receipt is approximately 97.2 percent for women and 97.9 percent for men.

These results support the internal validity of the experiment: assigned treatment status substantially changed actual capital receipt.

### Financial Instrument Use

The financial-use tables show that assignment to the loan arm increases the probability of having a loan. Grant assignment substantially increases total external funding. Among women, in-kind and cash grants also raise savings, suggesting that grant receipt changes both enterprise financing and short-run liquidity. For men, the savings effects are weaker and not statistically significant in the replicated tables.

### Business Outcomes

The strongest business impacts appear among women. In the female sample:

- Microcredit increases business ownership by about 14 percentage points and raises the standardized business index by 0.35 standard deviations.
- In-kind grants increase business ownership by about 24 percentage points and raise the standardized business index by 0.66 standard deviations.
- Cash grants increase business ownership by about 22 percentage points and raise the standardized business index by 0.45 standard deviations.

Grant treatments also produce large and statistically significant increases in business assets, revenue, expenses and profits for women. Among men, treatment effects on business ownership are positive, but effects on profits and the broader business index are weaker and generally less precisely estimated.

### Employment and Income

The income tables again show stronger effects for women. In the female sample, all three treatment arms increase work activity, profits, labor income and total income, with particularly strong effects for grant recipients. In the male sample, estimated effects on employment, profits, labor income and total income are small and statistically insignificant.

Overall, the replication supports the paper's conclusion that the form of capital matters and that grants generate larger improvements in microenterprise performance than loans in this setting, especially for women.

## Broad Replication: Nigeria Household Credit and Welfare

As an external-validity exercise, the project applies the paper's broad theme to Nigeria using the General Household Survey Panel, Wave 5. The extension asks whether loan approval is associated with short-run household welfare, measured by log food expenditure.

The preferred specification estimates:

```text
ln(Food Expenditure_i) = beta * LoanApproved_i + State FE + Sector FE + epsilon_i
```

The estimated coefficient on loan approval is negative and statistically insignificant in the preferred model, approximately -0.147 log points with a p-value of 0.147. This result does not provide evidence that loan approval increases short-run food consumption in the Nigerian observational setting.

This broad replication is interpreted cautiously. Unlike the original RCT, loan approval in the Nigerian data is not randomly assigned. The estimate may reflect selection into borrowing, adverse shocks, credit rationing or differences in institutional context. The exercise therefore provides suggestive external-validity evidence rather than a causal estimate.

## Software and Packages

The main replication is written in Stata. The master setup file references the following user-written Stata packages and commands:

- `estout` / `esttab` / `eststo` for regression table output
- `winsor2` for winsorized outcome construction
- `grstyle` for graph formatting
- `ihstrans` for inverse hyperbolic sine transformations
- `fsum` for formatted summary statistics
- `lassopack` and `pdslasso` for high-dimensional and machine-learning related routines
- `leebounds`, `moremata`, `kdens` and `ivqte` for additional estimation and robustness procedures

The extension and auxiliary analysis use R for cross-software replication, robust standard errors and machine-learning related appendix routines.

## How to Reproduce

1. Download the replication package from the journal archive or AEA data repository.
2. Open `00_SetUp.do`.
3. Update the `global root` path so it points to the local repository folder.
4. Install any missing Stata dependencies listed in the setup file.
5. Run:

```stata
do 00_SetUp.do
```

Alternatively, run each stage manually:

```stata
do "Do Files/01_DataClean.do"
do "Do Files/02_Main_Tables.do"
do "Do Files/03_Main_Figures.do"
```

The generated tables and figures will be written to `Output/Tables/Main_Tables/` and `Output/Figures/Main_Figures/`.

## Technical Skills Demonstrated

This project demonstrates applied research skills relevant for research assistant and pre-doctoral roles at organizations such as the World Bank, J-PAL and IPA:

- Reproducible empirical workflow design using Stata master scripts and modular do-files
- Cleaning and merging baseline and endline survey data
- Construction of treatment indicators, gender interactions, household welfare measures and standardized outcome indices
- Implementation of randomized-control-trial analysis with fixed effects and robust standard errors
- Production of publication-style regression tables using `esttab`
- Generation of figures and treatment-effect visualizations
- Gender-disaggregated impact analysis
- Interpretation of treatment compliance, balance tests and intention-to-treat estimates
- Quantile and heterogeneity analysis
- Multiple-testing and false-discovery-rate adjustment procedures
- Cross-software replication using R
- External-validity analysis using nationally representative household survey data
- Clear documentation of empirical methods, results and limitations

## Research Position Relevance

The repository illustrates the ability to move from a published development economics paper to a working replication pipeline, understand the identification strategy, reproduce core empirical outputs and evaluate external validity in a new context. These are core competencies for applied microeconomics research roles involving randomized evaluations, household survey data, impact evaluation, poverty analysis and policy-oriented empirical work.

## Notes

Raw data should be obtained from the official replication archive where required. Users should verify data-access and redistribution rules before publishing this repository publicly.
