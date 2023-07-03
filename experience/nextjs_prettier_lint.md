# 在 Next.js 项目中使用 ESLint 和 Prettier

在 Next.js 项目中，我们可以使用 ESLint 和 Prettier 来帮助我们校验和格式化代码。这样可以确保我们的代码质量和一致性，使得团队成员能更好地理解和维护代码。

## 一、安装相关依赖包

首先，我们需要安装一些相关的 npm 包，具体包括：

- `@typescript-eslint/eslint-plugin`TypeScript ESLint 插件，提供了一些针对 TypeScript 的 lint 规则。

- `@typescript-eslint/parser`TypeScript ESLint 解析器，用于解析 TypeScript 代码以供 ESLint 使用。

- `eslint-config-airbnb`和`eslint-config-airbnb-base`Airbnb 的 ESLint 规则配置，包含了一些对 JavaScript 和 React 的推荐规则。

- `eslint-config-prettier`用于关闭所有可能与 Prettier 冲突的 ESLint 规则。

- `eslint-import-resolver-alias`提供了导入路径别名解析的功能。

- `eslint-plugin-jsx-a11y`提供了一些针对 JSX 和 a11y 的 lint 规则。

- `eslint-plugin-prettier`让 ESLint 和 Prettier 更好地协同工作。

## 二、.eslintrc.js 配置

下面是我们在 .eslintrc.js 文件中的配置，具体解释如下：

```markdown
module.exports = {
  env: {
    browser: true, // 设置环境为浏览器
    node: true, // 设置环境为 Node.js
  },
  extends: [ // 使用的扩展配置
    'airbnb/base', // Airbnb 的基础 JS 规则
    'airbnb/hooks', // Airbnb 的 React Hooks 规则
    'airbnb/rules/react', // Airbnb 的 React 规则
    'next', // Next.js 的规则
    'prettier', // Prettier 的规则
  ],
  parser: '@typescript-eslint/parser', // 使用的解析器
  parserOptions: {
    ecmaFeatures: {
      jsx: true, // 开启 JSX
    },
    ecmaVersion: 2021, // 设置 ECMAScript 的版本
    sourceType: 'module', // 设置源代码类型为模块
  },
  plugins: ['jsx-a11y', '@typescript-eslint', 'prettier'], // 使用的插件
  rules: {
    // 具体的规则配置...
  },
  settings: {
    react: {
      version: 'detect', // 设置 React 版本为自动检测
    },
  },
};
```

## 三、VSCode 插件安装

在 VSCode 中，我们需要安装以下插件：

- ESLint：ESLint 插件可以在我们编写代码时

就实时地进行 lint，帮助我们发现和修复问题。

- Prettier - Code formatter：Prettier 插件可以帮助我们自动格式化代码，保持代码风格的一致性。

- Prettier ESLint：Prettier ESLint 插件可以让 Prettier 和 ESLint 更好地协同工作。

## 四、使用 Husky 和 lint-staged 进行代码校验

最后，我们使用 Husky 和 lint-staged 来在代码提交时进行代码校验，以确保我们提交的代码都是经过 lint 的。

Husky 可以帮助我们管理 git hooks，而 lint-staged 则可以在每次提交时运行特定的命令。我们可以用以下命令来安装它们：

```markdown
# 安装 Husky
yarn add husky --dev
yarn husky install
yarn husky add .husky/pre-commit "yarn lint-staged"

# 安装 lint-staged
yarn add lint-staged --dev
```

然后，在 package.json 中添加以下配置：

```markdown
"lint-staged": {
  "*.{js,jsx,ts,tsx}": [
    "eslint",
  ]
},
```

以及在 scripts 中添加以下配置：

```markdown
"lint-staged": "lint-staged"
```

这样，在我们每次提交代码时，就会自动运行 ESLint 进行代码校验了。