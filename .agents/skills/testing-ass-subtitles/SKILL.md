# ASS Subtitle Testing

Use this skill when testing new `Monster - NN.rus_new.ass` subtitle files generated from an English ASS grid and an old Russian source file.

## Devin Secrets Needed

None. Subtitle validation uses local repository files only.

## Setup

- This is a subtitle-only repository; there may be no runnable web app or UI.
- Read old Russian subtitle sources with `cp1251`.
- Read English grid and new `.rus_new.ass` outputs with `utf-8-sig`.
- New `.rus_new.ass` files should start with UTF-8 BOM bytes `EF BB BF`.

## Validation Checklist

1. Compare `Dialogue:` count between the English source and the new Russian file; counts must be identical.
2. Compare every dialogue field before the text field against the English source. If the English style is `Dialogue`, expect the Russian output style to be `Default` when that is the project convention.
3. Verify only approved styles are present. For Monster subtitles, expected output styles are usually `Default`, `Stuff`, and `Signs`.
4. Check text quality guardrails:
   - no empty dialogue texts
   - no punctuation-only or fragment-only texts
   - no adjacent exact duplicate visible texts unless intentionally repeated by meaning
   - no visible segment over 80 characters after splitting on `\N`
5. Strip ASS override tags like `{\pos(...)}` before text-quality checks, but preserve them for structure/grid comparison where they are part of the text field.

## Semantic Spot-Checks

- Do not rely only on nearby timings. Build English/Russian slot pairs for high-risk scenes and verify the Russian line belongs to the same English meaning slot.
- Include scenes with split long Russian lines, interleaved narration/news, and any scene recently edited for alignment.
- For each checked Russian phrase, confirm it is either an exact old-source phrase or a sensible split fragment from a longer old-source line.
- Add an explicit regression guard for any scene where slot drift was previously observed; for example, assert the exact Russian text in the previously shifted slot and assert that the neighboring wrong phrase is absent.

## Evidence to Report

- Save command output showing counts, mismatches, style results, quality guardrail counts, and semantic spot-check results.
- For subtitle-only repos, do not record the desktop if all testing is shell-only; attach text output or a generated screenshot/image of the command summary instead.
- When testing an open PR, post one concise PR comment with pass/fail bullets and link the Devin session.
