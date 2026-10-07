# ToolCoach

A local equipment-training website for plumbing employers: retrieve approved lessons, explore a 3D pipe schematic, and send missing lessons to a trainer review queue.

## Start

Requires Node.js 22+. No package installation is required.

```sh
node server.mjs
```

Open http://127.0.0.1:5180. Keep the terminal running. The server listens only on this computer.

## Demo

1. Choose **Try a sample task**, then **Try the 3D exercise**. Rotate/separate the pipe schematic and answer the component question.
2. In **Lesson library**, add a title, exact tool model and approved reference text/transcript. Optionally upload MP4/WebM footage under 25 MB and specify a start time in seconds. Explicit trainer approval is required before retrieval.
3. In **Training agent**, confirm the same model and ask a source-supported question. A matching video plays; a reference without footage becomes a draft storyboard in **Trainer review**.
4. An unsupported request becomes an expert content request. No procedure is invented.
5. Edit/download sourced scripts. Marking a draft reviewed does not publish it. Add final reviewed content through the lesson library.

## Google AI

Enter a Google AI Studio key in **Google AI setup**, with a model available to your project. Default: `gemini-3.8-flash`, following current Google image-understanding documentation. Saving configures the key; the next lesson request tests account access. You may instead set `GEMINI_API_KEY` and optionally `GEMINI_MODEL` before starting the server.

The key stays in server memory, is not saved to disk or returned to the browser, and is cleared at shutdown. When connected, Google receives the request, optional photo and approved references for that model.

Without a key, local mode uses keyword search and returns reference text verbatim. It does not analyze the photo. Google failures are explicit rather than silently replaced with demo results.

## Prototype limits

- Video generation is manual: download a reviewed storyboard and try it in Google Flow. Footage needs expert review.
- 3D is a prepared schematic, not photo reconstruction, physical simulation or measurement.
- Reference text and timestamps are supplied by the trainer; video indexing/transcription is not automated yet.
- All trainer controls are accessible locally; no employee/trainer authentication. Do not expose this server publicly.
- No TradesQuest integration until its API documentation and credentials are supplied.
- Practice results measure vocabulary, not certification or safe workmanship.
- Live Google AI cannot be verified without the user's key.

## Storage and files

Lessons, drafts and attempts persist in `local-data/workspace.json`. Uploaded videos are in `local-data/media/`. All local data and credentials are excluded from Git.

| File | Purpose |
| --- | --- |
| server.mjs | Local server, storage and Gemini workflow |
| dist/index.html | Website interface |
| dist/style.css | Responsive design |
| dist/app.js | Uploads, library, review and practice interactions |
| dist/model.js | Interactive WebGL model |
| AI_BUILD_LOG.md | AI tools and prompts log |

## GitHub

Repository: https://github.com/fridaytaev001/toolcoach (private). Application source, this README and the AI log are included. Local company material and keys are excluded. GitHub stores the code; run the website locally with the command above.

Upstream examples (research references; their application code was not copied):

- https://github.com/FirebaseExtended/codelab-ai-genkit-rag — Firebase/Genkit retrieval app; useful for a future company-library implementation.
- https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart — website plus Gemini research agent; its public web search needs adapting for approved internal training.
