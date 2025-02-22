# Contextr

Contextr is a lightweight library that **packages your project’s code files into structured context**—ready to be consumed by Large Language Models (LLMs). It enables **single-shot code context generation** for LLM prompting and supports **dynamic packaging for LLM agents** that require iterative file submission.

## 🎯 Why We Built It: LLM Workflows Need Precision, Not Guesswork

Copilot, Replit, and other AI-assisted IDEs attempt to provide context, but they fall short in critical ways:

 - ***Limited & Unpredictable Context***: They typically rely on open file editors or recent edits, meaning you don’t fully control what gets sent to the AI.
 - ***Potentially Leaking Sensitive Files***: Without fine-grained selection, they may include files unintentionally, exposing sensitive or unnecessary data.
 - ***No Granular Control***: Customizing context in each tool’s own way is inconsistent and time-consuming, making AI-driven development slower, not faster.

## Why Contextr?

AI-assisted development needs a precise, structured way to send LLMs exactly what they need—nothing more, nothing less.

✅ Absolute Control Over Context: Hand-pick the exact files the AI sees, at the level of granularity of individual files.

✅ Works for Both Single-Shot & Automated Workflows: Whether working manually with LLMs or integrating AI-driven coding agents, pre-built context is faster and more reliable.

✅ Fits AI-Assisted Development Best Practices: Small files (under 200 lines, ideally 100) encourage modular design. This tool solves the problem of gathering multiple related files efficiently.

✅ Handles Distributed Code: Critical logic is often spread across shared/, providers/, schemas/, client/, and server/. This builder ensures you can package exactly what the AI needs for an end-to-end flow.

Build and send the precise LLM context you need, with full control, and stop relying on your IDE to do the guesswork.


# 🚀 Getting Started

### 1️⃣ &nbsp;&nbsp;**Install the Library**
You can install Contextr **directly from GitHub**:

```bash
yarn add contextr  
```

Or if you prefer npm:

```bash
npm i contextr
```

### 2️⃣ &nbsp;&nbsp;Define Your Context Configuration

Use a simple JSON-based config to select files for inclusion.

```ts
import {
  FileContextBuilder,
  FileCollectorConfig,
  ConsoleRenderer,
  JsonRenderer,
} from "contextr";

const config: FileCollectorConfig = {
  name: "MyProjectFileContext",
  showContents: true, // Include file contents
  showMeta: true,     // Include metadata (file paths, sizes, etc.)
  includeDirs: [
    {
      path: "./src",
      include: ["**/*.ts"], // Include all TypeScript files
      recursive: true,
    },
  ],
  includeFiles: ["README.md", "package.json"],
};

(async () => {
  const builder = new FileContextBuilder(config);
  const context = await builder.build();

  // Render as a console-friendly string
  const consoleRenderer = new ConsoleRenderer();
  console.log(consoleRenderer.render(context));

  // Render as a strongly-typed object literal.
  const jsonRenderer = new JsonRenderer();
  const output = jsonRenderer.render(context);
  console.log(output);
})();
```

## 🛠️ Extending the Output

Use Different Renderers

By default, two renderers are provided:
 - ConsoleRenderer → Outputs human-readable file trees and summaries.
 - JsonRenderer → Outputs structured JSON for LLM consumption.

You can create custom renderers by implementing the Renderer interface:

```ts
export interface Renderer<T = unknown> {
  render(context: FileContext): T;
}
```

## 🤝 Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for details on how to submit issues, bug fixes, and new features.

## 🔏 Code of Conduct

See [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) for Code of Conduct.

## Publishing

```npm version patch```

```npm publish```

## 📄 License

Contextr is licensed under the [MIT License](./LICENSE.md).