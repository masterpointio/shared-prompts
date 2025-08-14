# shared-prompts

Masterpoint's open source collection of AI/LLM prompts, Cursor rules, and templates for more effective workflows.

## How to Use

You can keep it basic and copy individual Cursor Rules into projects or use `rule-tool` to create symlinks in multiple projects.

### Using `rule-tool` to symlink Cursor Rules in repos

[`rule-tool`](https://github.com/circleci-petri/rule-tool) is a go CLI tool that generates symlinks between a centrally managed Cursor Rules repo and various projects. The advantage is that you're able to reference or pull in the same central set of Cursor Rules across multiple projects.

```bash
shared-prompts/
└── rules/
    ├── dockerfile-best-practices.mdc
    ├── tf-root-module-layout.mdc
    └── tf-testing-child-module.mdc

project-A/.cursorrules/
├── tf-testing-child-module.mdc → ../../shared-prompts/rules/tf-testing-child-module.mdc
├── tf-root-module-layout.mdc → ../../shared-prompts/rules/tf-root-module-layout.mdc
└── ...

project-B/.cursorrules/
├── dockerfile-best-practices.mdc → ../../shared-prompts/rules/dockerfile-best-practices.mdc
├── tf-testing-child-module.mdc → ../../shared-prompts/rules/tf-testing-child-module.mdc
└── ...
```

To start using `rule-tool`,

1. Install rule-tool following [these instructions](https://github.com/circleci-petri/rule-tool?tab=readme-ov-file#usage).

2. Git clone this `shared-prompts` repo

   ```bash
   mkdir -p $HOME/tooling
   cd $HOME/tooling
   git clone git@github.com:masterpointio/shared-prompts.git
   ```

3. Export an env var `RULE_TOOL_PATH` that points to the shared-prompts repo,

   ```bash
   export RULE_TOOL_PATH=$HOME/tooling/shared-prompts
   ```

   You can also easily add this to your respective shell config,

   ```bash
   # bashrc
   echo 'export RULE_TOOL_PATH=$HOME/tooling/shared-prompts' >> ~/.bashrc

   # zshrc
   echo 'export RULE_TOOL_PATH=$HOME/tooling/shared-prompts' >> ~/.zshrc
   ```

   **Please note**, `rule-tool` by convention expects to find a folder named `rules` within the `RULE_TOOL_PATH` folder.

4. Call `rule-tool` and symlink rules from `shared-prompts` in your current project

   ```bash
   # example project
   cd $HOME/git/some-project

   # Option 1
   rule-tool # this will open up a terminal based GUI

   # Option 2
   # See: https://github.com/circleci-petri/rule-tool?tab=readme-ov-file#non-interactive-mode
   rule-tool --non-interactive --list
   ```
