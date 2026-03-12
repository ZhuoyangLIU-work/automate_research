# How We Built the Literature Researcher Skill

A practical walkthrough of how we iterated from a prompt idea to a published Claude skill, using the built-in `skill-creator` skill in Cowork. Use this as a template for building your own.

## Starting Point

We began with a set of 9 research prompts originally shared by [Jainam Parmar (@aiwithjainam) on X](https://x.com/aiwithjainam) that turned Claude into a literature research co-pilot. The prompts covered steps like contradiction finding, citation chain tracing, gap scanning, and assumption testing. The goal was to turn this loose collection of prompts into a proper, reusable Claude skill.

## Step 1: Invoke the Skill Creator

We started by telling Claude: *"Let's create a skill together using your skill-creator skill. The skill is a literature researcher."*

Claude invoked the `skill-creator` skill, which guided us through a structured process. It asked clarifying questions about the skill's purpose, scope, and how it should behave. This is important --- don't skip the Q&A. The more specific you are upfront, the fewer rewrites you'll need.

## Step 2: Describe Each Step in Detail

Rather than having Claude guess what each step should do, we dictated the protocol step by step. For example:

> "Step 1 -- The intake protocol: I will typically give you a few papers on a topic. Before doing anything, you should (1) list every paper by author + year + core claim in one sentence, (2) group them into clusters of shared assumptions, (3) flag any papers that contradict another."

We went through all 9 steps this way. Claude drafted the SKILL.md file after each round of input.

## Step 3: Tweak and Refine

After the first draft, we made targeted tweaks:

- **Tweak 1 -- Paper indexing**: We asked the skill to automatically rename/name papers with a unified indexing system: `[NNN]-[S/D]-[YYYY]-[LastName]-[Short_Title].pdf`. This makes every reference traceable throughout the analysis.

- **Tweak 2 -- Web search sources**: We expanded the source hierarchy to include Google Scholar, arXiv, top lab blogs and technical reports (Google Research, DeepMind, Anthropic, OpenAI, Qwen, Mistral), SSRN, and paywalled databases accessible through the user's institutional library login via Chrome MCP.

After each tweak, we reviewed the updated SKILL.md to make sure the changes were fully reflected. When they weren't ("I didn't see tweak 1 and 2 fully reflected"), we pushed back and Claude revised.

## Step 4: Write Eval Test Cases

The skill-creator helped us write 3 eval test cases in `evals.json`, each testing a different scenario:

1. **Small seed set** (2 RAG papers provided, expects the skill to expand via search)
2. **No seed papers** (topic only --- chain-of-thought reasoning --- expects all papers found via web search)
3. **Cross-disciplinary with pausing** (LLMs for scientific discovery, expects step-by-step execution with user checkpoints)

Each eval specifies the prompt, expected output characteristics, and any files to include.

## Step 5: Test and Evaluate

We ran the evals and reviewed the output qualitatively. The skill-creator can also run quantitative benchmarks, but for this skill, qualitative review was more informative --- we looked at whether the 9 steps were all completed, whether index codes were used consistently, and whether the synthesis was genuinely analytical (not just paper-by-paper summaries).

## Step 6: Condense

After testing, we asked: *"How long is the current skill file, and do you think it's worthwhile making it more concise without losing clarity?"*

The verbose version was 351 lines. Claude produced a condensed version at 203 lines with tighter instructions. We kept both:

- `literature-researcher/` (condensed, 203 lines) --- recommended for most use
- `literature-researcher-verbose/` (351 lines) --- more guidance on edge cases

## Step 7: Package and Publish

We packaged each version as a `.skill` file (a zip archive containing the SKILL.md). Then we published everything to a public GitHub repo with a README, evals, and both skill versions.

## Lessons Learned

**Be specific in your step descriptions.** Don't say "analyze the papers." Say exactly what analysis means: what to look for, what format to output, what to name the file.

**Push back when changes aren't reflected.** Claude sometimes incorporates feedback partially. Review the diff and say so if something's missing.

**Create both a condensed and verbose version.** The condensed version performs better (fewer tokens, tighter instructions), but the verbose version serves as documentation and handles edge cases better.

**Write evals that test different modes.** Our 3 evals tested small seed sets, no seeds, and step-by-step execution with pausing. This caught issues that a single test wouldn't.

**Use the unified indexing system.** The `[NNN]-[S/D]` paper indexing turned out to be one of the most valuable features. It makes every claim in every step traceable back to a specific source file.

**Cite your sources.** We searched online and found the 9-step protocol originated from Jainam Parmar's prompt framework. We added an acknowledgment. If your skill builds on someone else's work, credit them.

**The skill-creator skill is your friend.** It handles the scaffolding (YAML frontmatter, file structure, eval format) so you can focus on the actual content and logic of your skill.
