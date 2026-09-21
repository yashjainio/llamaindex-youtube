# CLAUDE.md

Rules for all Claude Code sessions in this repository (the "LlamaIndex RAG Series" YouTube series).

1. **Full type hints.** All Python functions and methods must have complete type hints for every argument and return type. No untyped or partially typed signatures anywhere.

2. **Never touch `.env` contents.** Never read, open, print, or otherwise access the contents of any `.env` file, even while debugging. Environment variables are accessed only via `os.environ` (or `python-dotenv`'s `load_dotenv()`) inside running code.

3. **All installs go through the project conda env.** All packages must be installed inside the `.llama-index-youtube-env` conda environment (`conda activate ./.llama-index-youtube-env`) — never install packages globally or in any other environment.

4. **Notebook layout.** Each episode notebook lives directly in the project root (NOT in an `episodes/` subfolder), numbered by filename (e.g. `01_what_is_llamaindex.ipynb`, `02_vectorstoreindex_basics.ipynb`) so episodes are easy to find and open directly. The one exception is the final capstone episode, which gets its own numbered subfolder (currently `20_llamaindex_langgraph_agent/`) since it's a multi-file project rather than a single notebook.

5. **Independence.** Each episode notebook must be runnable independently — later episodes may import shared sample data from `data/`, but must not require re-running earlier notebooks first.

## About this repo

This is the **LlamaIndex RAG Series** — Jupyter notebooks (`01_what_is_llamaindex.ipynb`, `02_vectorstoreindex_basics.ipynb`, ... `NN_topic.ipynb`) teaching LlamaIndex episode by episode. Episode breakdown and channel links live in `README.md`.

## Creating YouTube title, description, and tags for an episode

When asked to create YouTube metadata for an episode (e.g. "create the youtube title, description and tags for episode N"):

1. Read the episode's notebook (`NN_topic.ipynb`) in full to understand what's actually built and demonstrated — the description must reflect the real code and demo, not a generic summary.
2. Follow the exact format below, modeled on past episodes. Keep section labels (`Title:`, `Description:`, `Tags:`) literal so the output can be copied straight into YouTube Studio.
3. Print the result directly in the chat by default. Only write it to a file if the user asks for one.

### Format

```
Title: <High-CTR hook phrase, curiosity/benefit/specific-result driven> in LlamaIndex

Description:
Github: https://github.com/yashjainio

Welcome back to the LlamaIndex RAG Series! 🚀🤖

In this video, we cover <topic> — <one-sentence definition of the concept, in plain terms>.

<One paragraph walking through what we actually build/demo in the notebook, in narrative order: setup -> action -> the proof/test that shows it works. Reference real function/class names from the code (e.g. VectorStoreIndex, QueryEngine, StorageContext.from_defaults(...)).>

By the end of this video, you'll understand:

✅ <checklist item 1 — core concept>
✅ <checklist item 2 — key API/class used>
✅ <checklist item 3 — key API/class used>
✅ <checklist item 4 — how it's wired up>
✅ <checklist item 5 — a nuance or gotcha>
✅ <checklist item 6 — the test/proof shown in the demo>
✅ <checklist item 7 — practical use case, optional>

Whether you're a beginner or an experienced developer, this episode will help you <one-sentence practical takeaway>.

💬 Don't forget to Like, Subscribe, and Comment what you learned today!

✨ Before you sleep, make sure you've learned something new. ✨

#LlamaIndex #RAG #AIProgramming #AICodingAssistant #AgenticAI #SoftwareEngineering #DeveloperTools #Programming #CodingTutorial #ArtificialIntelligence #DevOps #CloudComputing #AIAgents #CodeAutomation #DeveloperProductivity #TechEducation #MachineLearning #SoftwareDevelopment #Coding #TechTutorial #Developers

Tags:
LlamaIndex,<topic-specific tag>,<key class/API name>,<key class/API name>,LlamaIndex <topic>,LlamaIndex tutorial,RAG,<topic-specific tag>,<topic-specific tag>,LlamaIndex custom tools,building RAG applications,agentic RAG,LlamaIndex framework,LlamaIndex API tutorial,AI coding assistant,Python RAG,LlamaIndex RAG Series,RAG framework,LlamaIndex AI,LlamaIndex Python,Yash Jain,Agent,Yash Claude,Yash AI,Yash LLM
```

### Notes on each section

- **Title** — must end with `in LlamaIndex`. The lead-in should be a high-CTR, clickable hook, not a dry label — favor curiosity gaps, concrete results/numbers, or a bold claim over a flat "`<Concept> Explained:`" prefix. Don't default to "Explained" every time; vary the hook per episode based on what's genuinely surprising or useful in that notebook (e.g. what it unlocks, a gotcha it avoids, a before/after). Keep it to one line, no numbering/episode number in the title itself. The hook must stay generic to the episode's overall concept, not to one specific example/demo used to illustrate it — e.g. for a hybrid search episode that happens to demo filtering support tickets by status, hook on "combining metadata filters with vector search" broadly, not on "filtering support tickets" specifically, since the concept applies to any structured+semantic search, not just that one demo. When a title names two concepts from the notebook, use "and" instead of "vs" unless they're genuinely alternatives someone would choose between — e.g. "Documents and Nodes" (a Node is what a Document becomes after splitting, not a competing option) not "Documents vs Nodes"; reserve "vs" for real either/or comparisons like "LlamaIndex vs LangChain". The title must always name the episode's core concept explicitly, not just imply it through the hook — e.g. "Hybrid Search" for the hybrid-search episode, "Metadata Filtering" for the metadata-filtering episode, "VectorStoreIndex" for the VectorStoreIndex episode, "Documents and Nodes" for the Documents/Nodes episode, "RouterQueryEngine" for the router episode. Work the concept's actual name into the hook itself rather than leaving it to be inferred. Keep the full title (hook + the fixed `in LlamaIndex` suffix) around 60 characters or under where possible — YouTube truncates titles on mobile feeds and search around 55–60 characters, so put the core concept name and the sharpest part of the hook within the first 40 characters, since that portion stays visible even when the rest gets cut off. Favor concrete specifics — a real number, a named class/API, an actual before/after result the notebook demonstrates — over vague superlatives like "amazing" or "powerful"; specific, curiosity-driven hooks reliably out-click flat declarative ones. The hook is a promise: never open a curiosity gap the episode doesn't actually close, since misleading titles hurt click-through-rate quality signals and viewer trust over time.
- **Description** — always starts with the `Github: https://github.com/yashjainio` line and the "Welcome back" line verbatim. The checklist is 6–7 items using ✅, drawn from what the notebook's code and markdown cells actually cover — don't invent features not shown in the notebook. The closing hashtag block is fixed and reused verbatim across episodes (do not customize it per topic).
- **Formatting** — never use angle brackets (`<` or `>`) anywhere in the Title, Description, or Tags output — YouTube descriptions don't render them correctly. This includes arrow notation like `-->` for triplets/relationships; use a Unicode arrow (`→`) instead, e.g. `Naruto → Confronts → Pain`.
- **Tags** — comma-separated, no `#`. First few tags are topic-specific (concept name, key class/API names used in the notebook), followed by the fixed recurring tag set (`LlamaIndex custom tools`, `building RAG applications`, `agentic RAG`, `LlamaIndex framework`, `LlamaIndex API tutorial`, `AI coding assistant`, `Python RAG`, `LlamaIndex RAG Series`, `RAG framework`, `LlamaIndex AI`, `LlamaIndex Python`), ending with the personal branding tags verbatim: `Yash Jain,Agent,Yash Claude,Yash AI,Yash LLM`. **Print the tags in the chat joined with `, ` (comma + space) for readability** — but the 500-character limit must be computed against how YouTube itself counts the string, which is *not* the same as that display string's length. YouTube serializes tags as comma-separated with **no space after the comma**, and wraps **any tag containing a space in double quotes** — both the bare commas and the quote marks count toward the 500-character total. Concretely: `effective_length = Σ len(tag) for every tag, + (tag_count − 1) for the commas, + 2 × (number of tags containing a space) for their wrapping quotes`. This `effective_length` — not the length of the `, `-joined display string — must be **exactly 500 characters, strictly**. (A `, `-joined string of exactly 500 characters is NOT sufficient — it undercounts YouTube's real total by `2 × multi-word-tag-count − (tag_count − 1)`, so verify `effective_length` directly rather than reusing the display-string count.) Adjust the number/length of topic-specific tags at the front to hit exactly 500 on `effective_length` — never round to "close enough."
