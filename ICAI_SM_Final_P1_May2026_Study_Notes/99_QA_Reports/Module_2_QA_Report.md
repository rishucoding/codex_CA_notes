# Module 2 QA Report

## Overall Verdict

**Pass with fixes.** The Module 2 notes are generally accurate, exam-oriented, and internally consistent. The main problems are not conceptual collapse but a handful of rendering/formatting defects in worked examples, plus one practice-guide file that is a bit too abstract for a mixed-question set.

Note: I could not locate the matching PDF files for 012-022 in the workspace, so this review was done against the Markdown set and the underlying standard coverage rather than a literal PDF line-by-line diff.

## Per-File Findings

### 012. `012_Module_2_Initial_Pages_Overview.md`

Coverage is good for an opener. It gives the module map, sequencing, and exam strategy cleanly.

Required fixes: none.

Nice-to-have: add one short line that separates chapter content from module-level navigation more explicitly, if you want the opener to act as a stricter orientation page.

### 013. `013_Chapter_5_Unit_1_Ind_AS_2_Inventories.md`

Coverage is strong. The note captures scope, cost build-up, cost formulas, NRV, write-down/reversal, and the service-inventory angle well.

Required fixes:
- Fix broken inline-code formatting in the worked examples. The currency amounts in the example block render as stray backticks rather than clean values, especially around lines 288-316.

Nice-to-have:
- Add one tiny reminder on the broker-trader / agricultural-produce measurement exception so the special cases stand out faster in revision.

### 014. `014_Chapter_5_Unit_2_Ind_AS_16_Property_Plant_and_Equipment.md`

Coverage is strong and the chapter logic is well organized. Recognition, initial cost, component accounting, revaluation, depreciation, and derecognition are all present.

Required fixes:
- Fix the broken inline-code formatting in the worked examples around lines 263-291. The numeric examples are readable as prose, but the markdown is malformed.

Nice-to-have:
- Add one compact worked CGU-style or component-replacement example with a little more numeric working, since this chapter is often tested with arithmetic.

### 015. `015_Chapter_5_Unit_3_Ind_AS_23_Borrowing_Costs.md`

Coverage is good. The note handles qualifying asset logic, commencement/suspension/cessation, specific borrowings, and general borrowings clearly.

Required fixes: none.

Nice-to-have:
- Tighten the exchange-difference note if the source PDF uses narrower wording on when FX differences count as borrowing costs.

### 016. `016_Chapter_5_Unit_4_Ind_AS_36_Impairment_of_Assets.md`

Coverage is strong. The recoverable-amount logic, CGU treatment, goodwill rules, and reversal ceiling are all in place.

Required fixes: none.

Nice-to-have:
- Add one short CGU allocation example so the pro-rata loss allocation is easier to rehearse.
- Add a one-line reminder on the reversal ceiling using the "no impairment" carrying amount language.

### 017. `017_Chapter_5_Unit_5_Ind_AS_38_Intangible_Assets.md`

Coverage is strong. Recognition, research vs development, finite/indefinite life, revaluation, amortisation, and disclosure are all covered.

Required fixes:
- Fix broken inline-code formatting in the worked examples around lines 333-371. The example values are slipping out of markdown formatting.

Nice-to-have:
- Add one short line reinforcing why internally generated brands, mastheads, and customer lists stay out even when they have obvious commercial value.

### 018. `018_Chapter_5_Unit_6_Ind_AS_40_Investment_Property.md`

Coverage is good. The distinction between investment property, PPE, and inventory is clear, and the transfer logic is sensible.

Required fixes:
- Fix the broken inline-code formatting in the fair value example around lines 245-253.

Nice-to-have:
- Tighten the rare-case wording on fair value reliability so it mirrors the source material more closely.

### 019. `019_Chapter_5_Unit_7_Ind_AS_105_Non_current_Assets_Held_for_Sale_and_Discontinued_Operations.md`

Coverage is good. The held-for-sale gates, measurement rule, depreciation stop, disposal-group logic, and discontinued-operation presentation are all present.

Required fixes: none.

Nice-to-have:
- Add one very short checklist separating "held for sale" classification from "discontinued operation" presentation, since that is the easiest place for students to blur the two.

### 020. `020_Chapter_5_Unit_8_Ind_AS_116_Leases.md`

Coverage is strong. The lease test, component separation, lessee exemptions, lease liability / ROU asset logic, lessor classification, modifications, and sale-and-leaseback framing are all there.

Required fixes: none.

Nice-to-have:
- Add one sentence reminding the reader that sale-and-leaseback answers turn completely if no sale accounting occurs.

### 021. `021_Module_2_Practice_Questions_Pattern_Guide.md`

This file is useful, but it is more meta than the source practice set. As a pattern guide, that is acceptable, but it does over-compress the variety in a real mixed-question set.

Required fixes:
- Add a couple of concrete mixed-pattern examples, especially for standard pairings that students commonly miss.

Nice-to-have:
- Include one short example each for a PPE plus borrowing-cost question and a lease plus held-for-sale question.

### 022. `022_Module_2_Ind_AS_Puzzlers_Trap_Guide.md`

Coverage is clean and the trap framing works well. It is a good revision sheet.

Required fixes: none.

Nice-to-have:
- Add one reminder on discounting costs to sell when the sale sits beyond one year.
- Add one compact trap note on short-term versus low-value lease relief.

## Required Fixes Summary

1. Fix the broken inline-code formatting in the worked examples in 013, 014, 017, and 018.
2. Add a few concrete mixed-question examples to 021 so the pattern guide is less abstract.

## Nice-to-Have Improvements Summary

- Add one CGU worked example in 016.
- Add one or two micro-examples in 015, 019, and 020 where the source logic is easy to blur in exam conditions.
- Add one or two special-case reminders in 013 and 017.

