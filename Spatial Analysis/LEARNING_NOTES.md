# Learning notes: spatial project (do not commit to GitHub)

## The four new concepts

| Concept | What it means | Why it matters |
|---|---|---|
| `sf` object | A data frame with a `geometry` column | All dplyr verbs still work; spatial data is not a separate world |
| CRS | Coordinate reference system: how the globe maps onto a flat surface | The wrong one distorts area and misleads readers |
| EPSG:4326 | Longitude/latitude, the default for most sources | Fine for storage, poor for European maps |
| EPSG:3035 | ETRS89-LAEA, the EU equal-area standard | Use this for every map of Europe |
| Attribute join | `left_join()` on a shared code (`geo`) | Geometry and statistics arrive from different places |

## Expect breakage, and treat it as normal

Eurostat changes dataset codes and column names. If the render fails:

1. **`get_eurostat()` returns nothing.** Run the discovery chunk in
   Section 2 with `eval: true` and find the current code.
2. **The `unit` filter empties the table.** Read the unit table printed
   just above it and change `"PC_UAA"` to whatever the data actually
   contains.
3. **`rename(year = all_of(time_col))` fails.** Run
   `names(organic_raw)` and find the time column by eye.
4. **Fewer geographies match than expected.** Print the unmatched codes
   with `map_data |> filter(is.na(values)) |> pull(geo)` and check
   whether they are non-EU countries or genuine failures.

Debugging API changes is ordinary analyst work, not evidence that you
chose the wrong career.

## The exercises

1. **Drop the projection (YOUR TURN 1).** Teaches you what a CRS
   actually does, by showing you the damage when you skip it.
2. **Add country labels (YOUR TURN 2).** Teaches you that presentation
   choices affect whether anyone can read your output.

## Interview questions this project invites

1. Why EPSG:3035 rather than the default 4326?
2. How did you verify the join between geometry and statistics worked?
3. Your map shows clustering. How would you demonstrate that
   statistically rather than visually?
4. What does your linear projection assume, and where does that
   assumption fail?
5. Why is certified organic area an imperfect measure of sustainable
   farming?

Question 3 is the one that separates candidates. The honest answer is
Moran's I, and admitting you have not run it yet is better than
pretending the map proves the claim.

## Sequencing reminder

Finish project one before this one. Two half-built projects impress
nobody; one complete project you can defend does.
